# DataBaseView

Este código SQL cria um banco de dados para gerenciar informações sobre produtos, marcas e fornecedores. Ele inclui a criação de uma tabela principal, inserção de dados nessa tabela, criação de visualizações e execução de consultas para análise de dados.

## Operações Realizadas

1. **Criação da Tabela**: Uma tabela chamada `tabela` é criada para armazenar informações sobre os produtos, como nome, marca, fornecedor, estoque, data de validade e preço.

2. **Inserção de Dados**: Diversos produtos são inseridos na tabela `tabela`, com informações sobre nome, marca, fornecedor, estoque, data de validade e preço.

3. **Criação de Visualizações**: São criadas quatro visualizações:
   - `marcasv`: Mostra o nome e a marca de cada produto.
   - `nomefornecedor`: Mostra o nome do produto e seu fornecedor.
   - `fornecedormarca`: Mostra o fornecedor e a marca de cada produto.
   - `insuficiente`: Mostra produtos com estoque abaixo do mínimo.

4. **Atualização da Tabela**: É adicionada uma nova coluna chamada `data_val` à tabela `tabela`, para armazenar a data de validade dos produtos.

5. **Inserção de Novos Dados**: Mais produtos são inseridos na tabela `tabela`, incluindo informações sobre data de validade.

6. **Consulta de Dados**: Duas consultas são realizadas:
   - Calcula a média de preços dos produtos.
   - Lista os nomes dos produtos com preço superior a 14.
  
   --------------------------------------------------------------------------------------------------------------------------------------------
   view

({ CREATE TABLE tabela(
	id			integer PRIMARY KEY autoincrement,
	nome		varchar,
	marca		varchar,
	fornecedor	varchar,
	estoque_min	int DEFAULT 100 ,
	estoque		int,
	data_atual	date DEFAULT current_date,
	preco		double
)

DROP TABLE tabela;

INSERT INTO tabela (nome,marca,fornecedor,estoque,preco) VALUES
('maionese','helmans', 'helmans ltda', 102,10),
('bolacha','oreo', 'oreo ltda', 50, 12),
('nescau','nestle', 'nestle ltda', 150, 11),
('danoninho','danone', 'danone ltda', 120, 22),
('salgadinho','lays', 'lays ltda', 90, 13),
('salgadinho','pringles', 'pringles ltda', 110, 23),
('macarrão','barilla', 'barilla ltda', 80,9),
('maionese','heinz', 'heinz ltda', 140, 8),
('sucrilhos','kelloggs', 'kelloggs ltda', 95,12),
('refrigerante','pepsi', 'pepsi ltda', 180, 20);

CREATE VIEW marcasv as
SELECT nome, marca FROM tabela;

CREATE VIEW nomefornecedor as
SELECT nome,fornecedor FROM tabela;

CREATE VIEW fornecedormarca as
SELECT fornecedor, marca FROM tabela;

CREATE VIEW insuficiente as
SELECT * FROM tabela WHERE estoque > estoque_min;

ALTER TABLE tabela ADD data_val	date;
INSERT INTO tabela (nome,marca, fornecedor, estoque, data_val,preco) VALUES
('chocolate','snickers', 'snickers ltda', 80, '2024-01-25', 4),
('batata','pringles', 'pringles ltda', 95, '2024-02-05', 8),
('nescau','nestea', 'nestea ltda', 120, '2024-03-15', 12),
('batata','lays', 'lays ltda', 60, '2024-04-10', 20),
('chocolate','kitkat', 'kitkat ltda', 110, '2024-05-20', 4),
('refrigerante','coca-cola', 'coca-cola ltda', 180, '2024-06-30', 4),
('suco','tang', 'tang ltda', 130, '2024-07-25', 1),
('salgadinho','doritos', 'doritos ltda', 85, '2024-08-15', 10),
('macarrão', 'barilla', 'barilla ltda', 105, '2024-09-05', 9),
('bolacha','oreo', 'oreo ltda', 160, '2024-10-10',2);

CREATE VIEW vencidos as
SELECT * FROM tabela WHERE data_val < data_atual;


SELECT avg(preco) AS media_preco FROM tabela;
SELECT nome FROM tabela WHERE preco > 14;
})
