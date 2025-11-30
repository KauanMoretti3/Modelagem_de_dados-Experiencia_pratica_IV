# Modelagem-de-dados---Experi-ncia-pr-tica-IV
Código SQL comentado. Baseado nas experiências práticas da graduação de CC. 


## 1. CRIAÇÃO DAS TABELAS (DDL)


CREATE TABLE FORNECEDOR (
    pk_IDfornecedor INT PRIMARY KEY,
    nome_fornecedor VARCHAR(100)
);

CREATE TABLE ENDERECO (
    pkfk_IDfornecedor INT PRIMARY KEY,
    rua VARCHAR(100),
    numero VARCHAR(10),
    bairro VARCHAR(100),
    FOREIGN KEY (pkfk_IDfornecedor) REFERENCES FORNECEDOR(pk_IDfornecedor)
);

CREATE TABLE NOTA (
    pk_NumeroNota INT PRIMARY KEY,
    data_emissao DATE,
    valor_total DECIMAL(10,2),
    fk_IDfornecedor INT,
    FOREIGN KEY (fk_IDfornecedor) REFERENCES FORNECEDOR(pk_IDfornecedor)
);

CREATE TABLE PRODUTO (
    id_produto INT PRIMARY KEY,
    fk_NumeroNota INT,
    quantidade INT,
    validade DATE,
    FOREIGN KEY (fk_NumeroNota) REFERENCES NOTA(pk_NumeroNota)
);


## 2. POPULAÇÃO DAS TABELAS (INSERTS)


INSERT INTO FORNECEDOR VALUES (1, 'Fornecedor Alfa');
INSERT INTO FORNECEDOR VALUES (2, 'Fornecedor Beta');
INSERT INTO FORNECEDOR VALUES (3, 'Fornecedor Gama');

INSERT INTO ENDERECO VALUES (1, 'Rua das Flores', '120', 'Centro');
INSERT INTO ENDERECO VALUES (2, 'Avenida Brasil', '2000', 'Jardim América');
INSERT INTO ENDERECO VALUES (3, 'Rua Projetada', '45', 'Industrial');

INSERT INTO NOTA VALUES (101, '2025-02-15', 1200.50, 1);
INSERT INTO NOTA VALUES (102, '2025-03-10', 850.00, 2);
INSERT INTO NOTA VALUES (103, '2025-04-05', 4300.00, 1);

INSERT INTO PRODUTO VALUES (10, 101, 50, '2026-01-01');
INSERT INTO PRODUTO VALUES (11, 101, 10, '2025-12-15');
INSERT INTO PRODUTO VALUES (12, 102, 100, '2026-03-20');
INSERT INTO PRODUTO VALUES (13, 103, 5, '2025-11-11');


## 3. CONSULTAS SELECT


SELECT N.pk_NumeroNota, N.data_emissao, F.nome_fornecedor
FROM NOTA N
JOIN FORNECEDOR F ON N.fk_IDfornecedor = F.pk_IDfornecedor;

SELECT id_produto, quantidade, validade
FROM PRODUTO
WHERE fk_NumeroNota = 101;

SELECT * FROM FORNECEDOR
ORDER BY nome_fornecedor ASC;

SELECT pk_NumeroNota, valor_total
FROM NOTA
ORDER BY valor_total DESC
LIMIT 2;

SELECT F.nome_fornecedor, E.rua, E.numero, E.bairro
FROM FORNECEDOR F
JOIN ENDERECO E ON F.pk_IDfornecedor = E.pkfk_IDfornecedor;


## 4. UPDATES


UPDATE FORNECEDOR
SET nome_fornecedor = 'Fornecedor Alfa LTDA'
WHERE pk_IDfornecedor = 1;

UPDATE NOTA
SET valor_total = 900.00
WHERE pk_NumeroNota = 102;

UPDATE PRODUTO
SET quantidade = quantidade + 20
WHERE id_produto = 12;


## 5. DELETES


DELETE FROM PRODUTO
WHERE id_produto = 13;

DELETE FROM NOTA
WHERE pk_NumeroNota = 103;

DELETE FROM FORNECEDOR
WHERE pk_IDfornecedor = 3;
