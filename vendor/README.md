# vendor/

## supabase-2.112.4.js

Cópia **byte-a-byte** de `@supabase/supabase-js@2.112.4`, ficheiro `dist/umd/supabase.js`,
obtida do tarball oficial do npm. Auto-alojada para eliminar a dependência de CDN de
terceiros numa aplicação que manipula dados clínicos (achado A6 da auditoria).

- Tamanho: 212 426 bytes
- SHA-384: `sha384-ysv13JVP3fufiEXfjML9OdCa/rRbMJvUBOWyor82wfuK8INNZAvmbxHgKIHi+oqz`

O ficheiro **não** foi modificado (nem sequer com um cabeçalho de comentário), para que o
hash acima possa ser verificado directamente contra a origem:

```bash
npm pack @supabase/supabase-js@2.112.4 && tar xzf supabase-supabase-js-2.112.4.tgz
openssl dgst -sha384 -binary package/dist/umd/supabase.js | openssl base64 -A
diff package/dist/umd/supabase.js vendor/supabase-2.112.4.js   # tem de ser vazio
```

### Ao actualizar
Repetir o procedimento com a nova versão, criar um ficheiro novo com o número de versão no
nome, actualizar o `<script>` no `index.html` e **testar o login** antes de publicar.

Nota: o `supabase.min.js` servido pelo jsDelivr é gerado pela própria CDN e não é um
artefacto publicado pelo Supabase — o seu hash não é reproduzível a partir da origem.
Por isso vendorizamos o `supabase.js` não minificado.
