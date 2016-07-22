# Guia prático de segurança para desenvolvedore web

### O Público Alvo

Problemas com segurança acontecem por 2 razões - 

1. Desenvolvedores que acabaram de começar a programar e não sabem dizer a diferença entre usar MD5 ou bcrypt.
2. Desenvolvedores que sabem das coisas, mas esquecem/ignoram.

Nossas explicações detalhadas devem ajudar a primeira categoria enquanto esperamos que nosso checklist ajude a segunda a criar sistemas mais seguros. Não é o intuito aqui criar um guia compreensivo, apenas a abranger elementos baseados nos problemas mais comuns que descobrimos no passado.



### Conteúdo

1. [Checklist de Segurança](security-checklist.md)
2. O que pode dar errado?
3. Transportando dados de forma segura: HTTP explicado
4. Eu sou quem digo que sou: Autenticação 	
4.1 Autenticação baseada em formulário			
4.2 Autenticação básica			
4.3 Um não é o suficiente: 2 fatores, 3 fatores... 			
4.4 Por que usar mensgens de texto inseguras? HOTP & TOTP 		
4.5 Lidando com reset de passwords 		
5. O que eu posso fazer? Autorização	
5.1 Autorização baseada em token	
5.2 OAuth & OAuth2  	
5.3 JWT	
6. Não confie em ninguém: Entradas (inputs) de usuários são DO MAL	
6.1 Sanitizando Entradas  	
6.2 Sanitizando Saídas 	
6.3 Scriptação Entre Sites (Cross Site Scripting aka XSS)  	
6.4 Ataques de Injeção (Injection) 		
6.5 Uploas de Usuário 	
6.6 Entradas de usuários à prova de alterações 	
7. Texto puro (plaintext) != Codificação (encoding) != Criptografia  != Hashing  	
7.1 Esquemas comuns de codificação 		
7.2 Criptografia 	
7.3 Hashing & Funções de uma via 	
7.4 Guia rápido de velocidade de hashing 	
8. dadada, 123456, futebol@123: Senhas 	
8.1 Políticas de Senha 			
8.2 Armazenamento de Senhas  	
8.3 Uma Vida sem Senhas 	
9. Chave Pública de Criptografia  	
10. Por favor, lembre-se de mim: Lidando com Sessões 		
10.1 Onde salvar o estado?   		
10.2 Invalidando sessões   	
10.3 O monstro dos cookies & você 	
11. Consertando a Segurança, um cabeçalho de cada vez  	
11.1 Cabeçalhos web seguros 	
11.2 Checagem de integridade de dados para códigos de terceiros 	
11.3 Fixando Certificados 	
12. Erros de Configuração 
12.0 Provisionamento em nuvem: Portas, Shodan & AWS 	
12.1 Amor, você deixou o debug ligado 	
12.2 Logar (ou não logar) 	
12.3 Monitoramento  	
12.4 Princípio do Menos Privilegiado 	
12.5 Limitação de Avaliações & Captchas  	
12.6 Armazenando de segredos de projetos e senhas em arquivo 	
12.7 DNS: De subdomínios e projetos menores esquecidos  	
12.7 Patching & Updates  	
13. Quando o vilão chega: Ataques 	
13.1 Sequestro de cliques 	
13.2 Falsificação de Requisições Entre Sites (CSRF) 	
13.3 Negação de Serviço (DoS) 	
13.4 Falsificação de Requisições pelo Servidor (SSRF) 	
14. [Estatísticas sobre vulnerabilidades encontradas em empresas de internet](vulnerabilities-stats.md)    
15. Sobre reinventar a roda, e torná-la quadrada 		
15.1 Bibliotecas e pacotes de segurança para Python  	
15.2 Bibliotecas e pacotes de segurança para Node/JS 	
15.3 Aprendendo sobre Recursos 
16. Mantendo uma boa higiene de segurança 
17. Segurança vs Usabilidade 
18. Voltando pra casa 1: O Checklist de Segurança explicado 
 



### Quem somos?

Somos desenvolvedores fullstack cansados de observar como os desenvolvedores diminuem a barreira para chamar alguma coisa de hack, escrevendo código inseguro. Nos últimos 6 meses prevenimos leaks de mais de 15 milhões de cartões de créditos, dados pessoais de mais de 45 milhões de usuários e potencialmente salvamos empresas de fecharem as portas. Recentemente, descobrimos um problema que poderia resultar no roubo de sistema e vazamento de dados numa instituição de bitcoin. Ajudamos algumas startups a protegerem seus sistemas, a maioria delas de graça, e às vezes sem nem receber um "obrigado" como resposta. :)

* Se você discorda de algo ou achou um bug, por favor abra um issue ou ande um PR. Alternativamente, pode falar conosco em hello@fallible.co (em inglês por que né)*.

**Nota: Esse repositório é uma tradução do projeto forkado. A tradução é minha mas o conteúdo é todo deles. Sinta-se a vontade para me sugerir mais conteúdos aqui no githubss pra traduzir.**