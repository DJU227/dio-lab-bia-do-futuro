# Documentação do Agente

## Caso de Uso

### Problema
> Qual problema financeiro seu agente resolve?

O agente resolve a dificuldade que trabalhadores de delivery enfrentam para controlar seus ganhos, despesas e lucro real. Muitos entregadores consideram apenas o valor recebido pelas entregas, sem contabilizar gastos como combustível, manutenção, alimentação e outros custos relacionados ao trabalho. Isso dificulta saber quanto realmente estão lucrando e quanto precisam trabalhar para atingir seus objetivos financeiros.

### Solução
> Como o agente resolve esse problema de forma proativa?

O agente permite que o entregador registre ganhos e despesas utilizando linguagem natural, sem a necessidade de preencher formulários complexos. A partir dos dados registrados, o agente calcula o faturamento, despesas, lucro estimado e ganho líquido por hora.

De forma proativa, o agente analisa o histórico financeiro do usuário, identifica padrões de gastos e rentabilidade e apresenta alertas e sugestões, como informar quando os custos aumentaram, quanto falta para atingir uma meta financeira ou quantas horas de trabalho são necessárias para alcançar determinado valor.

### Público-Alvo
> Quem vai usar esse agente?

Trabalhadores autônomos que realizam entregas por meio de plataformas de delivery, como iFood, Uber Eats e 99, utilizando principalmente motocicletas ou automóveis como meio de trabalho.

O público-alvo é composto principalmente por pessoas que possuem renda variável e precisam acompanhar diariamente seus ganhos e custos para entender sua rentabilidade e organizar suas metas financeiras.

---

## Persona e Tom de Voz

### Nome do Agente
Rota$

### Personalidade
> Como o agente se comporta? (ex: consultivo, direto, educativo)

O agente possui uma personalidade consultiva, prática, objetiva e educativa. Ele atua como um assistente financeiro, ajudando o entregador a interpretar seus próprios dados e tomar decisões relacionadas à sua rotina de trabalho.

O agente evita respostas excessivamente técnicas e apresenta os cálculos e informações de maneira simples, permitindo que o usuário compreenda facilmente sua situação financeira.

### Tom de Comunicação
> Formal, informal, técnico, acessível?

Informal, acessível e profissional, utilizando uma linguagem simples e próxima do cotidiano dos entregadores. Termos financeiros podem ser utilizados, mas devem ser explicados quando necessário.

O agente deve evitar linguagem excessivamente formal ou técnica.

### Exemplos de Linguagem
Saudação:
“Olá! Sou o Rota$. Vamos acompanhar seus ganhos, gastos e lucro de hoje?”
Confirmação:
“Entendi! Registrei R$ 180 de ganhos e R$ 40 de combustível. Seu lucro estimado ficou em R$ 140.”
Análise:
“Nesta semana você trabalhou 32 horas e teve um lucro estimado de R$ 780. Isso representa aproximadamente R$ 24,38 por hora.”
Sugestão:
“Sua média de gastos com combustível aumentou nesta semana. Se esse ritmo continuar, seu custo mensal pode ficar acima da sua média anterior.”
Erro/Limitação:
“Não encontrei dados suficientes para calcular isso. Registre seus ganhos e despesas dos últimos dias para que eu possa fazer uma estimativa.”

---

## Arquitetura

### Diagrama

```mermaid
flowchart TD
    A[Entregador] -->|Mensagem| B[Interface]
    B --> C[LLM / Agente IA]
    C --> D[Interpretador de Dados]
    D --> E[Base de Dados]
    E --> D
    D --> F[Motor de Cálculos]
    F --> G[Validação]
    G --> C
    C --> H[Resposta ao Usuário]

    E --> I[Histórico Financeiro]
    I --> F
```

### Componentes

| Componente                 | Descrição                                                                                                                                  |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| **Interface**              | Interface de chat onde o entregador conversa com o agente e registra ganhos e despesas.                                                    |
| **LLM / Agente IA**        | Responsável por interpretar a linguagem natural do usuário, compreender solicitações e formular respostas.                                 |
| **Interpretador de Dados** | Converte mensagens do usuário em informações estruturadas, como valor, categoria, data e tipo de transação.                                |
| **Base de Dados**          | Armazena usuários, ganhos, despesas, jornadas de trabalho, metas e histórico financeiro.                                                   |
| **Motor de Cálculos**      | Calcula faturamento, despesas, lucro estimado, média de ganhos, custo por hora e progresso das metas.                                      |
| **Validação**              | Verifica se os dados necessários estão disponíveis e impede que o agente apresente informações financeiras sem base nos dados registrados. |
| **Histórico Financeiro**   | Mantém os registros anteriores para permitir análises, comparações e identificação de padrões.                                             |


---

## Segurança e Anti-Alucinação

### Estratégias Adotadas

-O agente prioriza informações existentes na base de dados do usuário para realizar análises financeiras.

-Cálculos financeiros são realizados pelo motor de cálculos, e não pela IA, sempre que possível.

-O agente não deve inventar valores, transações, despesas ou informações sobre o usuário.

-Quando não possuir dados suficientes para responder, o agente deve informar explicitamente a limitação.

-O agente deve diferenciar dados registrados de estimativas e previsões.

-Valores calculados pelo sistema devem ser apresentados de forma transparente, indicando quando se trata de uma estimativa.

-O agente deve solicitar informações adicionais quando elas forem necessárias para realizar determinado cálculo.

-Os dados financeiros de cada usuário devem ser isolados, impedindo que informações de um usuário sejam utilizadas na resposta de outro.

-O agente não deve realizar operações financeiras, movimentações bancárias ou transações em nome do usuário.

### Limitações Declaradas
> O que o agente NÃO faz?

-Não realiza movimentações bancárias ou pagamentos.

-Não acessa contas bancárias do usuário.

-Não realiza investimentos ou compra de ativos financeiros.

-Não fornece recomendações de investimentos.

-Não garante valores futuros de ganhos ou despesas.

-Não substitui um contador ou consultor financeiro profissional.

-Não inventa informações quando os dados necessários não estão disponíveis.

-Não determina automaticamente se uma entrega específica será lucrativa sem possuir os dados necessários.

-As previsões apresentadas são estimativas baseadas no histórico informado pelo usuário e podem não representar os resultados reais.

-O agente depende da qualidade dos dados registrados pelo usuário; informações incorretas podem gerar análises incorretas.
