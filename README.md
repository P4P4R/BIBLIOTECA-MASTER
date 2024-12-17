Proposta de Arquitetura do Sistema de Biblioteca
Visão Conceitual da Arquitetura
A arquitetura do sistema é baseada em uma abordagem de três camadas:
1.	Camada de Aplicação (Interface Gráfica):

○	Responsável pela interação direta com o usuário.
○	Utiliza JavaFX para criação de telas intuitivas e responsivas.
2.	Camada de Lógica de Negócio:

○	Contém as regras de negócio para validação e processamento das operações.
○	Implementação modular para facilitar manutenção e expansão.
3.	Camada de Persistência (DAO):

○	Utiliza o padrão DAO (Data Access Object) para interagir com o banco de dados.
○	Promove o desacoplamento entre a lógica de negócio e o sistema de armazenamento.
Descrição dos Elementos da Arquitetura
Interface Gráfica
●	É composta por classes responsáveis pelas telas de cadastro, empréstimo e devolução de livros.
●	Exemplo: DevolucaoLivro, CadastroLivro, CadastroAluno.
Lógica de Negócio
●	Implementa a verificação de regras como:
○	Aluno não pode realizar empréstimo com débitos pendentes.
○	Não é permitido emprestar livros já reservados ou indisponíveis.
○	Controle de prazo de devolução.
●	Exemplo: Classes Emprestimo, Devolucao, DAOaluno, DAOlivro.
Persistência (DAO)
●	Garante que todas as interações com o banco de dados sejam realizadas de forma segura e eficiente.
●	Implementação padronizada para operações de CRUD (Create, Read, Update, Delete).
●	Exemplo: Classes DAOaluno, DAOlivro, DatabaseConnect.
Padrões Arquiteturais Adotados
MVC (Model-View-Controller):
●	Justificativa:
○	Facilita a separação de responsabilidades.
○	Promove a reutilização de código e facilita manutenção.
DAO (Data Access Object):
●	Justificativa:
○	Centraliza a lógica de acesso ao banco de dados.
○	Simplifica a migração para outros SGBDs.
Singleton:
●	Justificativa:
○	Garante uma única instância de conexão ao banco de dados durante a execução do sistema.
Factory Method:
●	Justificativa:
○	Facilita a criação de objetos DAO, promovendo flexibilidade e desacoplamento.
Discussão sobre Suporte a Outros SGBDs
Custo de Adaptação
Para suportar outro tipo de SGBD (como MySQL ou SQLite), as alterações seriam concentradas nas seguintes áreas:
1.	Driver de Conexão JDBC:

○	Substituir o driver atual pelo correspondente ao novo SGBD.
2.	Scripts SQL:

○	Ajustar scripts que utilizam sintaxes específicas do PostgreSQL, como manipulação de datas ou funções nativas.
3.	Testes de Integração:

○	Realizar testes para validar a compatibilidade com o novo SGBD.
Impacto
Devido ao uso do padrão DAO, o custo de adaptação é considerado baixo, uma vez que as interações com o banco de dados estão centralizadas em classes específicas, facilitando a manutenção e a migração.
________________________________________
Funcionalidades Adicionais
Cadastro de Livros
Descrição:
Interface para adicionar novos livros ao sistema, incluindo campos como:
●	Título.
●	Código do livro.
Tela:
●	Implementada com JavaFX, permitindo que o usuário insira os dados em um formulário.
Persistência:
●	Classe DAOlivro realiza as operações de inserção no banco de dados.
Cadastro de Alunos
Descrição:
Interface para cadastrar novos alunos, incluindo campos como:
●	Nome.
●	RA (Registro Acadêmico).
Tela:
●	Formulário desenvolvido em JavaFX.
Persistência:
●	Classe DAOaluno realiza a inserção dos dados no banco.
________________________________________
Implementação de Casos de Uso
Caso de Uso: Emprestar Livro
Atualização do Diagrama de Classes
●	Inclui a camada DAO para acesso ao banco.
●	Classes envolvidas: Emprestimo, DAOlivro, DAOaluno.
Diagrama de Sequência
Fluxo Principal:
1.	Usuário insere RA e códigos dos livros na interface.
2.	Verificação de pendências do aluno (débitos, cadastro).
3.	Atualiza o status dos livros no banco.
4.	Insere os registros de empréstimo no banco.
Implementação
●	Utiliza padrões MVC e DAO.
●	Persistência realizada em um banco PostgreSQL.
Caso de Uso: Devolver Livro
Descrição
Permite ao aluno devolver livros emprestados, atualizando o status no sistema e verificando se há débitos gerados por atraso.
Atualização do Diagrama de Classes
●	Classes envolvidas: Devolucao, DAOlivro, DAOaluno.
Diagrama de Sequência
Fluxo Principal:
1.	Usuário insere RA e código do livro na interface.
2.	Verifica se o livro está emprestado pelo aluno.
3.	Atualiza o status no banco de dados.
4.	Registra a data de devolução no banco.
Implementação
●	Utiliza padrões MVC e DAO.
●	Persistência realizada no mesmo banco PostgreSQL.
________________________________________
Conclusão
O sistema foi projetado para ser modular, escalável e de fácil manutenção, adotando padrões consolidados como MVC, DAO, Singleton e Factory Method. A arquitetura proposta garante uma separação clara entre as responsabilidades, facilitando futuras expansões e adaptações para diferentes tecnologias.
