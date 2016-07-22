[Voltar aos conteúdos](README.md)


### Estatísticas dos bugs divulgados publicamente pela Hackerone

Enquanto este documento é escrito, a plataforma Hackerone teve 1731 bugs divulgados abertamente em empresas como Twitter, Uber, Dropbox, Github, etc.

8 dos bugs foram removidos spam total. 9 eram relacioandos à linguagem de programação ou à Internet em geral. Dos 1714 restantes, conseguimos classificar 1359 problemas usando um pouco de código e trabalho manual.

    
    

#### Problemas por tipo de erro


| Classificação | Quantidade | Porcentagem |
| --- | --- |  --- |
| Sanitização de Entrada de Usuário        | 481      | 27.8
| Outros problemas de código              | 549      | 31.7
| Problemas de Configuração           | 325      | 18.8
| Sem classificação + lixo + informações         | 376      | 21.7


#### Problemas organizados pela sua frequência de ocorrência

A cada 3 problemas, 1 era relacionado a XSS, referências inseguras a dados (vazamento de dados) ou falta de token CSRF. A listagem dos problemas da [página do Hackerone](https://hackerone.com/hacktivity/new)  é bem interessante, dá uma lida lá.

Tipo|Contagem|Porcentagem
| --- | --- | --- |
XSS|375|21.87
Referência Insegura + Vazamento de dados|104|6.06
Token CSRF|99|5.77
Redirects abertos|59|3.44
Divulgação de informações/código fonte|57|3.32
DNS mal-configurado + Apache/Nginx + Roubo de subdomínio +  AWS_S3 aberto |44|2.56
Manutenção/fixação de sessão imprópria|39|2.27
TLS/SSL/POODLE/Heartbleed|39|2.27
Injeção de HTML/JS/XXE/conteúdo|37|2.15
Problemas com cabeçalhos HTTP|34|1.98
NULL POINTER + SEGFAULT + uso de memória após free()|33|1.92
configurações DMARC/DKIM/SPF de Mail|31|1.8
SQL Injection|28|1.63
Sequestro de click (clickjacking) |27|1.57
Cookies impróprios (secure/httpOnly/exposed)|25|1.45
Divulgação de caminhos/rotas|25|1.45
Autenticação aberta / quebrada|24|1.4
Ataques de força bruta|24|1.4
Conteúdo falso (content spoofing)|20|1.16
Estouro de buffer|20|1.16
Negação de serviço|19|1.1
Falsificação de Requisições pelo Servidor|18|1.05
Vulnerabilidades do Adobe Flash |18|1.05
Enumeração de Usuários/Informações|17|0.99
Execuções de Código Remoto|15|0.87
Expiração/Tentativas/Outras ações com Token de redefinição de senha|13|0.75
Estouro de Inteiro|11|0.64
Divulgação de Versão|11|0.64
Injeção de CSV |10|0.58
Escalamento de Privilégico|9|0.52
Vazamento/estado de OAuth e outros problemas|9|0.52
Política de Senha|7|0.4
CRLF|7|0.4
PythonLang|6|-0.65
Ataque Homógrafo|6|0.35
Sanitização de tipo/tamanho/localidade de upload de arquivo|6|0.35
Burlagem de Captcha|5|0.29
Inclusão de arquivo remoto/local|4|0.23
Listagem de diretório|4|0.23
Caminho traversal|4|0.23
Upload de arquivo remoto|4|0.23
Autocompletar habilitado|4|0.23
Vazamento via referer|3|0.17
Ataque de flood de píxel|3|0.17
Controle de caracteres de entrada|2|0.11


### Alguns tipos únicos de vulnerabilidades

1. Vulnerabilidades baseadas em Race Conditions
2. Ataque de Flood de Pixels
3. Ataque de IDN Homógrafo
4. Controle de caracteres de entrada, levando a retornos interessantes
