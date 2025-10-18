A documentação a seguir está formatada em Markdown (README.md) para apresentação no GitHub, abrangendo tanto a estrutura SQL do sistema de vendas quanto a metodologia eficiente de importação de dados.

---

# 💾 Projeto SQL: Estrutura Base de Dados de Vendas

Este repositório contém os scripts SQL e a documentação necessária para configurar um banco de dados de vendas, focado na tabela de pedidos, e orientações sobre como preencher essa tabela rapidamente usando arquivos de dados externos.

## 1. Configuração Inicial do Banco de Dados

O projeto utiliza o banco de dados **`sistema_vendas`**, que deve ser criado antes de popular as tabelas.

```sql
CREATE DATABASE IF NOT EXISTS `sistema_vendas`;
USE `sistema_vendas`;
```
O script fornecido garante que a tabela principal seja recriada, caso já exista (`DROP TABLE IF EXISTS`).

## 2. Estrutura da Tabela `pedidos`

A tabela `pedidos` é a estrutura central deste sistema. Ela foi projetada para armazenar **um registro para cada item vendido dentro de um pedido específico**.

| Coluna | Tipo de Dado | Descrição | Fontes |
| :--- | :--- | :--- | :--- |
| **`pedido_numero`** | INT | Identificador do pedido. | |
| `data_pedido` | DATE | Data em que o pedido foi realizado. | |
| `valor_total_pedido` | DECIMAL(10,2) | O valor total pago pelo pedido. | |
| `forma_pagamento` | VARCHAR(30) | Método de pagamento (e.g., PIX, Boleto). | |
| `cliente_id` | INT | Identificador do cliente. | |
| `cliente_nome` | VARCHAR(100) | Nome do cliente. | |
| `cliente_endereco` | VARCHAR(255) | Endereço completo do cliente. | |
| `cliente_telefone` | VARCHAR(30) | Telefone de contato. | |
| `cliente_email` | VARCHAR(100) | Email do cliente. | |
| **`produto_id`** | INT | Identificador do produto. | |
| `produto_descricao` | VARCHAR(150) | Nome ou descrição do item. | |
| `produto_categoria` | VARCHAR(50) | Categoria do item (e.g., 'Eletrônicos', 'Vestuário'). | |
| `preco_unitario` | DECIMAL(10,2) | Preço individual do produto. | |
| `quantidade` | INT | Quantidade de itens comprados. | |
| `valor_item` | DECIMAL(10,2) | Valor total do item (Preço Unitário \* Quantidade). | |

### Chave Primária
A chave primária é **composta** pelos campos `pedido_numero` e `produto_id`.

## 3. Dados de Exemplo

O script inclui instruções `INSERT INTO` para popular a tabela com dados iniciais.

Os registros de exemplo demonstram:
*   Pedidos realizados entre **2025-01-05 e 2025-03-02**.
*   Registros de vendas mais antigas, datando de **2023-05-01 a 2023-05-13**.
*   Diversas formas de pagamento, como **'Cartão de crédito'**, **'PIX'**, **'Boleto'**, **'Cartão de débito'**, e **'Dinheiro'**.

## 4. Importação Rápida de Dados em Massa (CSV)

Para preencher grandes volumes de dados de forma rápida e eficiente, o MySQL utiliza o comando **`LOAD DATA INFILE`**. Este é o método mais rápido para transferir dados tabulares de um arquivo de texto simples, como um CSV, para uma tabela.

### O que é CSV?

CSV (Comma-Separated Values) é um formato de arquivo estruturado onde os dados são organizados em linhas (registros) e colunas (campos). Os valores de cada coluna são separados por um **delimitador**, que pode ser uma vírgula (`,`), ponto e vírgula (`;`) ou tabulação.

### Sintaxe do `LOAD DATA INFILE`

A sintaxe básica é crucial para informar ao MySQL como interpretar o arquivo de texto:

```sql
LOAD DATA INFILE 'caminho/para/arquivo.csv'
INTO TABLE nome_da_tabela
FIELDS TERMINATED BY 'delimitador'
ENCLOSED BY 'caractere_delimitador'
LINES TERMINATED BY 'terminador_de_linha';
```

### Componentes Chave

| Cláusula | Função | Detalhes Importantes | Fontes |
| :--- | :--- | :--- | :--- |
| `LOAD DATA INFILE` | Indica onde o MySQL deve encontrar o arquivo. | O caminho para o arquivo CSV deve ser completo e acessível pelo MySQL. | |
| `FIELDS TERMINATED BY` | Define o caractere usado para separar as colunas no arquivo CSV. | Se o arquivo usa ponto e vírgula, deve-se definir `FIELDS TERMINATED BY ';'`. O padrão é a vírgula (`,`). | |
| `ENCLOSED BY` | Especifica o caractere que delimita campos de texto (Opcional). | Por exemplo, se os dados de texto estiverem entre aspas duplas, defina `ENCLOSED BY '"'`. | |
| `LINES TERMINATED BY` | Define o caractere ou sequência que marca o final de cada linha (registro). | O valor padrão é a nova linha (`\n`). Em ambientes Windows, pode ser necessário usar `\r\n`. | |
| `IGNORE 1 ROWS` | Ignora a primeira linha do arquivo. | É crucial quando o arquivo CSV inclui o cabeçalho (nomes das colunas), impedindo que ele seja inserido como dado. | |

**Atenção:** É imprescindível que a ordem e os tipos de dados das colunas no arquivo CSV correspondam à estrutura da tabela no banco de dados para que a importação seja bem-sucedida.
