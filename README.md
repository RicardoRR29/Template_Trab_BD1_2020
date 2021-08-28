# TRABALHO 01:  JG Mercados
Trabalho desenvolvido durante a disciplina de BD1

# Sumário

### 1. COMPONENTES<br>
Integrante do grupo<br>
Ricardo Rocha Ribeiro: r3ifes@gmail.com
<br>

### 2.INTRODUÇÃO E MOTIVAÇÃO<br>

> Um mercadinho popular tem aumentado sua demanda consideravelmente e o dono percebeu a necessidade de ter um controle maior do que está entrando e saindo e para poder analisar melhor o próprio negócio. Para isso, ele quer um programa de controle simples para conseguir armazenar algumas informações

 
### 3.MINI-MUNDO<br>

> O sistema proposto para o JG Mercados conterá as informacões aqui detalhadas. Sobre os clientes serão armazenados um código de identificação, nome, email, endereço. Sobre o endereço serão armazenadas as informações referentes as ruas, cidades, CEPs e código do clientes. Os clientes poderão ou não ter pedidos, e este será composto por um código, data, código do cliente, e valor. Haverá também uma lista de produtos, em que os produtos possuirão um código, nome do produto, preço, quantidade, descricao e código de categoria. Os pedidos estarão ligados a produtos, com a informação da quantidade, valor total, código do produto e código do pedido. Sobre as categorias serão armazenados um código específico para cada categoria e um nome.

### 4.PROTOTIPAÇÃO, PERGUNTAS A SEREM RESPONDIDAS E TABELA DE DADOS<br>
#### 4.1 RASCUNHOS BÁSICOS DA INTERFACE (MOCKUPS)<br>

Link para baixar o pdf interativo:

![Arquivo PDF do Protótipo Balsamiq feito para JG Mercados](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/arquivos/JGMercados.pdf?raw=true "JG Mercados")
#### 4.2 QUAIS PERGUNTAS PODEM SER RESPONDIDAS COM O SISTEMA PROPOSTO?
    
a) O sistema proposto pode ajudar a entender o que está acontecendo na empresa, quem são os clientes, o que é mais vendido, qual produto é mais vendido entre os clientes que moram perto/longe. Qual categoria os clientes de determinada região compram mais. Estas informações podem se tornar chaves para uma boa decisão de negócio.
<br>
b) Relatórios:
> 1) Relatório que mostre o a localização dos clientes. Caso queiram fazer alguma propaganda digital ou até mesmo física, sabem qual área escolher para a exibição da propaganda.
> 2) Relatório que mostre os horários de pico do mercado.
> 3) Relatório para saber qual produto/categoria está sendo mais/menos vendido(a). 
> 4)
> 5)
 
 
#### 4.3 TABELA DE DADOS DO SISTEMA:
    
![Exemplo de Tabela de dados da Empresa Devcom](https://github.com/discipbd1/trab01/blob/master/arquivos/TabelaJGMercados.xlsx?raw=true "Tabela - Empresa Devcom")
    
    
### 5.MODELO CONCEITUAL<br>
Modelo conceitual feito a partir das informações retiradas do minimundo.
        
![Modelo conceitual](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/modelo-conceitual.PNG?raw=true "Modelo Conceitual")
    
    
        
    
#### 5.1 Validação do Modelo Conceitual
    [Grupo01]: Gustavo Gomes
    [Grupo02]: George Matheus Santos

#### 5.2 Descrição dos dados 
    
    CLIENTE: tabela com os principais dados do cliente
    ENDERECO: tabela com o endereço de cada cliente
    PEDIDO_PRODUTO: tabela que cria a relação entre os produtos e os pedidos, possuindo uma referência de cada um deles.
    PRODUTO: tabela com os principais dados dos produtos
    CATEGORIA: tabela com a lista de categorias
    Na tabela CLIENTE:
        id: identificação única do cliente
        nome: nome do cliente
        email: email do cliente
    Na tabela ENDERECO:
        id: identificação única do endereço
        rua: rua em que o cliente mora
        cidade: cidade que o cliente mora
        bairro: bairro o cliente mora
        cep: identificação do endereço do cliente
        id_cliente: identificação do código da tabela cliente
    Na tabela PEDIDO:
        id: identificação única do pedido
        data: data em que houve o pedido
        valor: valor total do pedido
        id_cliente: identificação de qual cliente fez o pedido
    Na tabela PRODUTO:
        id: identificação única do produto
        produto: nome do produto
        preco: valor de venda do produto
        quantidade: quantidade do produto em questão no estoque
        descricao: descrição/comentário do produto
    Na tabela CATEGORIA:  
        id: identificação única da categoria
        categoria: nome da categoria
        id_produto: identificação do produto relacionada a categoria
    Na tabela PEDIDO_PRODUTO:  
        id: identificação única da relação entre um dos pedidos e um dos produtos
        id_pedido: identificação do pedido
        id_produto: identificação do produto
        quantidade: quantidade vendida do produto no pedido em questão
### 6	MODELO LÓGICO<br>

![Modelo Lógico](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/modelo-logico.PNG?raw=true "Modelo Lógico")


### 7	MODELO FÍSICO<br>

```
drop table if exists CLIENTE cascade;
drop table if exists ENDERECO cascade;
drop table if exists PRODUTO cascade;
drop table if exists PEDIDO cascade;
drop table if exists PEDIDO_PRODUTO cascade;
drop table if exists CATEGORIA cascade;


create table CLIENTE(
    id serial PRIMARY KEY,
    nome varchar(255),
    email varchar(255)
);

create table ENDERECO(
    id serial PRIMARY KEY,
    rua varchar(255),
    cidade varchar(255),
    bairro varchar(255),
    cep varchar(20),
    id_cliente int,
    FOREIGN KEY(id_cliente) REFERENCES CLIENTE(id)
);

create table PEDIDO(
    id serial PRIMARY KEY,
    data date,
    valor real,
    id_cliente int,
    FOREIGN KEY(id_cliente) REFERENCES CLIENTE(id)
);

create table CATEGORIA(
    id serial PRIMARY KEY,
    categoria varchar(50)
);

create table PRODUTO(
    id serial PRIMARY KEY,
    produto varchar(255),
    preco real,
    quantidade int,
    descricao varchar(255),
    id_categoria int,
    FOREIGN KEY(id_categoria) REFERENCES CATEGORIA(id)
);

create table PEDIDO_PRODUTO(
    id serial PRIMARY KEY,
    id_pedido int,
    id_produto int,
    quantidade int,
    FOREIGN KEY(id_pedido) REFERENCES PEDIDO(id),
    FOREIGN KEY(id_produto) REFERENCES PRODUTO(id)
);
```


### 8	INSERT APLICADO NAS TABELAS DO BANCO DE DADOS<br>

### Tabela CLIENTE

```
INSERT INTO "cliente" (nome,email) VALUES 
('Jermaine','amet.dapibus@lacus.com'),
('Oprah','non@augueeutempor.edu'),('Claudia','enim@mollis.edu'),
('Levi','nunc.sed@libero.com'),
('Dominique','leo.in.lobortis@Aliquam.org'),
('Vladimir','iaculis@etultricesposuere.org'),
('Holmes','sit@Nam.org'),
('Hannah','Mauris.molestie@volutpatNulla.co.uk'),
('Alexa','Donec@tempus.ca'),
('Kiara','metus.In@nonenim.edu');
INSERT INTO "cliente" (nome,email) VALUES 
('Samuel','ut.pharetra@vulputatelacus.edu'),
('Randall','ipsum@temporerat.net'),
('Lillian','Donec@accumsansed.org'),
('Elaine','nisl.Quisque@Nunc.org'),
('Stephanie','venenatis.a@aliquet.net'),
('Camille','dapibus.quam@etcommodoat.com'),
('Jason','dolor@pede.org'),
('Diana','egestas.Aliquam@risus.com'),
('Lydia','ut@et.net'),
('Thor','pretium@Aliquam.ca'),
('Chloe','non@semperet.co.uk');

```

### Tabela PEDIDO

``` 
INSERT INTO "pedido" (id_cliente,data, valor) VALUES 
(17,'2014-10-07',33.35),
(20,'2012-02-21',60.00),
(3,'2010-09-05',20.00),
(18,'2020-03-14',19.90),
(17,'2019-08-21',20.90),
(3,'2020-12-21',10.00),
(17,'2021-04-30',20.10),
(2,'2021-02-05',30.00),
(11,'2021-05-13',10.50),
(19,'2021-01-06',500.00),
(14,'2013-06-03',10.00),
(1,'2018-12-04',5.00),
(8,'2020-03-30',3.00),
(14,'2020-10-10',33.35),
(13,'2020-12-14',60.00),
(10,'2021-11-05',20.00),
(16,'2021-10-05',19.90),
(21,'2021-05-19',20.90),
(2,'2021-01-07',10.00),
(19,'2013-06-03',20.10),
(3,'2018-12-04',30.00),
(1,'2020-03-30',10.50),
(20,'2020-10-10',500.00),
(13,'2020-12-14',10.00),
(8,'2021-11-05',5.00),
(2,'2021-10-05',3.00),
(10,'2021-05-19',33.35),
(17,'2021-01-07',60.00),
(16,'2013-06-03',20.00),
(3,'2018-12-04',19.90),
(5,'2020-03-30',20.90),
(5,'2020-10-10',10.00),
(5,'2020-12-14',20.10),
(21,'2021-11-05',30.00),
(13,'2021-10-05',10.50),
(15,'2021-05-19',500.00),
(11,'2021-01-07',10.00),
(13,'2020-12-14',5.00),
(12,'2021-11-05',3.00),
(6,'2021-10-05',2.00),
(15,'2021-05-19',1.50);
```
### Tabela ENDERECO
```
INSERT INTO "endereco" (rua,cidade,bairro,cep, id_cliente) VALUES 
('Rua Conselheiro Antônio Prado','Jacareí','Parque Itamarati','12307-410',1),
('Rua Quatorze','Belo Horizonte','Diamante (Barreiro)','30660-720',2),
('Rua Pedro Celestino 1550','Campo Grande','Centro','79002-925',3),
('Quadra 305 Sul Alameda 2','Palmas','Plano Diretor Sul','77015-436',4),
('Rua Vaticano','Porto Velho','Igarapé','76824-238',5),
('Rua Carmelita Ireng','Boa Vista','Senador Hélio Campos','69316-600',6),
('Rua Nossa Senhora da Conceição','São Luís','Coroadinho','65042-590',7),
('Rua Osvaldo Cruz','Cuiabá','Pico do Amor','78065-125',8),
('Travessa','LinhoManaus','Tarumã','69041-191',9),
('Rua Plínio Schmidt','Lages','Sagrado Coração de Jesus','88508-526',10),
('Rua Existente','Aracaju','Zona de Expansão (Aruana)','49000-861',11),
('Rua Vigário Freire 10','Caruaru','Nossa Senhora das Dores','55002-907',12),
('Quadra Quadra 107 Conjunto 8','Brasília','Recanto das Emas','72601-309',13),
('Alameda Lugar Bonito','Macapá','Boné Azul','68909-607',14),
('Rua Professor Rodrigo Costa','Manaus','Cidade Nova','69096-630',15),
('Rua Marfim','Rio Branco','Wanderley Dantas','69902-885',16),
('Rua Centaurias','Aparecida de Goiânia','Expansul','74986-240',17),
('Rua Lineo Arantes de Mello','Presidente Prudente','Conjunto Habitacional Ana Jacinta','19064-415',18),
('Rua Padre Cícero','São Luís','São Bernardo','65053-490',19),
('Adonis Costa','Cachoeiro de Itapemirim','Jardim América','29310-845',20),
('Rua Anita Garibaldi','Francisco Beltrão','Centro','85601-280',21);
```
### Tabela CATEGORIA
```
INSERT INTO "categoria" (categoria) VALUES
('Vegetais'),
('Brinquedos'),
('Eletrônicos'),
('Carnes'),
('Frios'),
('Filmes'),
('Cereais'),
('Higiene'),
('Marcenaria'),
('Biscoitos'),
('Outros'),
('Processados'); 
```
### Tabela PRODUTO
```
INSERT INTO "produto" (produto,preco,quantidade,descricao,id_categoria) VALUES
('tomate',1,200,'vegetal fresco',1),
('alface',2,300,'vegetal fresco',1),
('feijão',3,1000,'Vindo da fazenda',7),
('ps4',2000,30,'Ainda terá muito tempo',3),
('ps3',700,35,'Bem velho mas ótimo',3),
('Moto G8 Power',1200,75,'Ótimo celular',3),
('ps2',150,55,'Melhor custo beneficio para crianças',3),
('ps1',100,65,'Raridade',3),
('Maminha 300gr',10,100,'Ótima pra churrasco',4),
('ps5',5000,20,'O mais novo',3),
('arroz',5,300,'O de sempre',7),
('sabonete',0.5,320,'Para todo banho',8),
('porta',900,10,'Resistente e com um toque fino',9),
('Presunto',5,30,'Pro misto de cada dia',12),
('Queijo',6,40,'Completa o misto',5),
('Pizza congelada',20,10,'Sempre bom ter no congelador',5),
('Fósforo',3,30,'Nunca deixe fazer falta',11),
('Biscoito Fit',3.5,20,'Não tão fit',10),
('Costela',10,23,'Ótima pra churrasco',4),
('Max Steel',14,7,'Faz parte da infância',2),
('Barbie',13,6,'Faz parte da infância',2),
('Power Ranger',1,8,'Faz parte da infância',2),
('Ben 10',12,4,'Faz parte da infância',2),
('Dragon Ball DVD',10,3,'Faz parte da infância',6);
```
### Tabela PEDIDO_PRODUTO
```
INSERT INTO "pedido_produto" (id_produto,id_pedido,quantidade) VALUES 
(7,1,1),
(3,2,3),
(5,3,2),
(8,4,4),
(5,5,6),
(9,6,2),
(1,7,3),
(4,8,4),
(7,9,1),
(9,10,2),
(3,11,12),
(5,12,11),
(7,13,1),
(2,14,1),
(5,15,2),
(7,16,1),
(8,17,2),
(9,18,1),
(2,19,1),
(3,20,1),
(5,21,1),
(7,22,2),
(8,23,1),
(6,24,2),
(4,25,1),
(2,26,1),
(3,27,1),
(5,28,1),
(6,29,2),
(1,30,1),
(2,31,2),
(4,32,1),
(5,33,1),
(7,34,1),
(8,35,1),
(3,36,2),
(2,37,1),
(24,27,2),
(23,28,1),
(21,29,1),
(23,30,1),
(2,31,1),
(22,32,2),
(19,33,1),
(17,34,2),
(12,35,1),
(14,36,1),
(15,37,1),
(11,34,1),
(12,35,2),
(15,36,1),
(16,37,2),
(16,36,1),
(18,37,1),
(19,34,3);
``` 


### 9	TABELAS E PRINCIPAIS CONSULTAS<br>

#### 9.1	CONSULTAS DAS TABELAS COM TODOS OS DADOS INSERIDOS (Todas) <br>
```
select * from CLIENTE;
```
![Tabela cliente](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectCliente.PNG?raw=true "Tabela cliente")
```
select * from ENDERECO;
```
![Tabela endereço](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectEndereco.PNG?raw=true "Tabela endereço")
```
select * from PEDIDO;
```
![Tabela pedido](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectPedido1.PNG?raw=true "Tabela pedido")
![Tabela pedido](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectPedido2.PNG?raw=true "Tabela pedido")
```
select * from PRODUTO;
```
![Tabela produto](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectProduto.PNG?raw=true "Tabela produto")
```
select * from PEDIDO_PRODUTO;
```
![Tabela pedido_produto](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectPedidoProduto1.PNG?raw=true "Tabela pedido_produto")
![Tabela pedido_produto](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectPedidoProduto2.PNG?raw=true "Tabela pedido_produto")
![Tabela pedido_produto](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectPedidoProduto3.PNG?raw=true "Tabela pedido_produto")
```
select * from CATEGORIA;
```
![Tabela categoria](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectCategoria.PNG?raw=true "Tabela categoria")

#### 9.2	CONSULTAS DAS TABELAS COM FILTROS WHERE<br>
```
select id_pedido,id_produto from PEDIDO_PRODUTO WHERE quantidade = 2;
```
![Consulta com filtro where](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectPedidoProdutoWithWhereQuantidade2.PNG?raw=true "Consulta com filtro where")
```
select * from PRODUTO WHERE quantidade > 199;
```
![Consulta com filtro where](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectProdutoWithWhereQuatidade.PNG?raw=true "Consulta com filtro where")
```
select * from PRODUTO WHERE preco > 20;
```
![Consulta com filtro where](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectProdutoWithWherePreco.PNG?raw=true "Consulta com filtro where")
```
select * from PEDIDO WHERE data > '2021-10-14';
```
![Consulta com filtro where](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectPedidoWithWhereData.PNG?raw=true "Consulta com filtro where")
```
select * from pedido where id_cliente = 13;
```
![Consulta com filtro where](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectPedidoWithWhereId.PNG?raw=true "Consulta com filtro where")

#### 9.3	CONSULTAS QUE USAM OPERADORES LÓGICOS, ARITMÉTICOS E TABELAS OU CAMPOS RENOMEADOS (Mínimo 11)
### Consultas que envolvam os operadores lógicos AND, OR e Not
```
select * from PEDIDO WHERE data > '2019-10-14' AND valor > 10;
```
![Consulta com operador lógico](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/operador(9.3)-1.PNG?raw=true "Consulta com operador lógico")
```
select * from PEDIDO WHERE data > '2019-10-14' OR valor > 10;
```
![Consulta com operador lógico](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/operador(9.3)-2.PNG?raw=true "Consulta com operador lógico")
![Consulta com operador lógico](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/operador(9.3)-2(2).PNG?raw=true "Consulta com operador lógico")
```
select * from PEDIDO WHERE data > '2019-10-14' AND NOT valor > 10;
```
![Consulta com operador lógico](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/operador(9.3)-3.PNG?raw=true "Consulta com operador lógico")
```
select * from PRODUTO WHERE quantidade > 10 AND preco > 1000;
```
![Consulta com operador lógico](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/operador(9.3)-4.PNG?raw=true "Consulta com operador lógico")
```
select * from PRODUTO WHERE id_categoria = 3 OR preco < 1;
```
![Consulta com operador lógico](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/operador(9.3)-5.PNG?raw=true "Consulta com operador lógico")
### Consultas com operadores aritméticos
```
(select * from PEDIDO where id_cliente < 5)
UNION
(select * from PEDIDO where id_cliente > 15)
```
![Consulta com operador aritmético](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/OperadorArit-1.PNG?raw=true "Consulta com operador aritmético")
```
(select * from PEDIDO where id_cliente = 3)
INTERSECT
(select * from PEDIDO where valor > 20)
```
![Consulta com operador aritmético](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/OperadorArit-2.PNG?raw=true "Consulta com operador aritmético")
```
(select * from PEDIDO where id_cliente = 3)
EXCEPT
(select * from PEDIDO where valor > 20)
```
![Consulta com operador aritmético](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/OperadorArit-3.PNG?raw=true "Consulta com operador aritmético")
### Consultas com operação de renomear nomes de campos ou tabelas
```
select id as codigo, data, valor as preco, id_cliente as cod_cliente from pedido;
```
![Consulta com operação de renomear](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectPedidoProdutoWithWhere.PNG?raw=true "Consulta com operação de renomear")
```
select * from pedido as p;
```
![Consulta com operação de renomear](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectPedidoProdutoWithWhere.PNG?raw=true "Consulta com operação de renomear")
```
select id, categoria as nome_categoria  from categoria;
```
![Consulta com operação de renomear](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectPedidoProdutoWithWhere.PNG?raw=true "Consulta com operação de renomear")
#### 9.4	CONSULTAS QUE USAM OPERADORES LIKE E DATAS (Mínimo 12) <br>

### Consultas que envolvam like ou ilike
```
select * from cliente where nome like '%an%';
```
![Consulta com like ou ilike](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectPedidoProdutoWithWhere.PNG?raw=true "Consulta com like ou ilike")
```
select * from cliente where nome like '%Ra%';
```
![Consulta com like ou ilike](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectPedidoProdutoWithWhere.PNG?raw=true "Consulta com like ou ilike")
```
select * from cliente where nome ilike '%Ra%';
```
![Consulta com like ou ilike](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectPedidoProdutoWithWhere.PNG?raw=true "Consulta com like ou ilike")
```
select * from cliente where nome like 'ha%';
```
![Consulta com like ou ilike](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectPedidoProdutoWithWhere.PNG?raw=true "Consulta com like ou ilike")
```
select * from cliente where nome ilike 'ha%';
```
![Consulta com like ou ilike](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectPedidoProdutoWithWhere.PNG?raw=true "Consulta com like ou ilike")
```
select * from cliente where nome like '%A';
```
![Consulta com like ou ilike](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectPedidoProdutoWithWhere.PNG?raw=true "Consulta com like ou ilike")
```
select * from cliente where nome ilike '%A';
```
![Consulta com like ou ilike](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectPedidoProdutoWithWhere.PNG?raw=true "Consulta com like ou ilike")
### Consulta para cada tipo de função data apresentada.
```
select id,data,date_part('month',(age(current_date,data))) as mes_diferenca from pedido where date_part('month',(age(current_date,data))) > 5;
```
![Consulta com uso de funções date](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectPedidoProdutoWithWhere.PNG?raw=true "Consulta com uso de funções date")
```
select id,data,extract(month from data) as mes,extract(day from data) as dia from pedido where extract(day from data) > 15;
```
![Consulta com uso de funções date](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectPedidoProdutoWithWhere.PNG?raw=true "Consulta com uso de funções date")
```
select id,data,date_part('year',(age(current_date,data))) from pedido where date_part('year',(age(current_date,data))) > 1;
```
![Consulta com uso de funções date](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectPedidoProdutoWithWhere.PNG?raw=true "Consulta com uso de funções date")
```
select id,data,extract(month from data) as mes,extract(day from data) as dia from pedido where extract(month from data) < 6;
```
![Consulta com uso de funções date](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectPedidoProdutoWithWhere.PNG?raw=true "Consulta com uso de funções date")
```
select id,data,extract(day from data) as dia,extract(month from data) as mes,extract(year from data) as ano from pedido where extract(year from data) < 2018;
```
![Consulta com uso de funções date](https://github.com/RicardoRR29/Template_Trab_BD1_2020/blob/master/images/selectPedidoProdutoWithWhere.PNG?raw=true "Consulta com uso de funções date")

#### 9.5	INSTRUÇÕES APLICANDO ATUALIZAÇÃO E EXCLUSÃO DE DADOS (Mínimo 6)<br>
    a) Criar minimo 3 de exclusão
    b) Criar minimo 3 de atualização

#### 9.6	CONSULTAS COM INNER JOIN E ORDER BY (Mínimo 6)<br>
    a) Uma junção que envolva todas as tabelas possuindo no mínimo 2 registros no resultado
    b) Outras junções que o grupo considere como sendo as de principal importância para o trabalho

#### 9.7	CONSULTAS COM GROUP BY E FUNÇÕES DE AGRUPAMENTO (Mínimo 6)<br>
    a) Criar minimo 2 envolvendo algum tipo de junção

#### 9.8	CONSULTAS COM LEFT, RIGHT E FULL JOIN (Mínimo 4)<br>
    a) Criar minimo 1 de cada tipo

#### 9.9	CONSULTAS COM SELF JOIN E VIEW (Mínimo 6)<br>
        a) Uma junção que envolva Self Join (caso não ocorra na base justificar e substituir por uma view)
        b) Outras junções com views que o grupo considere como sendo de relevante importância para o trabalho

#### 9.10	SUBCONSULTAS (Mínimo 4)<br>
     a) Criar minimo 1 envolvendo GROUP BY
     b) Criar minimo 1 envolvendo algum tipo de junção

># Marco de Entrega 02: Do item 9.2 até o ítem 9.10<br>

### 10 RELATÓRIOS E GRÁFICOS

#### a) análises e resultados provenientes do banco de dados desenvolvido (usar modelo disponível)
#### b) link com exemplo de relatórios será disponiblizado pelo professor no AVA
#### OBS: Esta é uma atividade de grande relevância no contexto do trabalho. Mantenha o foco nos 5 principais relatórios/resultados visando obter o melhor resultado possível.

    

### 11	AJUSTES DA DOCUMENTAÇÃO, CRIAÇÃO DOS SLIDES E VÍDEO PARA APRESENTAÇAO FINAL <br>

#### a) Modelo (pecha kucha)<br>
#### b) Tempo de apresentação 6:40 

># Marco de Entrega 03: Itens 10 e 11<br>
<br>
<br>
<br> 



### 12 FORMATACAO NO GIT:<br> 
https://help.github.com/articles/basic-writing-and-formatting-syntax/
<comentario no git>
    
##### About Formatting
    https://help.github.com/articles/about-writing-and-formatting-on-github/
    
##### Basic Formatting in Git
    
    https://help.github.com/articles/basic-writing-and-formatting-syntax/#referencing-issues-and-pull-requests
    
    
##### Working with advanced formatting
    https://help.github.com/articles/working-with-advanced-formatting/
#### Mastering Markdown
    https://guides.github.com/features/mastering-markdown/

    
### OBSERVAÇÕES IMPORTANTES

#### Todos os arquivos que fazem parte do projeto (Imagens, pdfs, arquivos fonte, etc..), devem estar presentes no GIT. Os arquivos do projeto vigente não devem ser armazenados em quaisquer outras plataformas.
1. <strong>Caso existam arquivos com conteúdos sigilosos<strong>, comunicar o professor que definirá em conjunto com o grupo a melhor forma de armazenamento do arquivo.

#### Todos os grupos deverão fazer Fork deste repositório e dar permissões administrativas ao usuário do git "profmoisesomena", para acompanhamento do trabalho.

#### Os usuários criados no GIT devem possuir o nome de identificação do aluno (não serão aceitos nomes como Eu123, meuprojeto, pro456, etc). Em caso de dúvida comunicar o professor.


Link para BrModelo:<br>
http://www.sis4.com/brModelo/download.html
<br>


Link para curso de GIT<br>
![https://www.youtube.com/curso_git](https://www.youtube.com/playlist?list=PLo7sFyCeiGUdIyEmHdfbuD2eR4XPDqnN2?raw=true "Title")


