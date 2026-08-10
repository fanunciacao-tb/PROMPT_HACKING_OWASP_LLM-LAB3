# 🛡️ LAB 03: Sensitive Information Disclosure & System Prompt Leakage (OWASP LLM02 / OWASP LLM06)

Este repositório contém o laboratório prático de cibersegurança em Inteligência Artificial focado em **Vazamento de Informações Sensíveis (OWASP LLM06)**, exploração de **System Prompt Leakage** e implementação de **Guardrails Defensivos de Filtro de Dados (Data Leakage Guardrails)**.

---
## 🎯 Objetivo do Laboratório
Demonstrar na prática como a inclusão de segredos de negócio, chaves de API e dados pessoais (PII) no contexto de uma LLM pode ser explorada via engenharia de prompt para vazar dados confidenciais, e como construir filtros no backend Python para mascarar e bloquear esse vazamento.
---
## 🧪 Estrutura da Atividade

### 🔴 Red Team (Ataque)
* **Conceito:** Exploração da vulnerabilidade **OWASP LLM06**, aplicando técnicas de *System Prompt Leakage* e *Roleplay Ingestion* para forçar o modelo a revelar instruções confidenciais, chaves de API e dados sensíveis de clientes.
* **Desafio:** Utilizar táticas de bypass para extrair a chave secreta do sistema (`SEC_KEY_9988`) e o código de autorização do gerente mantidos no prompt do assistente.

### 🔵 Blue Team (Defesa)
* **Conceito:** Aplicação de *Data Sanitization Guardrails* e inspeção de saída por Expressões Regulares (Regex).
* **Solução:** Construção de um pipeline defensivo que inspeciona a resposta da LLM em tempo real e mascara automaticamente chaves de API, CPFs e códigos de autorização sensíveis antes de entregar a resposta ao usuário.
---
## 🚀 Como Executar no Google Colab

1. Acesse o notebook do laboratório clicando em [`SENSITIVE_INFO_DISCLOSURE.ipynb`](./SENSITIVE_INFO_DISCLOSURE.ipynb) ou abra diretamente pelo Google Colab.
2. Certifique-se de ativar a GPU T4:
   * Menu: `Ambiente de Execução` ➔ `Alterar tipo de ambiente de execução` ➔ `Acelerador de Hardware: GPU T4`.
3. Execute as células em sequência para carregar o modelo `TinyLlama/TinyLlama-1.1B-Chat-v1.0`.
4. Faça as missões práticas de **Red Team** e **Blue Team** indicadas no notebook.
---
## 🧰 Tecnologias Utilizadas
* **Ambiente:** Google Colab (GPU T4)
* **Linguagem:** Python 3.10+
* **Frameworks:** Hugging Face `transformers`, `torch`, `re` (Regular Expressions)
* **Modelo LLM:** `TinyLlama/TinyLlama-1.1B-Chat-v1.0`
