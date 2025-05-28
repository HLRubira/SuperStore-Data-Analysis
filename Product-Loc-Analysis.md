Estudo Completo: Modelo Estrela com PK e FK (Modelo de Dados) Aplicado ao Projeto de Vendas da SuperStore

Ao lidarmos com grandes volumes de informações transacionais, como pedidos de vendas, envio de produtos e lucros, é necessário organizar os dados de forma que fiquem prontos para análise. Para isso, usamos técnicas de modelagem de dados voltadas para **Business Intelligence (BI)** e **Data Warehousing**.

O modelo de dados da **SuperStore** é um exemplo clássico utilizado em análises de BI e Data Warehousing. Ele visa organizar os dados de vendas de uma empresa que comercializa produtos em diversos segmentos e regiões. Este modelo foi estruturado para facilitar consultas analíticas sobre vendas, lucros, desempenho por cliente, produto, região, entre outros.

---

## Modelo Estrela

O modelo estrela organiza os dados em uma **fato central (tabela de fatos)** conectada a várias **dimensões (tabelas de dimensão)**. A tabela de fatos armazena os dados quantitativos (**medidas**), enquanto as dimensões fornecem contexto para essas medidas.

- **Fato**: `ORDER_ITEM` (contém medidas de vendas, lucro, quantidade)  
- **Dimensões**: `ORDER`, `CUSTOMER`, `PRODUCT`, `CATEGORY`, `LOCATION`

Esse formato é ideal para permitir análises como:

- Total de vendas por região  
- Lucro por segmento de cliente  
- Volume de produtos vendidos por categoria  

O foco aqui será compreender a lógica do modelo estrela, como as informações se conectam e por que essa estrutura é tão importante para a inteligência de negócios.

---

## Modelagem de Dados (Explicações Técnicas)

### 1. LOCATION
- Representa a localização geográfica da entrega e do cliente.
- **PK**: `location_id`
- Campos: `country`, `state`, `city`, `postal_code`, `region`
- **Relacionamentos**:
  - Um cliente está localizado em uma `LOCATION`
  - Uma entrega ocorre em uma `LOCATION`

---

### 2. CUSTOMER
- Armazena informações sobre os clientes que efetuam pedidos.
- **PK**: `customer_id`
- **FK**: `location_id` (para `LOCATION`)
- Campos: `customer_name`, `segment` (Ex: Consumer, Corporate)

---

### 3. CATEGORY
- Representa a classificação dos produtos.
- **PK**: `category_id`
- Campos: `category_name`, `sub_category` (Ex: Technology > Phones)

---

### 4. PRODUCT
- Lista todos os produtos vendidos.
- **PK**: `product_id`
- **FK**: `category_id` (para `CATEGORY`)

---

### 5. ORDER
- Contém informações do pedido, como datas e modo de envio.
- **PK**: `order_id`
- **FKs**: `customer_id` (para `CUSTOMER`), `location_id` (para `LOCATION`)
- Campos:
  - `order_date`: data da compra
  - `ship_date`: data de envio
  - `delivery_days`: diferença entre envio e entrega
  - `ship_mode`: modo de envio (Standard, Express, etc.)

---

### 6. ORDER_ITEM
- Tabela de **fatos** central do modelo.
- **PK**: `order_item_id`
- **FKs**: `order_id` (para `ORDER`), `product_id` (para `PRODUCT`)
- Métricas:
  - `sales`: valor da venda
  - `quantity`: quantidade de itens vendidos
  - `profit`: lucro obtido

---

##  Relacionamentos – Modelo de Dados

| Tabela        | FK                         | Referência                        |
|---------------|-----------------------------|-----------------------------------|
| CUSTOMER      | `location_id`              | LOCATION(`location_id`)           |
| PRODUCT       | `category_id`              | CATEGORY(`category_id`)           |
| ORDER         | `customer_id`, `location_id` | CUSTOMER, LOCATION               |
| ORDER_ITEM    | `order_id`, `product_id`   | ORDER, PRODUCT                    |

---

## Benefícios dessa Modelagem

- **Facilidade de Consulta**: Permite análises rápidas com `JOINs` simples.  
- **Desempenho**: Ideal para agregações em grandes volumes de dados.  
- **Modularidade**: Facilidade para expansão com novas dimensões ou métricas.  
- **Rastreabilidade**: Cada venda pode ser rastreada até o cliente, localização, produto e categoria.

---

## Conclusão

O modelo de dados da SuperStore implementado em formato estrela é um exemplo robusto e eficiente para armazenar e consultar informações transacionais de uma loja de vendas. A separação clara entre fatos e dimensões, aliada ao uso correto de chaves primárias e estrangeiras, proporciona uma base sólida para a construção de relatórios analíticos e dashboards em ferramentas como **Power BI** ou **Tableau**.
