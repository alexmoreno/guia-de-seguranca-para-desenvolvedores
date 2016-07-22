[Voltar aos conteúdos](README.md)


### O Checklist de Segurança

##### SISTEMAS DE AUTENTICAÇÃO (Registro/Login/2 fatores/Reset de senha) 
- [ ] Usar HTTPS em todo lugar.
- [ ] Armazenar hashes de senha usando `Bcrypt` (não precisa de salt - `Bcrypt` faz isso) pra você.
- [ ] Destruir o identificador de sessão após deslogar
- [ ] Destruir todas as sessões ativas ao resetar a senha (ou ao solicitar).  
- [ ] Deve haver o parâmetro `state` no OAuth2.
- [ ] Sem redirecionamento abertos depois de um login bem-sucedido ou em qualquer redirecionamento intermediário	
- [ ] Quando parsear a entrada de Registrar/Logar, sanitize por javas javascript://, data://, caracteres CRLF. 
- [ ] Cookies seguros, httpOnly.
- [ ] Na verificação mobile baseada em `OTP`, não envie o OTP de volta na resposta quando as chamadas de API de `generate OTP` ou `resend OTP` forem chamadas.
- [ ] Limite as tentativas de chamadas de API para `Login`, `Verify OTP`. `Resend OTP` `Generate OTP` de um usuário individual. Tenha uma barreira exponencial e/ou algo como um desafio baseado em captcha.
- [ ] Cheque aleatoriedade nos tokens de reset de senha no link do email ou SMS. 
- [ ] Sete um tempo razoável de expiração no token de reset de senha.
- [ ] Expire o token de reset depois de ser usado com sucesso.
- [ ] Destrua a sessão de usuário logado em todos os lugares após um reset de senha. 


##### DADOS DE USUÁRIO & AUTENTICAÇÃO
- [ ] Qualquer recurso tipo, `meu carrinho`, `meu histórico` deve checar se o usuário logado é realmente o dono do recurso.
- [ ] IDs de recursos serialmente ieráveis devem ser evitados. Use `me/orders` ao invés de `/user/37153/orders`. Serve como checagem de sanitização caso tenha esquecido de checar o token de autorização. 
- [ ] O recurso `Editar email/número de telefone` deve ser acompanhado de uma verificação de email e telefone ao dono da conta. 
- [ ] Qualquer recurso de upload deve sanitizar o nome do arquivo fornecido pelo usuário. Por razões não necessariamente de seguranças, faça o upload em algo tipo o S3 (e faça um pós-processo usando Lambda) e não no seu server capaz de executar códigos.  
- [ ] O recurso `Upload de foto de perfil` deve sanitizar todos os `EXIF`s se não for obrigatório.
- [ ] Para ids de usuário e outros ids, use  `UUID`s [compatíveis com RFC ](http://www.ietf.org/rfc/rfc4122.txt) `UUID` ao invés de inteiros. Você pode achar uma implementação disso na sua linguagem aqui no github mesmo.
- [ ] JWT são ótimos, use se precisar nos seus SPAs/APIs.


##### APPS ANDROID / IOS 
- [ ] `salt`  dos gateways de pagamento não devem ser chumbados.
- [ ] `secret` / `auth token` de SDK de terceiros não devem ser chumbados.
- [ ] Chamadas de API que deveriam ser feitas de servidor para servidor não devem ser feitas pelo app.
- [ ] No Android, todas as [permissões](https://developer.android.com/guide/topics/security/permissions.html) garantidas devem ser avaliadas cuidadosamente.
- [ ] [Fixaxão de certificado](https://en.wikipedia.org/wiki/HTTP_Public_Key_Pinning) é altamente recomendado.


##### CABEÇALHOS DE SEGURANÇA E CONFIGURAÇÕES
- [ ] `adicione` cabeçalhos [CSP](https://en.wikipedia.org/wiki/Content_Security_Policy) para mitigar ataques de XSS e injeção de dados. Isso é importante.
- [ ] `adicione` cabeçalhos [CSRF](https://en.wikipedia.org/wiki/Cross-site_request_forgery) para prevenir falsificação de requisição entre sites.
- [ ] `adicione` cabeçalhos [HSTS](https://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security) para prevenir ataque de desforramento de SSL. 	
- [ ] `adicione` [X-Frame-Options](https://en.wikipedia.org/wiki/Clickjacking#X-Frame-Options) para proteger de sequestro de cliques.
- [ ] `adicione` cabeçalhos [X-XSS-Protection](https://www.owasp.org/index.php/OWASP_Secure_Headers_Project#X-XSS-Protection) para mitigar ataques XSS.
- [ ] Update DNS records to add [SPF](https://en.wikipedia.org/wiki/Sender_Policy_Framework) record to mitigate spam and phishing attacks.
- [ ] adicione [checagem de integridade de subrecursos](https://en.wikipedia.org/wiki/Subresource_Integrity) se carregar seus javascripts de um CDN externo.
- [ ] Use tokens CSRF aleatórios e exponha APIs de lógicas de negócio em forma de requisições HTTP POST. Não exponha os tokens CSRF em HTTP numa requisição inicial de upgrade, por exemplo.
- [ ] Não coloque dados críticos ou tokens em parâmetros GET. Exposição de logs de servidores ou processamento de máquina/pilha neles iriam expor dados dos usuários.

##### SANITIZAÇÃO DE ENTRADA
- [ ] `Sanitize` todas as entradas de usuário ou qualquer parâmetro exposto ao usuário para prevenir [XSS](https://en.wikipedia.org/wiki/Cross-site_scripting)
- [ ] `Sanitize` todas as entradas do usuário ou qualquer parâmetro expoto ao usuário para prevenir [Injeção de SQL](https://en.wikipedia.org/wiki/SQL_injection)
- [ ] Sanitize as entradas de usuário se for usá-las diretamente para funcionalidades como importação de CSV.
- [ ] `Sanitize` entradas de usuário para casos especiais como robots.txt como nomes de perfis caso você esteja usando um padrão de URL tipo empresadahora.io/username. 
- [ ] Não concatene ou construa JSON manualmente, nunca, independente do quão pequeno o objeto é. Use as bibliotecas definidas pela sua linguagem ou framework.
- [ ] Sanitize entradas que recebam algum tipo de URL para prevenir[SSRF](https://docs.google.com/document/d/1v1TkWZtrhzRLy0bYXBcdLUedXGb9njTNIJXa3u9akHM/edit#heading=h.t4tsk5ixehdd).
- [ ] Sanitize as saídas antes de exibí-las ao usuário

##### OPERAÇÕES
- [ ] Se você é pequeno e inexperiente, avalie o uso de AWS elasticbeanstalk ou um PaaS para executar seu código.
- [ ] Use um script de provisionamento decente para criar VMs na nuvem..
- [ ] Cheque por máquinas com `portas abertas` publicamente que não deveriam estar.
- [ ] Cheque por banco de dados sem senha ou com senhas defaults para `databases`, especialmente com MongoDB e REDIS. A propósito, MongoDB é uma merda, evite.
- [ ] Use SSH para acessar suas máquinas, não use senhas.
- [ ] Instale atualizações pontualmente para lidar com 0day tipo Heartbleed, ShellShock.
- [ ] Modifique as configurações do servidor para usar TLS 1.2 para HTTPS e desabilite todos os outros esquemas (o retorno é bom).
- [ ] Não deixe o DEBUG ligado. Em alguns frameworks, DEBUG pode dar acesso a REPL totalmente prometidos ou shells, ou expor dados críticos no rastro de pilha das mensagens de erro. 	
- [ ] Esteja preparado para vilões e DDoS - use  [Cloudflare](https://www.cloudflare.com/ddos/)
- [ ] Monitoramento de configurações para seus sistemas e logs gerais (use [New Relic](https://newrelic.com/) ou algo do gênero)
- [ ] Se estiver desenvolvendo para empresas, faça adesão a requisitos de conformidade. Se usar AWS S3, considere usar o recurso de [criptografia de dados](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html). Se estiver usando AWS EC2, considere usar o recurso de volumes criptografados (agora até os volumes de boot podem ser encriptados )

##### PESSOAS
- [ ] Configure um email (tipo seguranca@empresalegal.io) e uma página para pesquisadores de segurança reportarem vunerabilidades.
- [ ] Dependendo do que você estiver fazendo, limite os acessos aos bancos de dado do seu usuário.
- [ ] Seja gentil com reportadores de bugs.
- [ ] Tenha seu code review feito por um amigo desenvolvedor de uma perspectiva de código seguro. (Quanto mais olhos, melhor)
- [ ] Em caso de ser hackeado ou brecha de dados, cheque os logs antigos de acesso de dados, peça às pessoas para trocarem suas senhas. Você pode solicitar uma auditoria com agências externas dependendo de onde você está instalado..  
- [ ] Configure [Netflix's Scumblr](https://github.com/Netflix/Scumblr) para ouvir sobre o que falam da sua empresa em mídias sociais e pesquisas do Google.
