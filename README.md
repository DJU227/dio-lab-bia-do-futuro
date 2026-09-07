# 💰 Rota$ — Agente Financeiro Inteligente para Entregadores

## 📌 Contexto

O **Rota$** é um agente financeiro desenvolvido com **Inteligência Artificial Generativa** para auxiliar trabalhadores autônomos de plataformas de delivery, como iFood e 99, no controle de sua vida financeira.

Entregadores geralmente acompanham apenas o valor recebido pelas entregas, sem considerar adequadamente despesas como combustível, alimentação e manutenção do veículo. Isso dificulta a identificação do **lucro real** obtido durante a jornada de trabalho.

O Rota$ foi desenvolvido para transformar esses dados em informações financeiras simples e úteis.

### 🎯 Problema

Um entregador pode, por exemplo, faturar R$ 250 em um dia e considerar que esse foi seu ganho. Porém, após descontar combustível, alimentação e outros custos operacionais, o lucro efetivo pode ser significativamente menor.

O agente busca responder perguntas como:

* Quanto eu faturei?
* Quanto eu gastei?
* Quanto foi meu lucro?
* Quanto gastei com combustível?
* Qual é minha meta de lucro?
* Como estão meus gastos?
* Estou aumentando ou reduzindo meus custos?
* Qual é minha rentabilidade?

### 💡 Solução

O Rota$ combina **processamento de linguagem natural, dados estruturados e IA Generativa** para permitir que o entregador registre e consulte suas informações financeiras utilizando linguagem simples e natural.

Exemplo:

> **Usuário:** Hoje fiz R$ 280 em entregas.
>
> **Rota$:** Perfeito! Registrei R$ 280,00 de ganhos no dia de hoje.

Outro exemplo:

> **Usuário:** Gastei R$ 40 de combustível.
>
> **Rota$:** Registrado! Adicionei uma despesa de R$ 40,00 em combustível.

A partir desses registros, o sistema atualiza os cálculos financeiros e disponibiliza essas informações para consultas e análises.

---

# 🤖 Funcionalidades do Agente

O Rota$ possui as seguintes funcionalidades principais:

### 💰 Controle de ganhos

Permite registrar valores recebidos pelas entregas e acompanhar o faturamento acumulado.

### 💸 Controle de despesas

Permite registrar gastos relacionados à atividade profissional, incluindo:

* Combustível;
* Alimentação;
* Manutenção;
* Outras despesas.

### 📊 Cálculo de lucro

O agente calcula o lucro estimado considerando:

```text
Lucro = Faturamento - Despesas
```

### ⛽ Controle de combustível

Permite acompanhar os gastos com combustível e identificar seu impacto sobre o faturamento.

### 🔧 Controle de manutenção

Permite acompanhar despesas e reservas destinadas à manutenção do veículo utilizado para realizar as entregas.

### 🎯 Metas financeiras

O perfil do entregador possui metas financeiras que podem ser consultadas pelo agente.

Exemplo:

> "Qual é minha meta de lucro mensal?"

### 🧠 Análise com IA Generativa

Perguntas mais complexas são encaminhadas para o modelo de IA, que utiliza como contexto:

* Perfil do entregador;
* Histórico de transações;
* Histórico de atendimentos;
* Categorias financeiras;
* Indicadores financeiros;
* Regras de comportamento do agente.

---

# 👤 Público-Alvo

O público-alvo principal do Rota$ é formado por **trabalhadores autônomos de plataformas de delivery**, principalmente:

* Entregadores de motocicleta;
* Entregadores de carro;
* Trabalhadores que utilizam iFood;
* Trabalhadores que utilizam 99;
* Profissionais com renda variável;
* Pessoas que precisam acompanhar custos e lucro da atividade de entrega.

O sistema foi projetado para usuários que podem não possuir conhecimento aprofundado em educação financeira.

Por isso, o agente utiliza uma comunicação **simples, objetiva, prática e educativa**.

---

# 🧠 Persona do Agente

O agente possui o nome **Rota$**.

### Características

* **Personalidade:** consultiva e prática;
* **Tom:** informal, acessível e profissional;
* **Objetivo:** ajudar o entregador a compreender sua situação financeira;
* **Comunicação:** clara e direta;
* **Foco:** ganhos, despesas, lucro, metas e rentabilidade.

O agente não atua como banco e não fornece recomendações personalizadas de investimentos.

---

# 📚 Base de Conhecimento

Os dados utilizados pelo agente estão armazenados na pasta [`data/`](./data/).

| Arquivo                     | Formato | Utilização                                     |
| --------------------------- | ------- | ---------------------------------------------- |
| `transacoes.csv`            | CSV     | Histórico de ganhos e despesas                 |
| `historico_atendimento.csv` | CSV     | Histórico de atendimentos anteriores           |
| `perfil_investidor.json`    | JSON    | Perfil, características e metas do entregador  |
| `produtos_financeiros.json` | JSON    | Categorias de custos e indicadores financeiros |

Os arquivos utilizam dados mockados para permitir o desenvolvimento e a avaliação do agente sem utilização de informações financeiras reais.

📄 **Documentação:** [`docs/02-base-conhecimento.md`](./docs/02-base-conhecimento.md)

---

# 🏗️ Arquitetura da Aplicação

O projeto utiliza uma arquitetura simples composta por uma interface web, uma camada de processamento do agente e uma integração com IA Generativa.

```text
                    ┌──────────────────────┐
                    │      Usuário         │
                    │    Entregador        │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │     Streamlit        │
                    │       app.py         │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │       agente.py      │
                    │                      │
                    │ Processamento das    │
                    │ mensagens e regras   │
                    └───────┬───────┬──────┘
                            │       │
                 ┌──────────┘       └──────────┐
                 ▼                             ▼
        ┌──────────────────┐          ┌──────────────────┐
        │ Dados locais     │          │ Google Gemini    │
        │                  │          │                  │
        │ CSV / JSON       │          │ IA Generativa    │
        └──────────────────┘          └──────────────────┘
```

O processamento local é utilizado para operações simples e determinísticas, como consulta de faturamento, despesas e lucro.

Perguntas mais complexas são encaminhadas ao modelo Gemini utilizando os dados financeiros como contexto.

---

# 🔐 Segurança e Confiabilidade

Por se tratar de uma aplicação relacionada a informações financeiras, o Rota$ possui regras para reduzir respostas incorretas ou inventadas.

Entre as principais regras estão:

* Utilizar os dados fornecidos pela aplicação;
* Não inventar valores;
* Não inventar transações;
* Não inventar datas;
* Diferenciar dados registrados de estimativas;
* Não inventar horas trabalhadas;
* Só calcular lucro por hora quando existirem horas correspondentes;
* Não solicitar senhas ou credenciais;
* Não fornecer informações de outros usuários;
* Não fornecer recomendações personalizadas de investimentos.

A aplicação também utiliza consultas locais para cálculos financeiros básicos, reduzindo a dependência da IA para operações matemáticas determinísticas.

📄 **Documentação:** [`docs/03-prompts.md`](./docs/03-prompts.md)

---

# 📁 Estrutura do Projeto

```text
📁 Rota$/
│
├── 📄 README.md
│
├── 📁 data/                              # Dados utilizados pelo agente
│   ├── 📄 historico_atendimento.csv      # Histórico de atendimentos
│   ├── 📄 perfil_investidor.json         # Perfil do entregador
│   ├── 📄 produtos_financeiros.json      # Categorias e indicadores financeiros
│   └── 📄 transacoes.csv                 # Histórico de ganhos e despesas
│
├── 📁 docs/                              # Documentação do projeto
│   ├── 📄 01-caso-de-uso.md              # Caso de uso do agente
│   ├── 📄 02-base-conhecimento.md        # Base de conhecimento e dados
│   └── 📄 03-prompts.md                  # Engenharia de prompts
│
├── 📁 src/                               # Código-fonte da aplicação
│   ├── 📄 app.py                         # Interface web desenvolvida com Streamlit
│   ├── 📄 agente.py                      # Lógica e funcionamento do agente financeiro
│   ├── 📄 config.py                      # Configurações e integração com a API Gemini
│   └── 📄 requirements.txt               # Dependências do projeto
│
├── 📁 assets/                             # Imagens, diagramas e recursos visuais
│   └── ...
│
└── 📁 examples/                           # Exemplos de utilização
    └── 📄 README.md
```

---

# 📂 Descrição dos Diretórios

## `data/`

Armazena os dados utilizados pelo agente.

### `transacoes.csv`

Contém os registros financeiros do entregador, incluindo:

* Data;
* Descrição;
* Categoria;
* Valor;
* Tipo da movimentação.

As movimentações podem ser classificadas como:

```text
entrada
saida
```

### `historico_atendimento.csv`

Armazena exemplos de atendimentos anteriores para fornecer contexto ao agente.

### `perfil_investidor.json`

Apesar do nome original do arquivo, neste projeto ele representa o **perfil financeiro do entregador**.

São armazenadas informações como:

* Nome;
* Profissão;
* Veículo;
* Plataformas utilizadas;
* Renda média;
* Horas trabalhadas;
* Meta de lucro;
* Custo médio de combustível;
* Reserva para manutenção;
* Objetivos financeiros.

### `produtos_financeiros.json`

Neste projeto, o arquivo foi adaptado para representar **categorias de custos e indicadores financeiros relevantes para entregadores**.

---

# 💻 Código da Aplicação

A aplicação está localizada na pasta [`src/`](./src/).

### `app.py`

Responsável pela interface do Rota$ utilizando o framework Streamlit.

### `agente.py`

Responsável pela lógica principal do agente, incluindo:

* Leitura dos dados;
* Processamento das mensagens;
* Identificação de ganhos;
* Identificação de despesas;
* Registro de transações;
* Cálculos financeiros;
* Consultas locais;
* Montagem do contexto;
* Integração com o Gemini.

### `config.py`

Centraliza as configurações utilizadas pela aplicação, incluindo a chave da API e o modelo Gemini utilizado.

### `requirements.txt`

Contém as dependências necessárias para executar o projeto.

---

# ⚙️ Tecnologias Utilizadas

| Tecnologia           | Utilização                               |
| -------------------- | ---------------------------------------- |
| **Python**           | Linguagem principal                      |
| **Streamlit**        | Interface web                            |
| **Pandas**           | Manipulação dos dados financeiros        |
| **Google Gemini**    | Inteligência Artificial Generativa       |
| **Google GenAI SDK** | Integração com o Gemini                  |
| **JSON**             | Armazenamento de dados estruturados      |
| **CSV**              | Armazenamento das transações e histórico |
| **python-dotenv**    | Gerenciamento de variáveis de ambiente   |

---

# 🚀 Como Executar

## 1. Clonar o repositório

```bash
git clone <URL_DO_REPOSITORIO>
```

## 2. Acessar a pasta do projeto

```bash
cd "Rota$"
```

## 3. Criar o ambiente virtual

No Windows:

```powershell
python -m venv .venv
```

## 4. Ativar o ambiente virtual

```powershell
.venv\Scripts\Activate.ps1
```

## 5. Instalar as dependências

```powershell
pip install -r src\requirements.txt
```

## 6. Configurar a API Gemini

Crie um arquivo `.env` na raiz do projeto:

```env
GEMINI_API_KEY=sua_chave_do_gemini
```

> ⚠️ **Importante:** nunca publique sua chave da API no GitHub.

## 7. Executar a aplicação

```powershell
python -m streamlit run src\app.py
```

Após a execução, o Streamlit abrirá a aplicação no navegador.

---

# 🧪 Exemplos de Utilização

### Registrar um ganho

```text
Hoje fiz R$ 280 em entregas
```

O sistema registra automaticamente uma entrada de:

```text
Valor: R$ 280,00
Categoria: faturamento
Tipo: entrada
```

### Registrar combustível

```text
Gastei R$ 40 de combustível
```

O sistema registra:

```text
Valor: R$ 40,00
Categoria: combustível
Tipo: saída
```

### Consultar o lucro

```text
Quanto lucrei?
```

O agente calcula:

```text
Lucro = Faturamento - Despesas
```

### Consultar uma meta

```text
Qual é minha meta de lucro?
```

O agente consulta o perfil financeiro do entregador.

### Pergunta analítica

```text
Como estão meus gastos com combustível?
```

Nesse tipo de consulta, o agente pode utilizar os dados financeiros disponíveis para produzir uma análise contextualizada.

---

# 📊 Fluxo Financeiro

O funcionamento principal do Rota$ pode ser representado pelo seguinte fluxo:

```text
Ganhos
   │
   ▼
Despesas
   │
   ▼
Lucro
   │
   ▼
Rentabilidade
   │
   ▼
Metas
   │
   ▼
Recomendações e análises da IA
```

O objetivo é transformar registros financeiros simples em informações que auxiliem o entregador na tomada de decisões sobre sua atividade profissional.

---

# 📈 Avaliação e Métricas

A qualidade do agente pode ser avaliada considerando:

* **Precisão dos cálculos financeiros;**
* **Assertividade das respostas;**
* **Consistência com os dados armazenados;**
* **Taxa de respostas sem informações inventadas;**
* **Coerência com o perfil do entregador;**
* **Capacidade de identificar corretamente ganhos e despesas;**
* **Qualidade das análises geradas pela IA.**

📄 **Documentação:** [`docs/04-metricas.md`](./docs/04-metricas.md)

---

# 🎤 Pitch

O Rota$ pode ser apresentado como uma solução que utiliza Inteligência Artificial para transformar o controle financeiro de entregadores.

A proposta central é simples:

> **O entregador registra seus ganhos e gastos em linguagem natural, e o Rota$ transforma essas informações em uma visão clara do seu lucro e da sua situação financeira.**

📄 **Roteiro do pitch:** [`docs/05-pitch.md`](./docs/05-pitch.md)

---

# 🎯 Objetivo do Projeto

O principal objetivo do Rota$ é **facilitar o controle financeiro de trabalhadores de delivery**, permitindo que eles compreendam não apenas quanto faturam, mas principalmente **quanto realmente lucram após os custos da atividade**.

A aplicação busca aproximar conceitos de educação financeira da rotina do entregador por meio de uma interface conversacional simples e acessível.

---

# 📌 Dicas para Utilização

1. **Registre seus ganhos** sempre que possível.
2. **Registre todas as despesas** relacionadas ao trabalho.
3. **Acompanhe o lucro**, e não apenas o faturamento.
4. **Monitore o combustível**, pois representa um dos principais custos operacionais.
5. **Reserve valores para manutenção** do veículo.
6. **Defina metas financeiras** e acompanhe sua evolução.
7. **Utilize a IA para análises**, mas considere sempre os dados registrados como base das informações.
8. **Não compartilhe chaves de API ou credenciais** no repositório.

---

## 👨‍💻 Projeto

**Rota$ — Agente Financeiro Inteligente para Entregadores**

Projeto acadêmico desenvolvido com Python, Streamlit, Pandas e Google Gemini, com foco na aplicação prática de **IA Generativa, processamento de dados e educação financeira**.
