# 🤖 Assistente de Investimentos Automatizado com RPA e IA Generativa

> Desafio de projeto prático desenvolvido para a trilha de automação inteligente da **DIO (Digital Innovation One)**.

## 🎯 Objetivo do Projeto
Desenvolver um pipeline inteligente de automação que realiza o web scraping de dados de clientes, processa e padroniza as informações financeiras, cruza perfis de investidores e utiliza Inteligência Artificial Generativa para criar e-mails consultivos altamente personalizados.

---

## 🧠 Arquitetura do Workflow Integrado

<img width="1828" height="850" alt="▶️ Assistente de Investimentos - RPA + IA - n8n (6)" src="https://github.com/user-attachments/assets/f128deda-dd73-438a-b619-6efc622b0b16" />

### 📋 Mapeamento Estrutural do Fluxo (Pipeline de Execução)

Abaixo está o mapa lógico de como as informações nascem na web, passam pela esteira de automação e chegam até a camada de Inteligência Artificial:

```text
  [ WEB PAGE ] ➔ Raspagem de Dados HTML com BeautifulSoup (RPA em Python)
        │
        ▼ (Requisição HTTP POST)
  [ WEBHOOK ] ➔ Node de Entrada que escuta e captura a lista de clientes
        │
        ▼ (Payload JSON)
  [ SPLIT OUT ] ➔ Quebra do array de clientes em 10 itens individuais
        │
        ▼ (Iteração Individual)
  [ CODE (JS) ] ➔ Limpeza e higienização dos saldos (conversão de String para Number)
        │
        ▼ (Dados Higienizados)
  [ SWITCH ] ➔ Roteamento condicional baseado no Perfil de Risco
        │
        ├─➔ [ EDIT FIELDS ] (Conservador) ─┐
        ├─➔ [ EDIT FIELDS ] (Moderado)    ─┼─➔ Contexto Técnico Acoplado
        └─➔ [ EDIT FIELDS ] (Arrojado)    ─┘
                                │
                                ▼
                       [ AI AGENT (Gemini) ] ➔ Engenharia de Prompt e Geração
                                │             do e-mail personalizado humanizado
                                ▼
                       [ MENSAGEM FINAL ] ➔ Output Consultivo de Alta Performance
```

### 🔍 Detalhamento das Etapas:
1. **RPA de Extração (Python):** O script acessa a página web simulada da DIO, extrai a tabela de usuários via `BeautifulSoup` e envia os dados consolidados via requisição HTTP POST para o N8N.
2. **Gatilho de Entrada (Webhook):** O **node** de entrada do N8N escuta a porta e recebe o payload JSON contendo a lista completa de clientes.
3. **Divisão de Lotes (Split Out):** Quebra o array principal de clientes em 10 itens individuais para garantir o processamento sequencial e personalizado de cada carteira.
4. **Higienização de Dados (JavaScript):** Remove caracteres de moedas, formatações regionais e converte as strings financeiras de saldo em dados numéricos puros para manipulação lógica dentro do **node**.
5. **Roteamento Condicional (Switch):** Filtra e separa os clientes dinamicamente conforme seus perfis de investimento declarados (`Conservador`, `Moderado` ou `Arrojado`).
6. **Mapeamento Estático (Edit Fields):** Cria a base contextual de recomendações técnicas iniciais para cada perfil mapeado (MVP).
7. **Camada de IA Generativa (AI Agent):** Consome os dados e o contexto gerado nas etapas anteriores. Conectado ao **node** do modelo **Gemini 3.8 Flash**, o agente redige mensagens ricas, personalizadas e humanas para o cliente final.

---

## 🚀 Tecnologias Utilizadas
*   **Python 3 & BeautifulSoup4:** Responsáveis pelo script estruturado de Web Scraping (RPA).
*   **N8N (Self-Hosted):** Motor de orquestração de workflows e integração de sistemas baseada em **nodes**.
*   **JavaScript (Node.js):** Manipulação, limpeza avançada e transformação de tipos de dados.
*   **Google Gemini API (Model 3.8 Flash):** Motor de IA Generativa encarregado da redação das mensagens consultivas premium com tratamento automatizado de cotas de requisição (*Execute Once*).

---

## 📁 Estrutura Atualizada do Repositório
```text
📁 dio-lab-assistente-investimentos-rpa-n8n/
├── 📄 README.md              # Documentação principal do projeto
├── 📁 rpa/
│   └── 📄 extrair_clientes.ipynb # Script Jupyter Notebook de extração RPA
└── 📁 n8n/
    └── 📄 workflow.json      # Arquivo JSON exportado do fluxo completo N8N
```

---

## 🛠️ Como Executar este Projeto

### 1. Preparação no N8N
* Importe o arquivo `n8n/workflow.json` para dentro do seu painel do N8N.
* Configure uma credencial válida com a sua API Key gratuita gerada no [Google AI Studio](https://google.com) dentro do **node** de modelo do Gemini.
* Defina a entrada do **node** *AI Agent* para o modo **Define Below** e mude o modelo interno para `gemini-3.8-flash`.
* Ative/Publique o workflow para que o Webhook de testes fique ativo aguardando dados.

### 2. Execução do Script RPA
* Abra o arquivo `rpa/extrair_clientes.ipynb` no Google Colab ou ambiente local.
* Substitua a variável `N8N_WEBHOOK` com a URL exata do Webhook gerado pelo seu painel do N8N.
* Execute a célula principal. O script irá raspar os dados e disparar o fluxo de automação automaticamente.


