# DEPLOY.md

Processo de publicação e manutenção do CRM clínico.

## Arquitectura

```
Navegador → index.html (estático, GitHub Pages) → Supabase (Auth + Postgres)
```

Sem backend próprio, sem build, sem dependências de execução além de uma
biblioteca auto-alojada.

| Camada | Onde |
|---|---|
| Código | `martinsbcesar98-svg/crm-dra-ivanaanapaz`, ramo `main` |
| Alojamento | GitHub Pages, raiz do repositório |
| Domínio | `www.consultoriodraivanaanapaz.fyi` (ficheiro `CNAME`) |
| Base de dados e autenticação | Supabase, projecto `jlzpujkykblqadzbojyj` |

## Ficheiros

| Ficheiro | Papel |
|---|---|
| `index.html` | A aplicação inteira: HTML, CSS e JavaScript |
| `vendor/supabase-2.112.4.js` | Biblioteca auto-alojada, byte-a-byte igual ao npm |
| `vendor/README.md` | Proveniência e procedimento de verificação |
| `CNAME` | Domínio próprio — **não apagar** |
| `.gitignore` | Impede cópias de segurança e documentos internos de serem publicados |

## Publicar uma alteração

```bash
git add index.html
git commit -m "descrição"
git push origin main
```

O GitHub Pages reconstrói em cerca de um minuto. Verificar sempre a seguir:

1. Abrir o site e **entrar** — valida que o `vendor/` carregou
2. DevTools → Network → confirmar **zero pedidos a CDNs externos**
3. DevTools → Application → Local Storage → **só deve existir `sb-…-auth-token`**
4. Um carregamento da página **não deve gerar nenhum `POST`**

## Configuração

Não há variáveis de ambiente. Sendo uma aplicação estática, tudo o que o
navegador recebe é público por definição. A configuração está no topo do
`index.html`:

```js
window.CRM_CONFIG = { url: "<project url>", key: "<anon public key>" };
```

A chave `anon` é **pública por desenho** e a sua exposição não é um problema: a
protecção é a política de RLS no servidor, que só devolve linhas a
`auth.uid() = user_id`.

> **Nunca colocar aqui a chave `service_role`.** Essa ignora o RLS por completo.

## Actualizar a biblioteca do Supabase

```bash
npm pack @supabase/supabase-js@<versão>
tar xzf supabase-supabase-js-<versão>.tgz
openssl dgst -sha384 -binary package/dist/umd/supabase.js | openssl base64 -A
cp package/dist/umd/supabase.js vendor/supabase-<versão>.js
```

Actualizar o `<script>` no `index.html`, registar o novo hash em
`vendor/README.md`, **testar o login** e só depois publicar.

Não usar o `supabase.min.js` do jsDelivr: é gerado pela CDN e o seu hash não é
reproduzível a partir da origem.

## Base de dados

Uma tabela de dados e uma de histórico.

```
crm_dados      user_id (PK) | dados jsonb | atualizado_em | versao
crm_historico  id | user_id | dados | versao | guardado_em
```

Todo o CRM de um utilizador vive num único campo `jsonb`. As escritas usam
concorrência optimista pela coluna `versao`: o cliente envia `dados` e
condiciona em `.eq("versao", versaoLocal)`; um trigger `BEFORE UPDATE`
incrementa a versão e guarda a versão anterior no histórico, sem anexos, com
janela de 5 minutos e retenção de 20 versões.

O bloco do histórico tem tratamento de excepções próprio: **uma falha no
histórico nunca impede a gravação da utilizadora.**

### Manutenção

O SQL Editor corre como `postgres`, que tem `BYPASSRLS`, portanto a manutenção
funciona apesar do `FORCE ROW LEVEL SECURITY`.

## Repor o acesso de administração

Não existe script nem rota para isto, e é deliberado. As passwords são geridas
pelo Supabase Auth.

**Se a titular perder a password:** deve usar o fluxo de recuperação da própria
aplicação («Esqueci-me da password»). Requer que o SMTP esteja operacional.

**Se o fluxo de recuperação falhar:** Supabase → Authentication → Users →
seleccionar o utilizador → definir nova password. Requer acesso ao painel.

> Após a entrega, o acesso ao painel é da titular. Não existe conta de
> desenvolvedor com acesso aos dados — ver o termo de entrega.

## Criar uma conta

Supabase → Authentication → Users → **Add user**, com **auto-confirmar
ligado** (não consome envio de e-mail). O registo público está desligado, pelo
que ninguém se pode inscrever sozinho.

## Cópias de segurança

- **Automáticas:** diárias, pelo Supabase (plano gratuito, sem restauro a um
  ponto no tempo)
- **Manuais:** Definições → Exportar cópia, dentro da aplicação
- **Restauro:** Definições → Importar cópia (pede confirmação e substitui tudo)

Um backup que nunca foi restaurado não é um backup: testar o restauro pelo
menos uma vez.
