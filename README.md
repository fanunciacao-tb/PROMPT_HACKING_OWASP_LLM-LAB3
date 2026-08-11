# 🛡️ LAB3 — OWASP LLM02_SENSITIVE INFORMATION DISCLOSURE & LLM07_SYSTEM PROMPT LEAKAGE

Este repositório contém o laboratório prático de cibersegurança em Inteligência Artificial focado na vulnerabilidade de **Vazamento de Informações Sensíveis (Sensitive Information Disclosure)** e na mitigação de ataques de **Prompt Leakage**, utilizando barreiras defensivas baseadas em expressões regulares (*Output Guardrails & Regex*).

---

## 🎯 Objetivo do Laboratório

Demonstrar na prática como a vulnerabilidade **OWASP LLM02 (Sensitive Information Disclosure)** e o vazamento de instruções de sistema permitem a extração não autorizada de dados confidenciais (chaves de API, regras internas e PII) embutidos no contexto de uma LLM, e como implementar barreiras defensivas robustas no backend Python para neutralizar esse risco antes que a informação atinja o usuário final.

* **Modelo Utilizado:** Qwen 2.5 (0.5B Instruct) (`Qwen/Qwen2.5-0.5B-Instruct`)
* **Ambiente de Execução:** GitHub Codespaces (Otimizado para CPU)
* **Vulnerabilidades Alvo:** 
  * OWASP LLM02: Sensitive Information Disclosure
  * System Prompt Leakage

---

## 🧪 Estrutura da Atividade

### 🔴 Red Team (Ataque)
* **Conceito:** Exploração de falhas onde o assistente virtual é manipulado para ignorar restrições textuais de sigilo inseridas no *System Prompt* e vazar credenciais corporativas e dados de clientes (PII).
* **Vetores de Teste:** Extração direta por engenharia social (*roleplay* de auditor), manipulação de formato (conversão para JSON) e solicitação direta de CPFs e saldos.

### 🔵 Blue Team (Defesa)
* **Conceito:** Aplicação de uma estratégia de **Inspeção de Saída e Filtragem Programática (Output Guardrails & Regex)**.
* **Solução:** Desenvolvimento de um filtro defensivo no backend Python utilizando a biblioteca `re` (`re.sub`) para interceptar, mascarar e bloquear chaves, códigos gerenciais e documentos pessoais.

---

## 📋 Detalhamento das Atividades Práticas

### Módulo Red Team (Ataques de Prompt Leakage)
* **Atividade A:** Ataque via *Roleplay* / Engenharia Social de Desenvolvedor.
* **Atividade B:** Ataque via Tradução / Reformaturação de Dados (JSON).
* **Atividade C:** Ataque de Extração de PII / CPF.

### Módulo Blue Team (Defesa & Guardrails)
* **Atividade D:** Implementação do Guardrail Regex (`guardrail_dados_sensiveis`).
* **Atividade E:** Teste de defesa contra extração de chaves e dados gerenciais.
* **Atividade F:** Teste de defesa contra extração de dados pessoais (PII/CPF).

---

## 🚀 Como Executar
1. Abra este repositório no **GitHub Codespaces**.
2. Crie um novo notebook Jupyter chamado `IA_SENSITIVE_INFORMATION.ipynb`.
3. Siga o passo a passo para carregar o modelo Qwen 0.5B e testar os cenários de Red Team e Blue Team.

---

> **Lição Principal:** *"Nunca confie que instruções puramente em linguagem natural no System Prompt manterão segredos a salvo! Dados de infraestrutura, senhas e PII jamais devem ser expostos sem proteções ativas. Sempre implemente Guardrails de inspeção de saída para blindar o backend da sua aplicação!"*
