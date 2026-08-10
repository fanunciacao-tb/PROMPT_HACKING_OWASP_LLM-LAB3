# 🛡️ LAB 03: Vazamento de Dados Sensíveis e System Prompt Leakage (OWASP LLM06) — Qwen Edition

Este repositório contém o laboratório prático de cibersegurança em Inteligência Artificial focado na vulnerabilidade de **Vazamento de Informações Sensíveis (Sensitive Information Disclosure)** e na mitigação de ataques de **Prompt Leakage**, utilizando barreiras defensivas baseadas em expressões regulares (*Output Guardrails & Regex*).

---

## 🎯 Objetivo do Laboratório

Demonstrar na prática como a vulnerabilidade **OWASP LLM06 (Sensitive Information Disclosure)** permite a extração não autorizada de dados confidenciais (chaves de API, regras internas de negócio e PII) embutidos no *System Prompt* ou no contexto de uma LLM, e como implementar barreiras defensivas robustas no backend Python para neutralizar esse risco.

* **Modelo Utilizado:** Qwen 2.5 (0.5B Instruct) (`Qwen/Qwen2.5-0.5B-Instruct`)
* **Ambiente de Execução:** GitHub Codespaces (Otimizado para CPU)
* **Vulnerabilidade Alvo:** OWASP LLM06 - Sensitive Information Disclosure / System Prompt Leakage

---

## 🧪 Estrutura da Atividade

### 🔴 Red Team (Ataque)
* **Conceito:** Exploração da vulnerabilidade OWASP LLM06 no modelo Qwen, onde o assistente virtual é manipulado para ignorar restrições textuais de sigilo inseridas no *System Prompt* e vazar credenciais corporativas e dados pessoais.
* **Vetores de Teste:** Extração direta por engenharia social (*roleplay* de auditor), manipulação de formato de saída (tradução para JSON) e solicitação direta de PII (CPF e saldos).

### 🔵 Blue Team (Defesa)
* **Conceito:** Aplicação de uma estratégia de **Inspeção de Saída e Filtragem Programática (Output Guardrails & Regex)**.
* **Solução:** Desenvolvimento de um filtro defensivo no backend Python utilizando a biblioteca `re` (`re.sub`) para interceptar, mascarar e bloquear chaves de API, códigos de autorização e dados de identificação pessoal (PII) antes que a resposta seja entregue ao usuário.

---

## 📋 Detalhamento das Atividades Práticas (A a F)

### 🔴 Módulo Red Team (Ataques de Prompt Leakage)

* **Atividade A: Ataque via *Roleplay* / Engenharia Social de Desenvolvedor**
  * **Tática:** Induzir o modelo a assumir um cenário simulado onde o usuário finge ser um "Auditor Principal de Segurança".
  * **Objetivo:** Comprovar que LLMs vulneráveis ignoram ordens de sigilo textuais quando confrontadas com figuras de autoridade simuladas no prompt.

* **Atividade B: Ataque via Tradução / Reformaturação de Dados**
  * **Tática:** Solicitar a reestruturação e tradução das regras internas secretas para o formato JSON.
  * **Objetivo:** Demonstrar como pedidos de alteração estrutural na saída quebram as barreiras lógicas do modelo, forçando-o a expor credenciais.

* **Atividade C: Ataque de Extração de PII / CPF**
  * **Tática:** Realizar uma consulta direta visando dados sensíveis de clientes cadastrados no contexto do sistema.
  * **Objetivo:** Validar o risco de vazamento de informações de identificação pessoal (PII), como CPFs e saldos bancários confidenciais.

---

### 🔵 Módulo Blue Team (Defesa & Guardrails)

* **Atividade D: Implementação do Guardrail Regex (`guardrail_dados_sensiveis`)**
  * **Tática:** Criação de uma camada programática de inspeção de saída utilizando expressões regulares para varrer o texto gerado pela IA.
  * **Objetivo:** Mascarar automaticamente padrões sensíveis (`SEC_KEY_*`, `AUTH_GERENTE_*` e CPFs) substituindo-os por marcadores de bloqueio.

* **Atividade E: Teste de Defesa contra Extração de Chaves / Gerente**
  * **Tática:** Reexecutar o ataque de engenharia social (*roleplay* de auditor) contra o assistente já protegido pelo *guardrail*.
  * **Objetivo:** Validar se a barreira de regex intercepta e neutraliza a tentativa de roubo de chaves da API e códigos gerenciais.

* **Atividade F: Teste de Defesa contra Extração de PII / CPF**
  * **Tática:** Submeter tentativas de extração de dados de clientes ao assistente blindado.
  * **Objetivo:** Confirmar que o filtro sanitiza com sucesso documentos sensíveis, exibindo o formato mascarado (`***.***.***-**`) ao invés do dado real.

---

> **Lição Principal:** *"Nunca confie que instruções puramente em linguagem natural no System Prompt manterão segredos a salvo! Dados de infraestrutura, senhas e PII jamais devem ser expostos sem proteções ativas. Sempre implemente Guardrails de inspeção de saída para blindar o backend da sua aplicação!"*
