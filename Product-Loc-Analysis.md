# Estudo Completo: Modelo Estrela com PK e FK (Modelo de Dados) Aplicado ao Projeto de Vendas da SuperStore

## Introdução

Ao lidarmos com grandes volumes de informações transacionais, como pedidos de vendas, envio de produtos e lucros, é necessário organizar os dados de forma que fiquem prontos para análise. Para isso, usamos técnicas de modelagem de dados voltadas para **Business Intelligence (BI)** e **Data Warehousing**.

O modelo de dados da **SuperStore** é um exemplo clássico utilizado em análises de BI. Ele organiza os dados de vendas de uma empresa que comercializa produtos em diversos segmentos e regiões. A estrutura facilita consultas analíticas sobre vendas, lucros, desempenho por cliente, produto, região, entre outros.

## 🧩 Modelo Estrela

O modelo estrela organiza os dados em uma **tabela de fatos** central conectada a várias **tabelas de dimensão**. A tabela de fatos armazena os dados quantitativos (**medidas**), enquanto as dimensões fornecem o **contexto** dessas medidas.

### Estrutura:

- **Fato:** `ORDER_ITEM` (contém medidas como vendas, lucro, quantidade)
- **Dimensões:** `ORDER`, `CUSTOMER`, `PRODUCT`, `CATEGORY`, `LOCATION`

### Exemplos de Análises Permitidas:

- Total de vendas por região
- Lucro por segmento de cliente
- Volume de produtos vendidos por categoria

## 📐 Modelagem de Dados (Explicações Técnicas)

### 1. LOCATION

- Representa a localização geográfica da entrega e do cliente.
- **PK:** `location_id`
- Campos: `country`, `state`, `city`, `postal_code`, `region`
- Relacionamentos:
  - Um cliente está em uma LOCATION
  - Uma entrega ocorre em uma LOCATION

### 2. CUSTOMER

- Armazena informações sobre os clientes.
- **PK:** `customer_id`
- **FK:** `location_id`
- Campos: `customer_name`, `segment` (Ex: Consumer, Corporate)

### 3. CATEGORY

- Representa a classificação dos produtos.
- **PK:** `category_id`
- Campos: `category_name`, `sub_category` (Ex: Technology > Phones)

### 4. PRODUCT

- Lista todos os produtos vendidos.
- **PK:** `product_id`
- **FK:** `category_id`

### 5. ORDER

- Contém informações do pedido.
- **PK:** `order_id`
- **FKs:** `customer_id`, `location_id`
- Campos:
  - `order_date`
  - `ship_date`
  - `delivery_days`
  - `ship_mode`

### 6. ORDER_ITEM (Fato)

- Tabela central do modelo.
- **PK:** `order_item_id`
- **FKs:** `order_id`, `product_id`
- Métricas:
  - `sales`
  - `quantity`
  - `profit`
    

---

## ✅ Benefícios da Modelagem Estrela

- **Facilidade de Consulta:** JOINs simples e rápidos.
- **Desempenho:** Ideal para agregações em grandes volumes.
- **Modularidade:** Fácil de expandir com novas dimensões ou métricas.
- **Rastreabilidade:** Permite rastrear cada venda até o cliente, localização, produto e categoria.

<div align="center">
  <img src="https://github.com/user-attachments/assets/4c12715c-340f-4067-bac6-87be8bd05002" alt="image">
</div>

---

## 📊 Análise Completa do Dashboard de Vendas, Lucros e Margens

### 🔹 1. Vendas Totais por Categoria

**Distribuição:**

- Móveis: `$271.730,81` (37%)
- Tecnologia: `$266.087,18` (36%)
- Escritório: `$213.287,27` (29%)

**Insights:**

- "Móveis" lidera com leve vantagem.
- As categorias têm volumes equilibrados — boa diversificação.
- Verificar se alto volume traz retorno adequado em lucro.

---

### 🔹 2. Lucro Total por Categoria

**Distribuição:**

- Escritório: `$60.486,26` (45%)
- Tecnologia: `$39.736,62` (30%)
- Móveis: `$35.018,99` (26%)

**Insights:**

- Escritório é o mais lucrativo mesmo com menos vendas.
- Móveis tem maior venda, mas menor lucro → possíveis margens baixas.

✅ **Ação recomendada:** Analisar custos na categoria Móveis.

---

### 🔹 3. Margem de Lucro por Subcategoria

**Top Margens:**

- Etiquetas: 45,18%
- Papel: 43,48%
- Envelopes: 42,67%
- Copiadoras: 42,60%
- Grampos: 35,56%

**Margens Negativas:**

- Mesas: -13,77%
- Máquinas: -6,59%
- Suprimentos: -5,95%
- Estantes: -1,94%

**Insights:**

- Produtos simples têm margens altas.
- Móveis e itens volumosos geram prejuízo.

📌 **Ações:**

- Expandir itens com alta margem.
- Rever ou eliminar produtos com margens negativas.
- Criar **combos promocionais** com produtos lucrativos.

---

### 🔹 4. Top 10 Produtos por Valor Total de Vendas

**Exemplos:**

1. Canon Copier - `$13.699,90`
2. Letter Opener - `$11.825,90`
3. GBC Binding System - `$10.943,88`
4. HP Copier - `$9.230,73`
5. Galaxy Mega 6.3 - `$8.799,78`

**Insights:**

- Equipamentos com alto valor unitário dominam o faturamento.

📌 **Ação:** Estratégia comercial diferenciada (ex: atendimento e pós-venda personalizados).

---

### 🔹 5. Top 10 Produtos por Volume (Unidades Vendidas)

**Exemplos:**

1. Grampos – 68
2. Papel – 58
3. Grampos coloridos – 52
4. Envelopes – 34
5. USB Mini – 30

**Insights:**

- Produtos com alto giro são baratos e de escritório.
- Alto volume não significa alto faturamento.

📌 **Ações:**

- Garantir estoque contínuo desses produtos.
- Explorar **assinaturas** e **combos mensais corporativos**.

---

## 📌 Insights Estratégicos Finais

- Foco em **produtos de alta margem**.
- Revisar produtos com **prejuízo unitário**.
- Otimizar **mix de produtos** para equilíbrio de volume e lucro.
- Criar **combos inteligentes** (ex: papel + etiquetas + grampos).
- Planejar ações promocionais baseadas nos dados de desempenho.

---

📁 **Projeto disponível em:**  
> [Repositório GitHub](#) _(insira o link do seu repositório aqui)_



