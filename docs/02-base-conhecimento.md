# Base de Conhecimento

## Dados Utilizados

Descreva se usou os arquivos da pasta `data`, por exemplo:

| Arquivo | Formato | Utilização no Agente |
|---------|---------|---------------------|
| `historico_atendimento.csv` | CSV | Contextualizar interações anteriores do entregador com o agente e identificar dúvidas ou objetivos já discutidos. |
| `perfil_investidor.json` | JSON | Armazenar o perfil financeiro e profissional do entregador, incluindo veículo, plataformas utilizadas, renda média e metas financeiras. |
| `produtos_financeiros.json` | JSON | Armazenar categorias de custos, indicadores financeiros e regras utilizadas nas análises do agente. |
| `transacoes.csv` | CSV | Registrar e analisar faturamentos e despesas relacionadas ao trabalho, como combustível, alimentação e manutenção. |

> [!TIP]
> **Quer um dataset mais robusto?** Você pode utilizar datasets públicos do [Hugging Face](https://huggingface.co/datasets) relacionados a finanças, desde que sejam adequados ao contexto do desafio.

---

## Adaptações nos Dados

> Você modificou ou expandiu os dados mockados? Descreva aqui.

Os dados mockados originais foram adaptados para atender ao caso de uso do agente Rota$, destinado a trabalhadores de plataformas de delivery.

O arquivo perfil_investidor.json, originalmente destinado ao perfil de investimento de um cliente bancário, passou a representar o perfil financeiro e profissional do entregador. Foram incluídas informações como tipo de veículo utilizado, plataformas de delivery, horas trabalhadas, renda média, gastos com combustível e metas de lucro.

O arquivo produtos_financeiros.json também foi modificado. Como o agente não tem como objetivo recomendar investimentos ou produtos bancários, o arquivo passou a armazenar categorias de custos e indicadores relevantes para a atividade do entregador, como combustível, manutenção, lucro por hora e metas financeiras.

O arquivo transacoes.csv foi adaptado para registrar receitas provenientes das plataformas de delivery e despesas diretamente relacionadas à atividade profissional.

Já o arquivo historico_atendimento.csv passou a registrar interações anteriores relacionadas a temas como lucro diário, metas, combustível, manutenção e rentabilidade.

Essas adaptações permitem que a base de conhecimento esteja diretamente relacionada ao problema financeiro tratado pelo agente.

---

## Estratégia de Integração

### Como os dados são carregados?
> Descreva como seu agente acessa a base de conhecimento.

Os arquivos CSV e JSON presentes na pasta data/ são carregados pela aplicação no início da execução do agente.

Os arquivos CSV são interpretados utilizando uma biblioteca de manipulação de dados, como Pandas, enquanto os arquivos JSON são convertidos para estruturas de dados utilizadas internamente pela aplicação.

Após o carregamento, os dados ficam disponíveis para consulta durante as interações do usuário com o agente.

Quando o usuário realiza uma pergunta, o sistema identifica quais informações são necessárias, consulta os dados correspondentes e monta um contexto específico para o modelo de linguagem.

Dessa forma, não é necessário enviar toda a base de conhecimento ao modelo em todas as interações.

### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?

Os dados são utilizados de forma dinâmica.

O prompt principal contém as regras gerais de comportamento do agente, como sua função, limitações e orientações de segurança.

As informações financeiras do entregador são adicionadas ao contexto apenas quando forem necessárias para responder à pergunta realizada.

Por exemplo, caso o usuário pergunte:

Quanto eu lucrei esta semana?

O sistema consulta o arquivo transacoes.csv, soma as entradas referentes ao faturamento, subtrai as despesas registradas e fornece ao modelo apenas o resultado necessário para elaborar a resposta.

Sempre que possível, cálculos matemáticos são realizados pela própria aplicação antes do envio dos dados ao LLM, reduzindo o risco de erros e alucinações.

O modelo de linguagem fica principalmente responsável por interpretar a intenção do usuário e transformar os resultados obtidos em uma resposta clara e compreensível.

---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.

Dados do Entregador: 
Nome: Carlos Oliveira 
Profissão: Entregador de aplicativo Veículo: Motocicleta 
Plataformas: iFood e 99 
Meta de lucro mensal: R$ 3.500,00 
Média de renda mensal: R$ 4.200,00 
Custos médios: 
- Combustível: R$ 850,00/mês
- Reserva para manutenção: R$ 250,00/mês 
- Últimas transações: 01/08/2026: - Entregas iFood: +R$ 215,00 - Combustível: -R$ 42,00 - Alimentação: -R$ 25,00 02/08/2026: - Entregas 99: +R$ 185,00 - Combustível: -R$ 38,00
  
-  03/08/2026: - Entregas iFood: +R$ 260,00 - Combustível: -R$ 45,00 - Manutenção: -R$ 80,00
Indicadores calculados: - Faturamento no período: R$ 660,00
- Despesas no período: R$ 230,00
- Lucro líquido estimado: R$ 430,00
Instrução ao agente: Responda utilizando exclusivamente os dados apresentados. Não invente valores ausentes. Caso não existam informações suficientes para realizar uma análise, informe ao usuário quais dados são necessários.
