# Segmentação de Clientes - Análise RFM | SuperStore

## Contexto do Negócio

A SuperStore é uma rede de supermercados com unidades físicas espalhadas por todo o país, atuando na venda de alimentos e diversos produtos de consumo.

Recentemente, o time de dados desenvolveu uma análise de **Cohort** para acompanhar a **retenção de clientes**, revelando bons resultados para alguns grupos e desempenho ruim para outros.

Com base nessas informações, a liderança decidiu implementar **ações específicas para diferentes grupos de clientes**, com o objetivo de aumentar a taxa de retenção. No entanto, ainda não havia clareza sobre **como segmentar os clientes** nem quais ações seriam mais eficazes para cada grupo.

Esse desafio foi encaminhado ao time de dados, que agora tem como missão segmentar a base de clientes, criando grupos menores e com características semelhantes. O objetivo é permitir ações mais direcionadas pelos times de Marketing, Vendas e Produtos.

## Objetivo

Aplicar a técnica de segmentação **RFM (Recência, Frequência e Valor Monetário)** para entender o comportamento dos clientes e propor ações personalizadas que contribuam para:

- Aumentar a retenção de clientes
- Melhorar a fidelização
- Otimizar os investimentos em marketing e relacionamento

## Análise RFM

A análise RFM é baseada em três variáveis fundamentais:

### Recência (R)
Refere-se ao tempo desde a última compra. Clientes que compraram recentemente tendem a estar mais engajados e são mais propensos a responder a campanhas.

### Frequência (F)
Mede o número de vezes que o cliente comprou em um determinado período. Clientes com alta frequência tendem a ser mais fiéis à marca.

### Valor Monetário (M)
Corresponde ao total gasto pelo cliente. Clientes que gastam mais são considerados mais valiosos.

A metodologia consiste em atribuir escores para cada variável (geralmente de 1 a 5). Com base nas pontuações combinadas, os clientes são agrupados em segmentos como:

- Campeões
- Fiéis em potencial
- Clientes em risco
- Novos clientes promissores
- Clientes perdidos

Esses segmentos ajudam a direcionar campanhas com maior precisão, aumentando a eficiência das estratégias comerciais.

## Planejamento da Solução

### 1. Definição dos Fatos

| Métrica     | Coluna       | Descrição                                 |
|-------------|--------------|-------------------------------------------|
| Recência    | `Order Date` | Dias desde a última compra                |
| Frequência  | `Order ID`   | Quantidade de pedidos realizados          |
| Monetização | `Sales`      | Soma dos valores gastos por cliente       |

### 2. Definição das Dimensões

| Coluna       | Dimensão | Descrição                          |
|--------------|----------|------------------------------------|
| Order Date   | Tempo    | Data da compra                     |
| Ship Date    | Tempo    | Data de envio                      |
| Ship Mode    | Entrega  | Método de envio                    |
| Sales        | Produto  | Valor da venda                     |
| Quantity     | Produto  | Quantidade comprada                |
| Discount     | Produto  | Desconto aplicado                  |
| Product      | Produto  | Identificador do produto           |
| User ID      | Cliente  | Identificação do cliente           |

### 3. Combinação Fato-Dimensão

- Quantidade de pedidos por cliente (frequência)
- Soma dos valores de pedidos por cliente (monetização)
- Tempo desde a última compra por cliente (recência)

### 4. Escolha dos Gráficos

| Gráfico             | Objetivo                                      |
|---------------------|-----------------------------------------------|
| Gráfico de Árvore   | Visualizar a quantidade de clientes por grupo|

### 5. Painel de Visão Geral

- Exibição macro e micro dos segmentos com filtros interativos
- Destaque para grupos mais valiosos e em risco

## Etapas do Processo (Metodologia SAPE)

### Etapa 1: Determinar a Saída

| Customer ID | Recência | Frequência | Monetização | Segmento             |
|-------------|----------|------------|--------------|----------------------|
| CG – 12040  | 49       | 9          | 904.47       | Fiéis em potencial   |
| CG – 12520  | 338      | 5          | 1,147.78     | Clientes perdidos    |
| DV – 13045  | 19       | 9          | 1,119.48     | Fiéis em potencial   |
| SO – 20335  | 29       | 15         | 2,602.58     | Clientes perdidos    |
| BH – 11710  | 23       | 24         | 6,225.35     | Campeões             |

### Etapa 2: Planejar o Processo

1. Unir as tabelas necessárias
2. Calcular Recência, Frequência e Monetização por cliente
3. Atribuir notas (escores) para cada uma das variáveis
4. Criar os segmentos com base na combinação dos escores
5. Associar cada cliente a um segmento
6. Interpretar os dados
7. Propor ações específicas para cada grupo

### Etapa 3: Identificar as Entradas

- `Customer.csv` → Customer ID
- `Product.csv` → Detalhes dos produtos
- `Location.csv` → Detalhes da localização
- `Orders.csv` → Datas de compra e atividade

## Recomendações Estratégicas por Segmento

| Segmento              | Ação Recomendada                                                                 |
|------------------------|----------------------------------------------------------------------------------|
| Campeões              | Oferecer benefícios exclusivos, programas de fidelidade e acesso antecipado     |
| Fiéis em potencial    | Estimular com ofertas personalizadas para aumentar frequência                   |
| Clientes em risco     | Reengajar com campanhas de reativação, cupons e e-mails personalizados           |
| Novos promissores     | Nutrir com boas experiências e acompanhamento personalizado                     |
| Clientes perdidos     | Avaliar custo-benefício de tentar reativação ou deixar sair naturalmente         |


---
# Desenvolvimento da Solução

<p align="center">
  <img src="https://github.com/user-attachments/assets/ea6fd03b-801e-4c1b-9d55-e99b8fbeac01" alt="Segmentação RFM" />
</p>

A análise de segmentação **RFM** — que considera a **Recência**, **Frequência** e **Valor Monetário** de cada cliente — nos ajuda a entender melhor o comportamento da base de clientes e a direcionar estratégias personalizadas. A seguir, apresento os principais destaques e interpretações com base nos dados obtidos:

---

### Fieis Potenciais (`38,5%`)

Esse é o maior grupo da base. São clientes com bom histórico de compra e grande chance de se tornarem fiéis.  
**Oportunidade de crescimento**: invista em ofertas personalizadas, nutrição com conteúdo e incentivo à recompra.

---

### Fieis (`28,5%`)

Clientes já engajados e com relacionamento estável com a empresa.  
**Manter engajamento** com programas de fidelidade, reconhecimento e relacionamento contínuo.

---

### Campeões (`3,5%`)

Clientes mais valiosos: compram com frequência, recentemente e em alto volume.  
**Alta prioridade**: atendimento VIP, benefícios exclusivos e contato direto.

---

### Risco + Perdidos (`8,6% + 10,5% = 19,1%`)

Clientes que demonstram forte tendência de abandono ou já foram perdidos.  
**Atenção imediata**: estratégias de retenção, pesquisas de satisfação e campanhas de reativação.

---

### Novos Clientes (`2,4%`)

Estão começando o relacionamento com a empresa.  
**Boas-vindas e onboarding eficaz** são fundamentais para gerar confiança e engajamento inicial.

---

### Precisam de Atenção, Hibernando, Quase Dormentes e Promissores (`~8%`)

Grupos menores em fases intermediárias.  
**Ações segmentadas** como campanhas de reengajamento, ofertas específicas e estímulo à atividade.

---

### Não Perder (`0,3%`)

Clientes valiosos prestes a sair.  
**Prioridade máxima**: intervenções personalizadas e rápidas para evitar a perda.

---

## Conclusão

A segmentação **RFM** revela que a empresa possui uma base sólida de clientes fiéis e com alto potencial de crescimento. No entanto, há áreas críticas que exigem atenção imediata — principalmente clientes em risco ou já perdidos.

Com **estratégias bem direcionadas para cada grupo**, é possível:
- Aumentar a fidelização;
- Melhorar o valor do ciclo de vida dos clientes;
- E reduzir perdas de receita.

---



