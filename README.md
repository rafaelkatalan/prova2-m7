Aplicação  consiste em duas instâncias EC2 e um banco de dados RDS. Uma instância EC2 é responsável por servir o front-end da aplicação, enquanto a outra executa o back-end.

## 2. Arquitetura

A arquitetura da aplicação é a seguinte:

- **Front-prova**: Esta instância EC2 roda com o sistema operacional Ubunto e é responsável por hospedar o servidor Apache que serve o front-end da aplicação. Ela foi criada permitindo o acesso dela de http e https. Ele recebe solicitações HTTP dos clientes e fornece a interface da aplicação e permite vizualizações das notas, criação das notas e exclusão das notas. Para fazer esta parte funcionar foi instalado o apache2, este repositorio do github foi clonado, onde o endereço das rotas do backend já estão configurados com o IP elastico do EC2 onde esta rodando o backend.


- **Back-prova**: Esta instância EC2 roda com o sistema operacional Ubunto e executa o back-end da aplicação. Ela processa solicitações do front-end e interage com o banco de dados RDS para armazenar, ler e excluir dados. Um IP elástico também é atribuído a esta instância para facilitar a comunicação com o front-end e garantir que meu ip publico será sempre o mesmo. Para ela poder ser acessada publicamente também foi necessario redirecionar as requisições http nela da porta 80, que é aberta, para a porta 8000 que é onde esta sendo servida a aplicação com o uvicorn. Para rodar a aplicação foi clonado este repositorio do github, foram instaladas as bibliiotecas e dependencias necessarias. Para o acesso ao banco de dados funcionar, foram alteradas as credenciais do RDS para acesso ao banco de dados dentro do EC2. 

- **RDS**: O banco de dados RDS armazena os dados da aplicação, como informações de usuários, conteúdo e configurações. O back-end se conecta ao RDS para acessar e gerenciar os dados. Para isso ser possivel foi criado uma instância de RDS com PostgreSQL na AWS com acesso publico e foi necessario mudar as regras de segurança para liberar acessos por TCP. Para carregar o banco de dados foram executados os comandos SQL que criam as tabelas necessarias atravez do DBeaver. Para o back-end poder se comunicar o banco de dados ele usa o endereço do host do banco de dados e o usuario e senha que foram configurados na criação da instância.

Seguem algumas imagens que demonstram o uso da aplicação:


Primeira pagina front:

![Primeira pagina front](/media/Captura%20de%20tela%202023-09-29%20140745.png)

Após adicionar 1 nota:
![Primeira pagina front](/media/Captura%20de%20tela%202023-09-29%20140802.png)

Após adicionar 2 notas:
![Primeira pagina front](/media/Captura%20de%20tela%202023-09-29%20140828.png)

Banco de dados com as notas:
![Primeira pagina front](/media/Captura%20de%20tela%202023-09-29%20140856.png)

Banco de dado após excluir uma das notas (da pra ver que o horario é depois de que a segunda nota foi criada)
![Primeira pagina front](/media//Captura%20de%20tela%202023-09-29%20140941.png)

É possivel verificar que a aplicação esta sendo acessada pelo ip publico da EC2 do frontend pelo browser.

