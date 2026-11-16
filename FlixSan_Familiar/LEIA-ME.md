# FlixSan Familiar V2

## Incluído
Aplicação React/Vite responsiva; autenticação Supabase; papel Master; convites por e-mail (lista de autorização, sem envio automático); ativação e bloqueio de moradores; papéis Master/Admin/Membro; cadastro, edição e exclusão de conteúdo; favoritos e progresso sincronizados para conteúdo cadastrado; player HTML5; exemplos gratuitos; políticas de acesso no banco (RLS).

## Implantação (obrigatória)
1. Crie um projeto Supabase ou use um projeto exclusivo para FlixSan. No **SQL Editor**, execute `supabase/setup.sql`.
2. Em **Authentication > Providers > Email**, habilite e-mail/senha. Recomenda-se confirmação de e-mail. Em **Authentication > URL Configuration**, configure o domínio Netlify final como Site URL e URL de redirecionamento. Para acesso exclusivamente familiar, desative cadastros públicos após criar todos os moradores; nesse caso, novos moradores precisam ser criados pelo painel de autenticação Supabase, além de serem convidados no FlixSan.
3. Copie `.env.example` para `.env` e preencha a URL e a chave **publishable/anon** do projeto (nunca a `service_role`).
4. Execute `npm install` e `npm run dev` para testar localmente.
5. Crie sua conta pelo formulário de cadastro e confirme o e-mail. No SQL Editor execute, substituindo o e-mail:
   `update public.profiles set role='master', active=true where email='SEU_EMAIL';`
6. Recarregue o aplicativo. Na aba Master, autorize os e-mails dos moradores. Eles devem criar conta com exatamente os e-mails autorizados. **Se o morador já tiver se cadastrado antes do convite**, o Master deve ativá-lo em Pessoas autorizadas; o convite não ativa retroativamente.
7. Suba o projeto no GitHub e conecte o repositório ao Netlify. Configure as variáveis `VITE_SUPABASE_URL` e `VITE_SUPABASE_ANON_KEY` no Netlify antes de publicar. Build `npm run build`, pasta `dist`.

## Limites e próximos componentes
- Esta entrega é um **aplicativo funcional com backend configurável**, não um serviço já publicado. Precisa da configuração do Supabase/Netlify.
- O catálogo demonstrativo não representa direitos sobre filmes comerciais. Use somente conteúdo próprio, licenciado ou autorizado.
- O player usa URLs diretas de vídeo compatíveis com navegador. Torrents, DRM, transcoding, biblioteca de arquivos grandes, legendas externas e app nativo de TV exigem um servidor de mídia ou integração posterior.
- Smart TVs: acesso pelo navegador quando suportado ou transmissão via AirPlay/casting; compatibilidade com controles e codecs varia por modelo.
- Os vídeos não ficam armazenados no Supabase nesta versão; ele armazena metadados e histórico.
- A política de autorização de convidados é aplicada ao criar conta. Convites não enviam e-mails automaticamente. Perfis bloqueados não conseguem consultar o catálogo.
- Em dispositivos compartilhados, use senhas individuais e não compartilhe credenciais Master.
