# Base de Conhecimento

> [!TIP]
> Prompt que pode ser usado nessa etapa: 
> Preciso organizar a base de conhecimento do meu agente finaceiro educativo. 
> Considere os arquivos anexados: [Liste os arquivos]. 
> Organize as informações em: [Insira a estrutura que quer que as informações sejam organizadas].


## Dados Utilizados

Os seguintes arquivos foram utilizados como base de conhecimento para o agente:

| Arquivo | Formato | Utilização na solução |
|---------|--------|----------------------|
| historico_atendimento.csv | CSV | Contextualizar interações anteriores e entender dúvidas recorrentes do usuário |
| perfil_investidor.json | JSON | Personalizar orientações financeiras com base no perfil, renda, objetivos e momento financeiro do usuário |
| produtos_financeiros.json | JSON | Sugerir opções de produtos financeiros compatíveis com o perfil e objetivos |
| transacoes.csv | CSV | Analisar padrão de gastos, identificar hábitos financeiros e oportunidades de melhoria |

---

## Adaptações nos Dados

Não foram realizadas alterações nos dados mockados fornecidos.

Os arquivos foram utilizados em sua estrutura original, mantendo:
- Formato dos dados (JSON e CSV)
- Campos existentes
- Organização original das informações

A escolha por não modificar os dados foi intencional, visando:
- Foco na construção da lógica do agente
- Simplicidade na primeira versão do projeto
- Validação do funcionamento do agente com dados estruturados básicos

Possíveis melhorias futuras incluem:
- Enriquecimento dos dados com mais atributos
- Inclusão de categorias de gastos mais detalhadas
- Expansão do portfólio de produtos financeiros
- Histórico mais robusto de interações do usuário

---

## Estratégia de Integração

### Como os dados são carregados?

Os arquivos JSON e CSV são carregados no início da sessão do agente.

- JSONs são convertidos em objetos estruturados
- CSVs são transformados em listas/tabelas para análise de padrão

Esses dados são então disponibilizados para o modelo durante a execução das respostas.

---

### Como os dados são usados no prompt?

Os dados podem ser utilizados de forma híbrida, inserindo os dados diretamente no Prompt e caso necessário carregar dados via Python. 

- Parte dos dados (perfil do cliente) é inserida diretamente no **contexto do prompt**

#### Exemplo de Prompt com Dados Reais

O exemplo contém informações das bases de conhecimento. 

```text
Você é o GranaLeve, um assistente de educação financeira para pessoas leigas.

Seu objetivo é:
- Explicar conceitos financeiros de forma simples e acessível
- Ajudar o usuário a organizar suas finanças
- Sugerir melhorias práticas no dia a dia
- Nunca usar linguagem técnica sem explicação

Regras importantes:
- Não faça recomendações específicas de investimento
- Sempre considere o perfil do usuário antes de sugerir algo
- Seja didático, acolhedor e direto
- Quando não souber algo, seja transparente

Contexto do cliente:

Dados do Cliente:
- Nome: João Silva
- Idade: 32 anos
- Profissão: Analista de Sistemas

Perfil financeiro:
- Perfil de investidor: Moderado
- Aceita risco: Não
- Objetivo principal: Construir reserva de emergência

Renda mensal:
- R$ 5.000

Situação atual:
- Patrimônio total: R$ 15.000
- Reserva de emergência atual: R$ 10.000

Metas:
- Completar reserva de emergência: R$ 15.000 até 06/2026
- Entrada do apartamento: R$ 50.000 até 12/2027

Últimas transações:
- Supermercado - R$ 450
- Streaming - R$ 55
- Restaurante - R$ 120
- Transporte - R$ 200
- Compras online - R$ 300

Com base nessas informações:
1. Analise o comportamento financeiro do usuário
2. Identifique possíveis problemas ou oportunidades
3. Sugira até 3 ações práticas que o usuário pode aplicar imediatamente
4. Use linguagem simples e amigável

```

- Para os arquivos extensos em formato CSV, é utilizado Python para leitura e preparação dos dados antes de serem enviados ao modelo.

#### Exemplo de leitura de CSV (transações)

```python
import pandas as pd

# Carregar arquivo de transações
df_transacoes = pd.read_csv("transacoes.csv")

# Visualizar as primeiras linhas
print(df_transacoes.head())

# Converter para formato de lista de dicionários (mais fácil para o modelo usar)
transacoes = df_transacoes.to_dict(orient="records")

# Exemplo de uso: pegar últimas 5 transações
ultimas_transacoes = transacoes[-5:]

print(ultimas_transacoes)

```

O agente utiliza essas informações para:
- Personalizar respostas
- Evitar recomendações genéricas
- Tornar as orientações mais práticas e contextualizadas

---

## Exemplo de Contexto Montado

### Dados do Cliente:

- Nome: João Silva
- Idade: 32 anos  
- Profissão: Analista de Sistemas  
- Renda mensal: R$ 5.000  
- Perfil: Moderado  
- Objetivo principal: Construir reserva de emergência  
- Patrimônio total: R$ 15.000  
- Reserva de emergência atual: R$ 10.000  
- Aceita risco: Não  

### Metas:

- Completar reserva de emergência: R$ 15.000 até 06/2026  
- Entrada do apartamento: R$ 50.000 até 12/2027  

---

### Produtos Financeiros Disponíveis (exemplo):

- Tesouro Selic  
  - Risco: Baixo  
  - Rentabilidade: 100% da Selic  
  - Indicado para: Reserva de emergência e iniciantes  

- CDB Liquidez Diária  
  - Risco: Baixo  
  - Rentabilidade: 102% do CDI  
  - Indicado para: Segurança com rendimento diário  

- Fundo Multimercado  
  - Risco: Médio  
  - Indicado para: Perfil moderado que busca diversificação  

---

### Exemplo de Uso pelo Agente

Com base nesses dados, o agente pode:

- Identificar que o usuário ainda não completou a reserva de emergência  
- Priorizar recomendações de baixo risco  
- Sugerir produtos como Tesouro Selic ou CDB com liquidez diária  
- Alertar sobre gastos excessivos (caso identificado no CSV de transações)  
- Criar planos simples para atingir metas financeiras  

---

## Observações

- O agente sempre prioriza educação financeira antes de recomendação de produtos  
- As sugestões são baseadas no perfil e objetivos, mas não configuram recomendação profissional  
- Os dados utilizados são simulados (mockados) para fins de aprendizado e demonstração
