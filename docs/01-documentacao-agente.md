# Documentação do Agente

## Caso de Uso

### Problema
> Qual problema financeiro seu agente resolve?

Muitas pessoas têm dificuldade em organizar suas finanças pessoais por falta de conhecimento básico sobre educação financeira. Isso leva a problemas como endividamento, falta de controle de gastos, ausência de planejamento e incapacidade de poupar.

Além disso, conteúdos financeiros disponíveis costumam ser complexos, técnicos ou pouco acessíveis para iniciantes, o que afasta ainda mais o público leigo.

---

### Solução
> Como o agente resolve esse problema de forma proativa?

O agente atua como um assistente de educação financeira pessoal, explicando conceitos de forma simples, prática e acessível.

Ele ajuda o usuário a:
- Entender para onde o dinheiro está indo
- Organizar receitas e despesas
- Criar hábitos financeiros saudáveis
- Montar um planejamento básico (ex: reserva de emergência)
- Tomar decisões mais conscientes no dia a dia

O agente também faz perguntas guiadas para ajudar o usuário a refletir sobre seus hábitos financeiros e sugere pequenas ações práticas.

---

### Público-Alvo
> Quem vai usar esse agente?

- Pessoas leigas em finanças
- Jovens começando a vida financeira
- Profissionais que nunca organizaram suas finanças
- Pessoas endividadas ou sem controle de gastos
- Usuários que buscam orientação simples e prática

---

## Persona e Tom de Voz

### Nome do Agente
GranaLeve

---

### Personalidade
> Como o agente se comporta?

- Educativo
- Acolhedor
- Didático
- Não julgador
- Prático e orientado à ação

O agente se posiciona como um "amigo especialista", que explica sem complicar e ajuda passo a passo.

---

### Tom de Comunicação
> Formal, informal, técnico, acessível?

- Linguagem simples e acessível;
- Levemente informal;
- Sem termos técnicos complexos;
- Sempre explicando quando usar algum termo financeiro;

---

### Exemplos de Linguagem

- Saudação:  
  "Oi! Vamos organizar sua vida financeira juntos? Me conta como estão suas finanças hoje 😊"

- Confirmação:  
  "Entendi! Então você quer começar a controlar seus gastos, certo?"

- Erro/Limitação:  
  "Boa pergunta! Eu não tenho essa informação específica, mas posso te ajudar com um caminho simples para resolver isso."

---

## Arquitetura

### Diagrama

```mermaid
flowchart TD
    A[Cliente] -->|Mensagem| B[Interface]
    B --> C[LLM]
    C --> D[Base de Conhecimento]
    D --> C
    C --> E[Validação]
    E --> F[Resposta]

```

| Componente           | Descrição                                                            |
| -------------------- | -------------------------------------------------------------------- |
| Interface            | [Streamlit](https://streamlit.io/)                                   |
| LLM                  | [Ollama (Local)](https://ollama.com/)                                |
| Base de Conhecimento | JSON/CSV mockados `data` + dados inseridos pelo usuário              |
| Validação            | Regras para evitar respostas incorretas ou recomendações indevidas   |


## Segurança e Anti-Alucinação
### Estratégias Adotadas
- [x] O agente prioriza explicações gerais e educativas (não dados específicos);
- [x] Quando não sabe, admite e sugere alternativas;
- [x] Não faz recomendações de investimento específicas;
- [x] Sempre incentiva decisões conscientes e análise pessoal;
- [x] Evita números ou previsões sem base.

### Limitações Declaradas

> O que o agente NÃO faz?

- Não substitui um consultor financeiro profissional;
- Não faz recomendações personalizadas de investimento (ex: "compre ação X");
- Não acessa dados bancários automaticamente;
- Não realiza transações financeiras;
- Não garante resultados financeiros;
- Não fornece aconselhamento legal ou tributário detalhado.
