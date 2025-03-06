# SuperStore - Análise de Retenção de Clientes

A **SuperStore** é uma rede de supermercados com várias unidades físicas espalhadas por todo o país, com o objetivo de fornecer alimentos e comercializar os mais diversos produtos para consumo.

Recentemente, o time de gerentes da SuperStore identificou um desafio crescente: a retenção de clientes. A empresa percebeu que, embora as vendas continuem ocorrendo, a frequência de compras de clientes recorrentes tem diminuído.

O time de Dados terá um papel fundamental na criação de indicadores que mostrem como os clientes interagem com a SuperStore ao longo do tempo. Essas análises vão gerar insights valiosos que permitirão à SuperStore entender os motivos que levem os clientes a diminuírem suas compras ou a não retornarem, além de oferecer soluções para melhorar a retenção.

Questões como:
- “O que está fazendo com que os clientes deixem de comprar na SuperStore?”
- “Quais iniciativas podem reverter esses comportamentos?”
- “Como podemos aumentar a fidelidade dos nossos clientes?”

Serão respondidas a partir dos dados.

## Base de Dados

| Arquivo        | Descrição                                                   |
|----------------|-------------------------------------------------------------|
| `Customer.csv` | Dados dos clientes de todas as lojas da rede                |
| `Location.csv` | Localização onde as compras foram feitas                    |
| `Orders.csv`   | Arquivo com todos os pedidos realizados nas lojas, dentro de um período |
| `Product.csv`  | Características dos produtos comercializados nas lojas     |

## Análise de Cohort

A **Análise de Cohort** é uma técnica analítica que agrupa indivíduos ou eventos com características comuns durante um determinado período para observar seu comportamento ao longo do tempo. Essa abordagem ajuda a entender como diferentes segmentos de clientes ou usuários se comportam após uma ação inicial, como uma compra ou uma visita a uma loja.

### O que é um Cohort?

Um **Cohort** é um grupo de indivíduos ou eventos que compartilham uma característica comum em um determinado momento. No contexto da SuperStore, um cohort pode ser composto por clientes que realizaram sua primeira compra em um mesmo mês ou semana. A ideia é acompanhar o comportamento desses clientes ao longo do tempo para entender sua lealdade, frequência de compras e retenção.

### Como definir um Cohort?

A definição de **Cohort** depende do objetivo da análise. No caso da SuperStore, que está interessada em melhorar a retenção de clientes, os cohorts podem ser definidos com base na data da primeira compra. Por exemplo, pode-se criar um cohort de todos os clientes que compraram pela primeira vez em janeiro e acompanhar como eles continuam a comprar nos meses subsequentes.

Outros exemplos de definição de cohorts incluem:
1. Data da primeira compra.
2. Data de registro em um programa de fidelidade.
3. Primeiro uso de um cupom de desconto.

### Qual a função de uma Análise de Cohort?

A **Análise de Cohort** permite identificar padrões de comportamento ao longo do tempo, ajudando a responder perguntas como:
1. “Os clientes que compraram no mês X continuam comprando nos meses seguintes?”
2. “Qual é a taxa de retenção ao longo dos meses?”
3. “Em qual momento os clientes começam a abandonar a SuperStore?”

No contexto de retenção de clientes, a função da Análise de Cohort é mostrar se e quando os clientes estão deixando de comprar, permitindo à SuperStore implementar estratégias para melhorar a fidelidade e reduzir a perda de clientes.
