Aqui está a documentação detalhada do seu projeto SQL, formatada como um arquivo `README.md` padrão.

# 🚗 Projeto de Modelo de Banco de Dados para Concessionárias (`db_auto`)

## 📜 Descrição do Projeto

Este projeto consiste em um modelo de banco de dados simples, criado em SQL, para gerenciar informações básicas de montadoras e modelos de veículos. O objetivo principal é demonstrar a criação de um esquema de banco de dados, a definição de tabelas com chaves primárias e estrangeiras, e a inserção de dados iniciais.

## 🛠️ Tecnologias Utilizadas

  * **SQL (Structured Query Language):** Linguagem de manipulação e definição de dados.
  * **Sistema Gerenciador de Banco de Dados (SGBD):** O código é compatível com a sintaxe padrão de SGBDs como **MySQL** ou **MariaDB** (devido ao uso de `AUTO_INCREMENT` e sintaxe de `INSERT` e `CREATE TABLE`).

## 📁 Estrutura do Banco de Dados

O banco de dados é composto por um esquema principal e duas tabelas:

### 1\. Esquema

| Nome do Esquema | Descrição |
| :--- | :--- |
| `db_auto` | Contém todas as tabelas e dados do projeto. |

### 2\. Tabela `tb_montadora`

Armazena informações sobre as montadoras de veículos.

| Coluna | Tipo de Dado | Restrições | Descrição |
| :--- | :--- | :--- | :--- |
| `idt_montadora` | `INT` | `PRIMARY KEY`, `AUTO_INCREMENT` | Identificador único da montadora. |
| `sgl_montadora` | `VARCHAR(20)` | `NOT NULL`, `UNIQUE KEY` | Sigla da montadora (ex: FIAT, VW). |
| `nme_montadora` | `VARCHAR(50)` | `NOT NULL` | Nome completo da montadora. |

### 3\. Tabela `tb_modelo`

Armazena informações sobre os modelos de veículos e faz referência à sua respectiva montadora.

| Coluna | Tipo de Dado | Restrições | Descrição |
| :--- | :--- | :--- | :--- |
| `idt_modelo` | `INT` | `PRIMARY KEY`, `AUTO_INCREMENT` | Identificador único do modelo. |
| `nme_modelo` | `VARCHAR(50)` | `NOT NULL` | Nome comercial do modelo (ex: Pulse, Onix). |
| `cod_montadora` | `INT` | `NOT NULL`, `FOREIGN KEY` | Chave estrangeira que liga o modelo à `tb_montadora`. |

## 🔗 Relacionamento entre Tabelas

O relacionamento entre as tabelas é de **Um para Muitos (1:N)**:

  * Uma **Montadora** (`tb_montadora`) pode ter **Muitos** **Modelos** (`tb_modelo`).
  * O campo `cod_montadora` na tabela `tb_modelo` é uma **Chave Estrangeira** (`FOREIGN KEY`) que referencia o campo `idt_montadora` (Chave Primária) na tabela `tb_montadora`.

**Restrição:** `CONSTRAINT fk_montadora_modelo FOREIGN KEY (cod_montadora) REFERENCES tb_montadora(idt_montadora)`

## ⚙️ Como Utilizar / Executar

Para replicar este projeto, siga os passos abaixo no seu SGBD (como MySQL Workbench, DBeaver, ou via terminal).

1.  **Criação do Esquema:**

    ```sql
    CREATE SCHEMA db_auto;
    USE db_auto;
    ```

2.  **Criação da Tabela `tb_montadora`:**

    ```sql
    CREATE TABLE tb_montadora(
      idt_montadora INT AUTO_INCREMENT PRIMARY KEY,
      sgl_montadora VARCHAR(20) NOT NULL UNIQUE KEY,
      nme_montadora VARCHAR(50) NOT NULL);
    ```

3.  **Inserção de Dados em `tb_montadora`:**

    ```sql
    INSERT INTO tb_montadora VALUES
      (DEFAULT, 'FIAT', 'Fábrica Italiana de Automóveis de Turim'),
      (DEFAULT, 'VW', 'Volkswagen (Carro do Povo)'),
      (DEFAULT, 'GM', 'General Motors'),
      (DEFAULT, 'GWM', 'Great Wall Motors'),
      (DEFAULT, 'BYD', 'Build Your Dreams');
    ```

4.  **Criação da Tabela `tb_modelo`:**

    ```sql
    CREATE TABLE tb_modelo(
      idt_modelo INT AUTO_INCREMENT PRIMARY KEY,
      nme_modelo VARCHAR(50) NOT NULL,
      cod_montadora INT NOT NULL,
      CONSTRAINT fk_montadora_modelo FOREIGN KEY (cod_montadora) 
        REFERENCES tb_montadora(idt_montadora)
      );
    ```

5.  **Inserção de Dados em `tb_modelo`:**

    ```sql
    INSERT INTO tb_modelo VALUES
      (DEFAULT, 'Pulse', 1),
      (DEFAULT, 'Argo', 1),
      (DEFAULT, 'Nivus', 2),
      (DEFAULT, 'Polo', 2),
      (DEFAULT, 'Onix', 3),
      (DEFAULT, 'Haval H6', 4),
      (DEFAULT, 'Tank 300', 4),
      (DEFAULT, 'Ora 03', 4),
      (DEFAULT, 'King', 5);
    ```

6.  **Verificação dos Dados:**

    ```sql
    SELECT * FROM tb_montadora;
    SELECT * FROM tb_modelo;
    ```

## 📈 Dados Atuais Inseridos

### Montadoras (`tb_montadora`)

| idt\_montadora | sgl\_montadora | nme\_montadora |
| :---: | :---: | :--- |
| 1 | FIAT | Fábrica Italiana de Automóveis de Turim |
| 2 | VW | Volkswagen (Carro do Povo) |
| 3 | GM | General Motors |
| 4 | GWM | Great Wall Motors |
| 5 | BYD | Build Your Dreams |

### Modelos (`tb_modelo`)

| idt\_modelo | nme\_modelo | cod\_montadora |
| :---: | :---: | :---: |
| 1 | Pulse | 1 (FIAT) |
| 2 | Argo | 1 (FIAT) |
| 3 | Nivus | 2 (VW) |
| 4 | Polo | 2 (VW) |
| 5 | Onix | 3 (GM) |
| 6 | Haval H6 | 4 (GWM) |
| 7 | Tank 300 | 4 (GWM) |
| 8 | Ora 03 | 4 (GWM) |
| 9 | King | 5 (BYD) |

