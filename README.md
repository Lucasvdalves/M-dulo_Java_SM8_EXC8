# M-dulo_Java_SM8_EXC8 

 # Exercicio módulo Java semana 8


 1 -- Implemente ao final uma consulta a todos os veículos cadastrados com as respectivas multas, e imprima estes registros no console (usar toString()).

 2 -- Este projeto consiste em um sistema simples de registro de ponto de um funcionário, onde você deverá ser capaz de registrar um funcionário, listar os funcionários cadastrados, recuperar detalhes de um único funcionário e também registrar o ponto do funcionário, informando se é um registro de entrada ou saída.
Essa atividade consiste na criação do projeto, envolvendo a sua estrutura e dependências. Para criá-lo, siga para o site do Spring Initializr: https://start.spring.io/

Este projeto requer as seguintes dependências:

Spring Web
Spring Boot DevTools
PostgreSQL Driver
Spring Data JPA
Validation

Crie o projeto e o importe em sua IDE (IntelliJ, Eclipse, dentre outros).

3 -- Essa atividade consiste na criação do seu banco de dados, que pode ter o nome de sua escolha. Para criar o banco de dados pelo terminal do PSQL:
CREATE DATABASE meu_banco;
O segundo ponto aqui é configurar a conexão com este banco de dados em sua aplicação Spring. Para isso, você deve ir no arquivo application.properties ou application.yml, caso você tenha trocado a extensão, e configurar as propriedades que vimos em aula.
Obs: Não precisamos decorar as configurações de conexão com o banco de dados! Portanto, sinta-se à vontade para consultar as informações no Github das nossas aulas.


3 -- Essa atividade consiste na criação das entidades, ou seja, as classes que irão representar as tabelas do seu banco de dados.
Teremos duas entidades: Funcionário e Registro de Ponto.

O funcionário possui id, nome, cargo e salário, e o registro é composto por id, identificador do funcionário, hora do registro e tipo do registro, que pode ser entrada ou saída (enum).
Lembre-se de mapear (anotações) corretamente os atributos e a entidade, para que ela possa ser gerenciada.
Uma dica aqui para o relacionamento entre as entidades é usar um mapeamento bidirecional, que consiste no funcionário ter uma lista de registros, e um registro ter um funcionário:

// Classe Funcionário
@OneToMany(mappedBy = "employee", orphanRemoval = true, cascade = {CascadeType.MERGE, CascadeType.PERSIST, CascadeType.REFRESH})
private List<Register> registers;

// Classe Registro

@ManyToOne
@JoinColumn(name = "employee_id", nullable = false, referencedColumnName = "id")
private Employee employee;



4 -- Essa atividade consiste na criação dos repositórios, ou seja, das interfaces que estendem JpaRepositorye fornecem métodos para que possamos realizar operações e leituras no banco de dados facilmente.
Você deve criar os repositórios para funcionário e para os registros.


5 -- Essa atividade consiste na implementação do cadastro do funcionário. Segue um passo a passo para te guiar:
Crie um DTO que representa a criação do funcionário. Ele deve conter seu nome, cargo e salário. Lembre-se de usar as anotações de validação dos atributos, que são todos obrigatórios.
A camada de serviço de funcionários deve ser criada, ela deve conter o método que recebe o DTO anterior, converte em um objeto de persistência e chama uma instância do repositório para salvar o funcionário.
O controlador deve conter um método POST que será o endpoint para o cadastro do funcionário.


6 -- Essa atividade consiste na listagem dos funcionários, que deve vir de forma paginada, contendo 12 itens por página.
Você deve criar um DTO para retornar esses objetos, não retornando diretamente a classe de persistência dos funcionários. Além disso, por ser uma listagem geral, você não deve retornar os registros de ponto dos funcionários, apenas suas informações básicas.


7 -- Essa atividade consiste na busca por um funcionário, que deve ser feita através de seu identificador.
Essa busca se trata de um detalhamento de determinado funcionário, então seus registros de ponto devem retornar junto, caso existam.
Para isso, você deve criar o DTO que represente um registro de ponto, e assim retornar essa lista dentro do DTO do funcionário.


8 -- Essa atividade consiste na documentação e adição de logs na aplicação.
Para a documentação, basta você configurar corretamente a dependência do OpenAPI com Swagger em seu pom.xml.
Para os logs, você deve utilizar o Log4j, e adicionar logs nos pontos que acredita serem importantes dentro da aplicação.

