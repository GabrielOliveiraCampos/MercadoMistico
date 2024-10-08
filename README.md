#Mercadomístico

Grupo: Gabriel Campos e Mirella Rezes
Turma: 2AM

O projeto do Mercado Místico é um site com banco de dados com funções de guardar informações de usuários, produtos, carrinhos de compras e favoritos de um mercado de poções. 
Para guardar e controlar esses dados foi utilizado o MySql como banco de dados

Esse trabalho também inclui uma API para se ligar com o Banco de dados desenvolvida em Node.js, com os seguintes pacotes:

Node.js, Express, MySQL2, Nodemon ,Dotenv, Cors e Multer

Estrutura do site:
Frontend:
Páginas HTML para diferentes partes do site
Arquivos css e javaScript para estilizar e aplicar funcionalidade das páginas 
Imagens de produtos e design da página 
Backend:
Pasta backend contendo a lógica do servidor
Conexão com um banco de dados SQL arquivo:Bancodedados.sql

Banco de Dados: Mercadomístico/Bancodedados.sql
Servidor: Mercadomístico/src/server.js 

Para a instalação:

Conecte-se ao servidor MySQL.
Crie o banco de dados com o comando: Create Database mercadomistico;
Selecione o banco de dados: USE mercadomistico;

Em seu terminal use o comando cd e entre nas pastas: exemplo: cd Mercadomístico
Instale os pacotes com : npm install
Após isso: npm start
Assim pode seguir com os passos do Banco de dados que está relacionado com todo o resto do site:

Estrutura do Banco de Dados:
Tabela Usuarios:
CREATE TABLE Usuarios (
    Idusuario INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    cpf_number BIGINT,
    status ENUM('Ativo', 'Inativo') DEFAULT 'Ativo'
);

INSERT INTO Usuarios (name, email, password, cpf_number, status)
VALUES 
    ('Gabriell', 'gabriell@gmail.com', 'senha1', '88878888', 'Ativo'),
    ('Lucas', 'lucas@gmail.com', 'senha2', '99987766', 'Ativo'),
    ('Ana', 'ana@gmail.com', 'senha3', '55566677', 'Inativo');

Select * from Usuarios: (para selecionar todos os usuarios)

Rotas:
Cadastrar Usuário
Método: POST
Rota: http://localhost:3000/usuario/cadastrar
Body:{
  "name": "Nome do Usuário",
  "email": "usuario@gmail.com",
  "password": "senhaSegura",
  "cpf_number": "12345678901",
  "tipo_usuario": "usuario"
}

Listar Usuários
Método: GET
Rota: http://localhost:3000/usuarios/listar

Editar Usuário
Método: PUT
Rota: http://localhost:3000/usuario/editar/:id

Deletar Usuário
Método: DELETE
Rota: http://localhost:3000/usuario/deletar/:id

Tabela Produtos
CREATE TABLE produtos (
    Produtoid INT AUTO_INCREMENT PRIMARY KEY,
    Tituloproduto VARCHAR(255) NOT NULL,
    valor DOUBLE NOT NULL,
    image TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

Adicionar Produto
Método: POST
Rota: http://localhost:3000/produto/cadastrar

Listar Produtos
Método: GET
Rota: http://localhost:3000/produtos/listar

Editar Produto
Método: PUT
Rota: http://localhost:3000/produto/editar/:id

Deletar Produto
Método: DELETE
Rota: http://localhost:3000/produto/deletar/:id

CREATE TABLE Carrinho (
    id_carrinho INT PRIMARY KEY AUTO_INCREMENT NOT NULL,
    UsuarioId INT NOT NULL,
    ProdutoId INT NOT NULL,
    
    FOREIGN KEY (ProdutoId) REFERENCES produtos(Produtoid),
    FOREIGN KEY (UsuarioId) REFERENCES usuarios(Idusuario)
);

Adicionar Produto ao Carrinho
Método: POST
Rota: http://localhost:3000/carrinho/adicionar
Body:{
  "UsuarioId": 1,
  "ProdutoId": 2
}

 Listar Itens do Carrinho por Usuário
 Método: GET
Rota: http://localhost:3000/carrinho/listar/:UsuarioId

Editar Quantidade de um Produto no Carrinho
Método: PUT
Rota: http://localhost:3000/carrinho/editar/:id_carrinho

Remover Produto do Carrinho
Método: DELETE
Rota: http://localhost:3000/carrinho/remover/:id_carrinho

Tabela Favoritos

CREATE TABLE Favoritos (
    IdFavorito INT AUTO_INCREMENT PRIMARY KEY,
    UsuarioId INT NOT NULL,
    ProdutoId INT NOT NULL,
    FOREIGN KEY (UsuarioId) REFERENCES usuarios(Idusuario),
    FOREIGN KEY (ProdutoId) REFERENCES produtos(Produtoid)
);

Adicionar Produto aos Favoritos
Método: POST
Rota: http://localhost:3000/favoritos/adicionar
Body:{
  "UsuarioId": 1,
  "ProdutoId": 2
}

 Listar produtos favoritos
 Método: GET
Rota: http://localhost:3000/favoritos/listar/:UsuarioId

Remover Produto de favoritos

Método: DELETE
Rota: http://localhost:3000/favoritos/remover/:IdFavorito

Aqui estão todas as rotas testadas que estão funcionando para o desenvolvimento do código.
