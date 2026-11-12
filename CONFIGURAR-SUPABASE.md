# Configurar a agenda compartilhada

A página usa o Supabase para compartilhar eventos e listas de funcionários/produtos entre os usuários autorizados.

## 1. Criar e configurar o projeto

1. Crie um projeto em [supabase.com](https://supabase.com/) e guarde a senha do banco em local seguro.
2. No **SQL Editor**, abra uma consulta nova e vazia, copie todo o conteúdo de `supabase-setup.sql` e execute. Não acrescente o script ao conteúdo de outra consulta.
3. Em **Project Settings → API** (ou **Data API**), copie a **Project URL** e a chave pública **anon / publishable**.
4. Cole esses valores em `supabase-config.js`, nos campos `url` e `anonKey`.
5. Em **Authentication → Settings**, desative o cadastro público de usuários (sign-ups). Crie/invite somente as contas dos funcionários que devem ter acesso. Todos os usuários autorizados deste projeto compartilham a mesma agenda.
6. Publique `index.html` e `supabase-config.js` juntos no GitHub Pages. O SQL é executado no Supabase, não precisa ser publicado junto com a página.

Exemplo de configuração (substitua pelos valores do seu projeto):

```js
window.AGENDA_SUPABASE_CONFIG = {
  url: "https://seu-id.supabase.co",
  anonKey: "sua-chave-publica"
};
```

Use somente a chave pública `anon`/`publishable` no navegador. **Nunca** coloque `service_role`, senha do banco ou outra chave secreta em `supabase-config.js` ou no GitHub. A chave pública é destinada ao cliente; as políticas de Row Level Security criadas pelo SQL limitam a leitura e alteração a usuários autenticados. Mantenha o cadastro público desativado e conceda contas apenas à equipe.

## 2. Usar a agenda

Abra a URL do GitHub Pages, entre com a conta criada para o funcionário e cadastre os eventos. As listas de funcionários e produtos começam vazias; adicione os itens reais da equipe pelo formulário de evento. As alterações são gravadas no Supabase e os outros usuários recebem os dados ao atualizar a página, clicar em **Atualizar** ou aguardar a sincronização automática.

O arquivo não transfere automaticamente os eventos que tenham sido salvos anteriormente no armazenamento local de um navegador. Se já houver dados importantes nessa agenda antiga, exporte/registre-os antes de migrar.
