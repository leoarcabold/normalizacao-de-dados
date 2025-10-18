# Projeto de Normalização de Dados

Este repositório contém um projeto de modelagem e normalização de banco de dados, focado na criação de um sistema de gerenciamento de pedidos de produtos. A normalização é realizada para evitar redundância de dados e otimizar a estrutura do banco de dados, melhorando a integridade e eficiência das operações.

## Objetivo

O objetivo deste projeto é criar um banco de dados relacional para uma aplicação de e-commerce que permite gerenciar:

- **Clientes**: informações sobre os clientes (nome, endereço, telefone, e-mail).
- **Produtos**: dados sobre os produtos disponíveis para venda (descrição, categoria e preço).
- **Pedidos**: registro dos pedidos feitos pelos clientes, incluindo o valor total, data e forma de pagamento.
- **Itens de Pedido**: informações detalhadas dos produtos adquiridos em cada pedido.

## Estrutura de Banco de Dados

A seguir, são apresentadas as tabelas que compõem o banco de dados. As tabelas são normalizadas em 3NF (Terceira Forma Normal), com o objetivo de reduzir a redundância e melhorar a integridade referencial.

### 1. Tabela `clientes`

![](https://github.com/leoarcabold/normalizacao-de-dados/blob/main/img/diagrama.png)

A tabela `clientes` contém informações sobre os clientes, incluindo dados pessoais e de contato.

```sql
CREATE TABLE `clientes` (
  `cliente_id` INT NOT NULL AUTO_INCREMENT,
  `nome` VARCHAR(100) NOT NULL,
  `endereco` VARCHAR(255) NOT NULL,
  `telefone` VARCHAR(30) NOT NULL,
  `email` VARCHAR(100) NOT NULL,
  PRIMARY KEY (`cliente_id`)
);



