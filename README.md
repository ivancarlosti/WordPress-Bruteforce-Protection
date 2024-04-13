Artigo: https://suporte.ivancarlos.com.br/hc/pt-br/articles/23669601566605

<p>
  WordPress é a plataforma CMS (sistema de gerenciamento de conteúdo) mais utilizada
  do mundo, com isso, é adotada por empresas de todos os tamanhos para todo tipo
  de uso, desde um blog pessoal a um portal de notícias completo, passando por
  sites institucionais, sistemas de licenciamento, de agenda, de tickets, enfim,
  as possibilidades são infinitas.
</p>
<p>
  Por esse motivo, essa também uma das plataformas mais visadas em busca de falhas,
  tornando ela uma vítima dos ataques de força bruta e sendo exploradas por vulnerabilidades
  de plugins que o administrador tenha instalado.
</p>
<p>
  Para evitar esse tipo de problema, uma boa forma de proteção, além dos plugins
  clássicos sugeridos em outro artigo e a infraestrutura de borda, são as proteções
  implementadas no arquivo <em>.htaccess</em> (para servidores web Apache HTTP
  Server, por exemplo) para direcionar as requisições feitas ao servidor.
</p>
<p>
  O código no link a seguir é uma sugestão de implementação para Apache que, em
  ordem, bloqueia solicitações ao arquivo xmlrpc.php, impede requisições POST feitos
  diretamente ao wp-login.php sem passar pela página de login, bloqueia solicitações
  de determinados agentes ao wp-login.php.
</p>
<p>
  GitHub:
  <a href="https://github.com/ivancarlosti/WordPress-Bruteforce-Protection/blob/main/.htaccess" target="_blank" rel="noopener noreferrer">https://github.com/ivancarlosti/WordPress-Bruteforce-Protection/blob/main/.htaccess</a>
</p>
<p>Note que a linha 11 deve ser alterada para seu domínio.</p>
<p>
  Caso você utilize algum serviço de pacote do WordPress, como o Bitnami, você
  precisará verificar qual a lógica de funcionamento do seu <em>.htaccess</em>.
  No caso do Bitnami, usualmente o <em>.htaccess</em> do WordPress fica localizado
  em <em>/opt/bitnami/apache/conf/vhosts/htaccess/wordpress-htaccess.conf</em>,
  e as linhas adicionadas devem estar inclusas dentro de uma chave
  <em>&lt;Directory&gt;</em>. Veja mais em
  <a style="background-color: #ffffff;" href="https://docs.bitnami.com/aws/apps/wordpress/administration/use-htaccess/" target="_blank" rel="noopener noreferrer">Understand Default .Htaccess File Configuration</a>
  para mais informações, lembrando que, caso você use a chave
  <em>&lt;Directory "/opt/bitnami/wordpress"&gt;</em> em uma instalação Bitnami,
  também é preciso trazer o conteúdo já existente em
  <em>/opt/bitnami/wordpress/.htaccess</em>, o mesmo vale para se você possuir
  plugins que editem o <em>.htaccess</em>.
</p>
<p>
  Para servidores NGINX, o processo é feito na configuração do vhost, adicionando
  2 trechos de código, a depender do uso, apontados no arquivo do link a seguir:
</p>
<p>
  GitHub:
  <a href="https://github.com/ivancarlosti/WordPress-Bruteforce-Protection/blob/main/nginx.conf">https://github.com/ivancarlosti/WordPress-Bruteforce-Protection/blob/main/nginx.conf</a>
</p>
<p>
  Note que o trecho "Block login bruteforce attempt on wp-login.php block" deve
  ser inserido dentro do location
  <span style="color: #1f2328; font-family: -apple-system, BlinkMacSystemFont, ' Segoe UI' , ' Noto Sans' , Helvetica, Arial, sans-serif, ' Apple Color Emoji' , ' Segoe UI Emoji' font-size:16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; white-space: normal; background-color: #ffffff; text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;">"~/(wp-admin/|wp-login.php)" caso exista, se não, declare o location e insira o trecho nele.</span>
</p>
<p>
  Estratégias para forçar redirecionamentos para https e também para mover usuários
  para o domínio correto, como de sites com subdomínio para sem subdomínio ou vice
  versa também são recomendados. Essas estratégias estão declaradas nos links a
  seguir:
</p>
<p>
  GitHub:
  <a href="https://github.com/ivancarlosti/WordPress-Bruteforce-Protection/blob/main/.htaccess-redirect">https://github.com/ivancarlosti/WordPress-Bruteforce-Protection/blob/main/.htaccess-redirect</a>
</p>
<p>
  GitHub:
  <a href="https://github.com/ivancarlosti/WordPress-Bruteforce-Protection/blob/main/nginx-redirect.conf">https://github.com/ivancarlosti/WordPress-Bruteforce-Protection/blob/main/nginx-redirect.conf</a>
</p>
<p>
  E para finalizar, um bloco de NGINX para quem estiver com dificuldade para fazer
  o CORS funcionar em aplicações específicas como uso de domínio próprio na rede
  Nostr, ou o uso de domínio próprio como endereço de carteira Lightning:
</p>
<p>
  GitHub:
  <a href="https://github.com/ivancarlosti/WordPress-Bruteforce-Protection/blob/main/nginx-cors.conf">https://github.com/ivancarlosti/WordPress-Bruteforce-Protection/blob/main/nginx-cors.conf</a>
</p>
<p>
  <strong>Fonte:</strong>
</p>
<ul>
  <li>
    <a href="https://docs.bitnami.com/aws/apps/wordpress/administration/use-htaccess/" target="_blank" rel="noopener noreferrer">Bitnami Documentation</a>
  </li>
  <li>
    <a href="https://reggiodigital.com/blog/nginx-rule-blocking-bad-bots/" target="_blank" rel="noopener noreferrer">Reggio Digital</a>
  </li>
</ul>
