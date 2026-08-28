# Termo de Entrega e Transferência de Responsabilidade

**Sistema:** CRM Clínico — consultório da Dr.ª Ivana Anapaz
**Endereço:** www.consultoriodraivanaanapaz.fyi
**Data da entrega:** ____ / ____ / ________

---

## 1. Partes

| | Nome | Contacto |
|---|---|---|
| **Responsável pelo desenvolvimento** | ________________________ | ______________ |
| **Titular do sistema e dos dados** | Dr.ª Ivana Anapaz | ______________ |

## 2. Objecto

Entrega do sistema de gestão clínica, incluindo aplicação, base de dados,
autenticação, domínio e documentação. A partir da data acima, a **titular
assume a responsabilidade pelos dados pessoais e de saúde** neles tratados,
na qualidade de responsável pelo tratamento.

## 3. Componentes entregues

| Componente | Identificação | Entregue |
|---|---|---|
| Aplicação | Repositório `crm-dra-ivanaanapaz`, ramo `main` | ☐ |
| Base de dados e autenticação | Projecto Supabase `jlzpujkykblqadzbojyj` | ☐ |
| Domínio | `consultoriodraivanaanapaz.fyi` | ☐ |
| Manual da utilizadora | `MANUAL.md` | ☐ |
| Documentação técnica | `DEPLOY.md` | ☐ |
| Documentação de segurança | `SECURITY.md` (canal cifrado) | ☐ |
| Relatório de auditoria | `AUDITORIA-SEGURANCA.md` (canal cifrado) | ☐ |

## 4. Acessos — registo

Este é o registo que responde à pergunta «quem teve acesso a quê, e desde
quando».

| Conta / acesso | Titular | Situação na data de entrega |
|---|---|---|
| Conta da aplicação (Supabase Auth) | Dr.ª Ivana Anapaz | ☐ Criada e testada |
| Conta de administração do desenvolvedor | ________________ | ☐ **ELIMINADA nesta data** |
| Painel Supabase | ________________ | ☐ Transferido / ☐ Mantido com autorização escrita |
| Repositório GitHub | ________________ | ☐ Transferido / ☐ Mantido com autorização escrita |
| Registo do domínio | ________________ | ☐ Transferido / ☐ Mantido com autorização escrita |

**Comprovação da eliminação do acesso aos dados clínicos:** após a eliminação
da conta de administração do desenvolvedor, foi executado o teste externo de
exposição, cujo resultado se anexa.

Resultado: `_______________________________`  Data/hora: `__________________`

## 5. Credenciais rodadas

| Credencial | Rodada em | Confirmado por |
|---|---|---|
| ____________________________ | ____ / ____ / ______ | ______________ |
| ____________________________ | ____ / ____ / ______ | ______________ |

## 6. Riscos conhecidos e aceites

A titular declara ter sido informada dos riscos documentados na secção 2 do
`SECURITY.md`, designadamente a ausência de restauro a um ponto no tempo, a
ausência de registo de auditoria por ficha, e o facto de a autenticação de
dois factores ainda não estar activa na aplicação.

**Rubrica da titular:** ______________

## 7. Obrigações da titular a partir desta data

- Manter a password pessoal, única e não partilhada
- Ativar a autenticação de dois factores na conta Supabase
- Realizar e guardar cópias de segurança periódicas
- Comunicar qualquer suspeita de acesso indevido
- Cumprir as obrigações de responsável pelo tratamento ao abrigo do RGPD
  (art. 9.º — categorias especiais) e da Lei angolana n.º 22/11

## 8. Assinaturas

| | Assinatura | Data |
|---|---|---|
| **Responsável pelo desenvolvimento** | ____________________ | ____ / ____ / ______ |
| **Titular** | ____________________ | ____ / ____ / ______ |

---

*Documento em duplicado, um exemplar para cada parte.*
