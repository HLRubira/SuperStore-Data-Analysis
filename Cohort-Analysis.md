# Análise de Cohort - SuperStore

## O Problema de Negócio
A **SuperStore** é uma rede de supermercados com unidades espalhadas por todo o país, fornecendo alimentos e diversos produtos para consumo. Recentemente, os gerentes identificaram um problema crescente: **retenção de clientes**.

Embora as vendas continuem ocorrendo, a frequência de compras de clientes recorrentes está diminuindo. O time de dados terá um papel fundamental na criação de **indicadores que mostrem como os clientes interagem com a loja ao longo do tempo**.

### Objetivo do Projeto
Este projeto visa responder questões como:
- **Por que os clientes estão comprando menos na SuperStore?**
- **Quais estratégias podem ser implementadas para reverter essa tendência?**
- **Como melhorar a fidelidade dos clientes?**

## 📂 Base de Dados
Os dados utilizados no projeto estão organizados em quatro arquivos principais:

| Arquivo        | Descrição                                       |
|---------------|-------------------------------------------------|
| **Customer.csv**  | Dados dos clientes de todas as lojas da rede. |
| **Location.csv**  | Localização onde as compras foram feitas.   |
| **Orders.csv**    | Pedidos realizados nas lojas em um período.  |
| **Product.csv**   | Características dos produtos comercializados. |

##  Planejamento da Solução
A metodologia utilizada será a **análise de cohort**, que segmenta os clientes com base na data da primeira compra para identificar padrões de retenção e engajamento ao longo do tempo.

### 🔹 O que é um Cohort?
Um **cohort** é um grupo de clientes que compartilham uma mesma característica em um determinado momento. No contexto da SuperStore, podemos agrupar clientes com base na **data da primeira compra** e analisar seu comportamento nos meses seguintes.

### 🔹 Como definir um Cohort?
A definição de cohort depende do objetivo da análise. Para a SuperStore, serão utilizados:
1. **Data da primeira compra**.
2. **Data de registro em um programa de fidelidade**.
3. **Primeiro uso de um cupom de desconto**.

### 🔹 Benefícios da Análise de Cohort
A Análise de Cohort permite identificar padrões de comportamento ao longo do tempo, respondendo perguntas como:
- Os clientes que compraram no mês X continuam comprando nos meses seguintes?
- Qual é a taxa de retenção ao longo dos meses?
- Em que momento os clientes param de comprar?

## ⚙️ Etapas da Análise
###  Passo 1: Definição do Fato
- **Customer ID**: Identifica cada cliente de forma única.

###  Passo 2: Definição das Dimensões

| Coluna       | Dimensão  | Descrição                         |
|-------------|-----------|---------------------------------|
| **Order Date**  | Tempo     | Quando aconteceu?              |
| **Ship Date**   | Tempo     | Data de envio.                 |
| **Ship Mode**   | Entrega   | Como foi entregue?             |
| **Sales**       | Produto   | O que foi comprado?            |
| **Quantity**    | Produto   | Quantidade comprada.           |
| **Discount**    | Produto   | Valor do desconto aplicado.    |
| **Product**     | Produto   | Identificação do produto.      |
| **User ID**     | Cliente   | Quem comprou?                  |

### Passo 3: Combinação Fato-Dimensão
- Quantidade de clientes (**fato**) que realizaram novos pedidos nos meses seguintes à primeira compra (**order date**).
- Dimensões derivadas pelo tempo para calcular a retenção.

###  Passo 4: Escolha dos Gráficos

| Gráfico | Mensagem | Recurso Visual |
|----------|----------|---------------|
| Quantidade de clientes que fizeram novos pedidos | Retenção | Tabela |

###  Passo 5: Painel Macro-Micro
- Painel interativo contendo a tabela de retenção por cohort.
  
![Análise de Cohort](https://github.com/user-attachments/assets/1135b035-0b32-4aa7-94d2-171a218b0579)

## 🚀 Implementação Técnica
### Passo 6: Inicialização da Solução
#### 📝 Exemplo de Saída Esperada
| Customer ID | Mês da Aquisição | Mês da Atividade | Mês Decorrido |
|------------|----------------|----------------|---------------|
| AA-10315  | 2014-03        | 2014-03        | 0             |
| AA-10315  | 2014-03        | 2014-09        | 6             |
| AA-10315  | 2014-03        | 2015-10        | 19            |
| AA-10375  | 2014-04        | 2014-04        | 0             |
| AA-10375  | 2014-04        | 2014-10        | 6             |

### Planejamento do Processo ETL
1. **União das tabelas** (Orders, Customers, Products).
2. **Definir os cohorts** com base na primeira compra.
3. **Encontrar o mês da primeira compra** de cada cliente.
4. **Calcular o tempo decorrido** entre cada compra e a primeira compra.
5. **Construir a tabela de cohort percentual**.
6. **Interpretar os resultados e gerar insights**.

###  Identificação das Entradas
| Fonte de Dados | Campos Utilizados |
|---------------|-----------------|
| **Orders.csv**   | Mês de Aquisição, Atividade, Tempo Decorrido |
| **Customer.csv** | Customer ID |


# Análise de Cohort - Retenção de Usuários
![Cohort](https://github.com/user-attachments/assets/28ed19b0-633c-4272-b374-8d4bd5781b14)

## 1. Estrutura da Tabela

- **Linhas**: Indicam os períodos de entrada (jan/2014 a dez/2014).
- **Colunas**: Representam o número de meses após a entrada (0 a 12 meses).
- **Células**: Contêm percentuais, indicando a retenção relativa ao período inicial (coluna "0" que sempre tem 100%).

## 2. Interpretação das Cores

- 🟩 **Verde**: Retenção mais alta (100% na coluna 0 e valores elevados nas colunas seguintes).
- ⚪ **Branco**: Retenção intermediária.
- 🟥 **Vermelho**: Retenção baixa ou nula.

## 3. Padrões Observados

### 3.1 Retenção Inicial (Coluna 0)
- Como esperado, todas as coortes começam com **100% de retenção**, pois representam o ponto de entrada dos usuários.

### 3.2 Queda de Retenção ao Longo do Tempo
- Há uma **queda perceptível** da retenção ao longo dos meses.
- Em alguns meses (ex: **novembro e dezembro de 2014**), a retenção **despenca rapidamente para 0%**, indicando que os usuários não se mantiveram ativos.

### 3.3 Exceções e Tendências Positivas
- Algumas coortes, como **janeiro, fevereiro e março de 2014**, apresentam **taxas razoáveis de retenção** por mais meses.
- **Janeiro de 2014** mantém uma retenção significativa até **o 11º mês (22%) e o 12º mês (9%)**.
- **Agosto de 2014** também apresenta uma retenção relativamente alta até o **3º mês**.

### 3.4 Meses com Retenção Baixa
- A partir de **setembro de 2014**, a retenção **cai rapidamente**, sugerindo que algo pode ter afetado a experiência dos usuários nesse período (**mudanças no produto, sazonalidade, etc.**).
- **Dezembro de 2014** é o **pior mês**, com **100% de abandono após o primeiro mês**.

## 4. Possíveis Conclusões

- Há uma tendência clara de **queda de retenção ao longo do tempo**, o que é comum em muitas análises de cohort.
- O desempenho de **jan-mar de 2014 foi melhor** em retenção a longo prazo.
- Algo pode ter impactado negativamente a retenção **a partir de setembro de 2014**, o que merece investigação mais aprofundada.

## 5. Próximos Passos

### 📊 Analisar os motivos da queda de retenção:
- Houve **mudanças na oferta, na concorrência ou na experiência do usuário**?

### 📈 Comparar com outras métricas:
- Cruzar esses dados com **churn, feedback de clientes e mudanças no produto**.

### 🎯 Implementar ações de reengajamento:
- Estratégias como **campanhas de e-mail, notificações e melhorias no produto** podem ajudar a melhorar a retenção.

## Conclusão
A análise de cohort será essencial para identificar padrões de retenção e comportamento dos clientes da SuperStore. Com essas informações, a empresa poderá **desenvolver estratégias para aumentar a lealdade do cliente e reduzir a perda de compradores recorrentes**.


