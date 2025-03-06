# SuperStore Data Analysis

## Problema de Negócio
A **SuperStore** é uma rede de supermercados com várias unidades físicas espalhadas pelo mundo, fornecendo alimentos e diversos produtos de consumo. O time de gerentes da empresa decidiu criar uma equipe de dados para otimizar as decisões relacionadas ao abastecimento de produtos e vendas.

Atualmente, os gerentes acessam planilhas de dados com informações pontuais, mas desejam interligar todos os dados da empresa para que cada área acompanhe os mesmos indicadores. O time de dados terá um papel essencial na geração desses indicadores, analisando o comportamento dos clientes, produtos mais comprados, quantidade comprada, tamanho da cesta de compra, valor médio gasto, produtos devolvidos e número de pedidos realizados em determinado período.

Essas análises gerarão **insights estratégicos** para entender melhor o funcionamento da empresa do ponto de vista analítico, ajudando na tomada de decisão. Nosso time foi contratado para esse desafio e, após o onboarding, recebemos a primeira missão: **analisar os pedidos de compra e extrair insights para o time de negócios.**

## Dados Utilizados
Os dados utilizados neste projeto serão extraídos de quatro arquivos principais:

| Arquivo       | Descrição                                        |
|--------------|------------------------------------------------|
| **Customer.csv** | Dados dos clientes de todas as lojas da rede. |
| **Location.csv** | Localização onde as compras foram feitas. |
| **Orders.csv** | Registro de todos os pedidos realizados. |
| **Product.csv** | Características dos produtos comercializados. |

## Planejamento da Solução
A tomada de decisão baseada em dados é essencial para aumentar a eficiência e a competitividade. Para isso, este projeto implementa um processo **ETL (Extract, Transform, Load)**, que possibilita:

1. **Extração** dos dados de diversas fontes.
2. **Transformação** dos dados para garantir qualidade e padronização.
3. **Carga** dos dados em um repositório centralizado para análise.
   
<p align="center">
  <img src="https://github.com/user-attachments/assets/d0d41a8e-d167-4299-b7d0-2119edca1dfb" alt="etl" width="900">
</p>


Esse processo permitirá estruturar um ambiente **data-driven**, facilitando a análise e obtenção de insights estratégicos.

### Passo 1: Definição do Fato
- **Fato principal:** `Order ID`

### Passo 2: Definição das Dimensões

| Coluna       | Dimensão  | Descrição  |
|-------------|-----------|--------------|
| Order Date  | Tempo    | Quando aconteceu? |
| Ship Date   | Tempo    | Data de envio. |
| Ship Mode   | Entrega  | Como foi entregue? |
| Sales       | Produto  | O que foi comprado? |
| Quantity    | Produto  | Quantidade comprada. |
| Discount    | Produto  | Valor do desconto aplicado. |
| Product     | Produto  | Identificação do produto. |
| User ID     | Cliente  | Quem comprou? |

### Passo 3: Combinação Fato-Dimensão
- Quantidade de pedidos por data (dia, mês, ano, semana, feriado)
- Quantidade de pedidos por data de envio
- Quantidade de pedidos por tier de preço (baixo, médio, alto)
- Quantidade de pedidos por quantidade de itens
- Quantidade de pedidos por tier de desconto
- Quantidade de pedidos por produto
- Quantidade de pedidos por cliente
- Quantidade de pedidos por data e tier de preço
- Quantidade de pedidos por data e quantidade de itens
- Quantidade de pedidos por data e produto
- Quantidade de pedidos por data e clientes
- Quantidade de pedidos por data de envio e tier de preço

### Passo 4: Visualização dos Dados

| Gráfico | Mensagem | Tipo |
|----------|----------|------|
| Quantidade de Pedidos por Data | Crescimento, comparação dia a dia | Linha, Coluna |
| Quantidade de Pedidos por Data de Envio | Crescimento, comparação dia a dia | Linha, Coluna |
| Quantidade de Pedidos por Tier de Preço | Comparativo percentual | Barra, Barra Empilhada |
| Quantidade de Pedidos por Produto | Comparativo, Parte do Todo | Barra, Pizza |
| Quantidade de Pedidos pelo Valor do Pedido | Comparativo | Dispersão |
| Quantidade de Pedidos por Cliente | Crescimento, Comparativo | Linha, Barra |
| Quantidade de Pedidos por Itens | Comparativo | Linha, Barra |

### Passo 5: Painel Macro-Micro
Desenvolver um painel que forneça visão macro e micro dos dados analisados.

### Passo 6: Inicialização da Solução

#### Determinar a Saída:
- Painel com os gráficos interativos.

#### Planejar os Processos:
- Criar gráfico de Linha Macro.
- Criar gráfico da Quantidade de Clientes Únicos.
- Criar gráfico da Quantidade de Pedidos por Cliente.
- Criar gráfico da Quantidade de Pedidos por Itens no carrinho.
- Criar gráfico da Distribuição de Pedidos por Produto.

#### Identificar as Entradas:
- **Fonte de Dados:** `Orders.csv`

---

Esse repositório apresenta a análise dos dados da **SuperStore**, implementando um pipeline **ETL** para extrair insights relevantes que auxiliam na tomada de decisão da empresa. Todas as análises e visualizações estão disponíveis no dashboard final.


# Análise de Dados: Comportamento de Pedidos e Clientes

A análise revelou várias correlações importantes entre o número de clientes, pedidos e o comportamento de compra dos consumidores. A seguir, apresento as principais conclusões:

<p align="center">
  <img src="https://github.com/user-attachments/assets/da5bfa34-b310-46e9-9b50-d7cbca5f8411" alt="Quantidade_Pedidos_Mes" />
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/be91bb22-068c-4e2b-8647-5faf7c19f533" alt="Quantidade_Clientes_Unicos" />
</p>


## 1. Correlação entre Clientes e Pedidos
- A quantidade de clientes está diretamente correlacionada com o número de pedidos realizados. Isso indica que, à medida que a base de clientes aumenta, o número de pedidos também tende a crescer.

## 2. Foco em Novos Clientes
- A empresa tem concentrado esforços em atrair novos clientes. No entanto, para otimizar o retorno sobre esse esforço, é necessário trabalhar na **retenção de clientes** e incentivar compras recorrentes. Isso evitaria depender exclusivamente da aquisição de novos clientes.

## 3. Correlação de Pedidos com Clientes Únicos
- A quantidade de pedidos por mês apresenta uma forte correlação com o número de clientes únicos, mostrando que ambos seguem um padrão de crescimento semelhante.

## 4. Impacto do Número de Produtos por Cliente
- Uma hipótese importante é que o aumento ou diminuição do número de pedidos pode estar relacionado à quantidade de produtos comprados por cliente. Se cada cliente comprasse apenas um produto, o número de pedidos e clientes seria o mesmo. Porém, a realidade é que cada cliente pode realizar múltiplos pedidos, o que resulta em um número de pedidos maior que o de clientes.

---

# Insights Detalhados:



## 1. Variação no Número de Pedidos ao Longo dos Meses
- **Início (381 pedidos/mês)**: O número de pedidos começa em 381 por mês e sofre uma queda em fevereiro.
- **Aumento e Estabilidade**: Em março, há um aumento para uma faixa de 600 a 700 pedidos, que se mantém até agosto.
- **Ação de Marketing/Produto/Preço (agosto)**: Em agosto, uma ação de marketing, produto ou preço provoca um aumento considerável no número de pedidos. No entanto, após esse pico, ocorre uma queda, seguida de uma recuperação, com patamares mais elevados que os anteriores.
- **Ação de Marketing (novembro)**: Em novembro, uma nova ação aumenta ainda mais o número de pedidos, mas a queda em dezembro é muito menor do que as quedas anteriores.

<p align="center">
  <img src="https://github.com/user-attachments/assets/42a5e5eb-0650-49fa-acbe-0130315202a3" alt="Quantidade_Pedidos_Cliente_Unico" />
</p>

## 2. Comportamento dos Clientes Únicos
- **Aumento e Sustentação de Clientes**: O número de clientes adquiridos segue um comportamento semelhante ao número de pedidos. Quando o número de clientes aumentou, o crescimento foi mantido por um período. Posteriormente, houve um aumento considerável de clientes únicos, seguido de uma queda, e depois uma nova fase de crescimento.
- **Dúvida sobre a Influência de Clientes ou Pedidos**: Existe a dúvida sobre se o aumento no número de pedidos foi causado pelo aumento de clientes únicos ou pelo número de pedidos feitos por cada cliente. Para esclarecer isso, analisou-se a **quantidade de pedidos por cliente único**.

## 3. Quantidade de Pedidos por Cliente Único
- **Média de Pedidos**: A média de pedidos por cliente se mantém em 2,4 pedidos. No entanto, em setembro, houve um aumento significativo, chegando a 3 pedidos por cliente, refletindo uma situação em que o número de pedidos foi três vezes maior do que o número de clientes.

<p align="center">
  <img src="https://github.com/user-attachments/assets/c40e4313-a403-48ad-bf7e-03b0142c6243" alt="Quantidade_Pedidos_Itens" />
</p>

## 4. Visão do Produto: Quantidade de Pedidos por Itens
- A maioria dos pedidos contém entre 2 a 3 produtos. Isso sugere que muitas compras são feitas para repor itens que faltam, sendo compras rápidas e com valor mais baixo, ao contrário de grandes compras mensais.

## 5. Modalidade de Entrega
- **Entrega Padrão (60%)**: A maioria das pessoas prefere a entrega padrão, indicando que não há uma grande urgência nas compras. Aproximadamente 60% dos pedidos são feitos com essa modalidade de entrega, sugerindo que os consumidores não têm pressa em receber os produtos.

<p align="center">
  <img src="https://github.com/user-attachments/assets/b211c590-cbee-4ffe-945b-a3a57cc5649f" alt="Modalidade_de_entrega" />
</p>


## Conclusão

A análise realizada revelou importantes correlações entre o número de clientes, pedidos e o comportamento de compra dos consumidores, além de oferecer insights valiosos para melhorar a estratégia da empresa. A partir das observações, foi possível identificar que:

### 1. Crescimento de Pedidos Relacionado a Novos Clientes
A quantidade de pedidos está diretamente ligada ao número de clientes, confirmando que a aquisição de novos clientes contribui para o aumento das vendas. No entanto, a retenção e fidelização de clientes são essenciais para evitar a dependência exclusiva da aquisição de novos clientes, tornando o crescimento mais sustentável.

### 2. Comportamento dos Clientes
A análise do comportamento de clientes únicos revelou que o aumento do número de clientes está diretamente relacionado à quantidade de pedidos, com um padrão de crescimento observado ao longo do tempo. A variação no número de pedidos por cliente, especialmente em setembro, indica que ações de marketing e estratégias de vendas podem impactar significativamente o volume de compras por cliente.

### 3. Análise de Produtos e Compras
A maior parte dos pedidos é composta por dois a três itens, sugerindo que muitos consumidores fazem compras rápidas para reposição de itens. Essa informação pode ajudar a ajustar a estratégia de vendas e marketing para fomentar compras mais robustas e de maior valor.

### 4. Preferência por Entregas Padrão
A maioria dos consumidores prefere a modalidade de entrega padrão, o que pode indicar um comportamento de compra mais relaxado, onde não há urgência na entrega dos produtos.

Com base nesses insights, é possível que a empresa foque não apenas na aquisição de novos clientes, mas também em estratégias de retenção e em ações de marketing que incentivem compras recorrentes e de maior valor. Além disso, a análise detalhada do comportamento de pedidos e clientes pode auxiliar na otimização dos processos de vendas e na criação de campanhas mais eficazes.

Este projeto busca fornecer uma base sólida de dados e informações para tomar decisões estratégicas que maximizem o potencial de vendas e melhorem a experiência do cliente.

