# Assistente de Investimentos Automatizado com RPA e IA Generativa

Projeto desenvolvido como desafio prático para a trilha de automação inteligente da **DIO (Digital Innovation One)**.

## 🚀 Tecnologias Utilizadas
- **Python + BeautifulSoup**: Automação de extração de dados (RPA) da tabela web de clientes.
- **N8N**: Orquestrador do pipeline de dados e execução lógica de ponta a ponta.
- **JavaScript (Node.js)**: Higienização e padronização dos saldos bancários dos investidores.
- **Google Gemini API (Model 3.8 Flash)**: IA Generativa integrada via Agente para criar recomendações personalizadas, amigáveis e exclusivas por perfil.

## 🧠 Arquitetura do Workflow
1. **Script Python** realiza a raspagem de dados de clientes e faz um disparo **HTTP POST** para o N8N.
2. O **Webhook** do N8N recebe a carga de dados e o **Split Out** separa em 10 itens únicos.
3. O node de **Código JS** trata as informações financeiras.
4. O node **Switch** segmenta as ações por perfil (Conservador, Moderado e Arrojado).
5. O **AI Agent** interpreta os dados do cliente e a recomendação estática para redigir o e-mail consultivo final de forma humanizada.

