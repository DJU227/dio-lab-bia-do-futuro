# Código da Aplicação

Esta pasta contém o código-fonte do agente financeiro **Rota$**, desenvolvido para auxiliar trabalhadores de plataformas de delivery no controle de ganhos, despesas e lucro.

## Estrutura do Projeto

```text
src/
├── app.py              # Aplicação principal (Streamlit)
├── agente.py           # Lógica e funcionamento do agente
├── config.py           # Configurações da aplicação e API
└── requirements.txt    # Dependências do projeto
```

## Dependências

As principais bibliotecas utilizadas pela aplicação são:

```text
streamlit
google-genai
python-dotenv
pandas
```

As dependências também estão disponíveis no arquivo `requirements.txt`.

## Como Instalar

Na raiz do projeto, execute:

```bash
pip install -r src/requirements.txt
```

## Configuração da API

Crie um arquivo `.env` na raiz do projeto:

```env
GEMINI_API_KEY=sua_chave_do_gemini
```

A chave da API não deve ser publicada no GitHub.

## Como Rodar

Na raiz do projeto, execute:

```bash
python -m streamlit run src/app.py
```

Após a execução, o Streamlit disponibilizará a aplicação no navegador.

## Funcionalidades

O agente **Rota$** permite:

* Registrar ganhos de entregas;
* Registrar despesas;
* Categorizar gastos;
* Calcular faturamento;
* Calcular despesas;
* Calcular lucro estimado;
* Consultar gastos com combustível;
* Consultar gastos com alimentação;
* Consultar gastos com manutenção;
* Acompanhar metas financeiras;
* Responder perguntas financeiras utilizando inteligência artificial;
* Utilizar dados históricos e perfil financeiro do entregador como contexto para a IA.
