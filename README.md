# 📊 Banco de Dados – Sistema de Vagas e Candidatos - LinkeTinder

Este repositório contém a modelagem e scripts SQL de um banco de dados relacional voltado para um sistema de **match entre candidatos e vagas**, permitindo o gerenciamento de usuários, empresas e competências.

---

## 🔗 Modelagem do Banco

A modelagem deste banco de dados foi criada utilizando a ferramenta online dbdiagram:

- [https://dbdiagram.io/d/69d3c27080896296842c3d30](https://dbdiagram.io/d/69d3c27080896296842c3d30)

Essa plataforma foi utilizada para estruturar e visualizar os relacionamentos entre as entidades de forma clara antes da implementação em SQL.

---

## 📌 Objetivo

Estruturar um banco de dados capaz de:

- Armazenar informações de candidatos e empresas
- Gerenciar competências (skills)
- Relacionar candidatos às suas competências
- Relacionar vagas às competências exigidas
- Permitir consultas para análise de compatibilidade entre candidatos e vagas

---

## 🧱 Modelagem do Banco

O banco é composto pelas seguintes entidades principais:

### 👤 Candidatos

Armazena dados pessoais dos usuários candidatos.

**Campos principais:**

- id (PK)
- nome
- data\_nascimento
- email (único)
- cpf (único)
- país
- cep
- senha

---

### 🏢 Empresas

Armazena dados das empresas que criam vagas.

**Campos principais:**

- id (PK)
- nome
- cnpj
- descricao
- país
- cep
- senha

---

### 💼 Vagas

Representa oportunidades de emprego criadas pelas empresas.

**Campos principais:**

- id (PK)
- nome
- descricao
- competencias
- local
- empresa\_id (FK)

---

### 🧠 Competências

Lista de tecnologias/habilidades disponíveis no sistema.

**Campos principais:**

- id (PK)
- nome

---

### 🔗 Tabelas de Relacionamento

#### candidato\_competencias

Relaciona candidatos às suas competências.

- candidato\_id (FK)
- competencias\_id (FK)
- nivel (Básico, Intermediário, Avançado)

#### vaga\_competencias

Relaciona vagas às competências exigidas.

- vaga\_id (FK)
- competencia\_id (FK)

---

## 🔗 Relacionamentos

- Um **candidato** pode ter várias competências
- Uma **competência** pode pertencer a vários candidatos
- Uma **vaga** pertence a uma empresa
- Uma **vaga** pode exigir várias competências

---

## 🧪 Dados de Exemplo

O script inclui dados iniciais para testes:

- 5 competências (PostgreSQL, MongoDB, Python, React, Node.js)
- 5 candidatos
- 5 empresas
- Relacionamentos entre candidatos e competências

---

## 🔍 Consultas Importantes

### Listar competências de candidatos

```sql
SELECT c.nome AS Candidato, comp.nome AS Tecnologia, cc.nivel
FROM candidatos c
JOIN candidato_competencias cc ON c.id = cc.candidato_id
JOIN competencias comp ON cc.competencias_id = comp.id;
```

---

### Listar todas as competências

```sql
SELECT * FROM competencias;
```

---

## 🚀 Como Executar

1. Crie um banco de dados (ex: PostgreSQL)
2. Execute o script SQL fornecido
3. Utilize as queries para testar os relacionamentos

---

## 🧠 Considerações Técnicas

- Utilização de **chaves primárias com auto incremento (IDENTITY)**
- Uso de **chaves estrangeiras** para garantir integridade referencial
- Estrutura normalizada com tabelas de relacionamento (N\:N)
- Uso de **constraints UNIQUE** para email e CPF
- Separação clara entre entidades e relacionamentos

---

## 📈 Possíveis Melhorias

- Implementar índice em colunas de busca frequente
- Criar sistema de matching automático entre candidatos e vagas
- Adicionar histórico de candidaturas
- Criar API para consumo dos dados

---

## 📄 Licença

Projeto desenvolvido para fins educacionais.

---

## ✍️ Autor

**Fernando Santos** 🚀

