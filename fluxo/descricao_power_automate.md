# 🔄 Fluxo Power Automate – Monitoramento de Jobs

## 📖 Visão geral

Este fluxo no Power Automate é responsável por receber eventos via webhook provenientes do Databricks e processar o envio de notificações para um canal do Microsoft Teams.

A solução permite o envio de mensagens simples ou estruturadas (com attachments), garantindo flexibilidade no formato dos alertas.

---

## ⚙️ Funcionamento do fluxo

### 🟦 1. Trigger – Recebimento do webhook

**Ação:** `Quando uma solicitação de webhook do Teams é recebida`

- O fluxo inicia automaticamente ao receber uma requisição HTTP
- A requisição contém os dados processados no Databricks (status dos jobs e informações de falha)

---

### 🟦 2. Etapa de controle

**Ação:** `Do Not Remove Flow`

- Etapa auxiliar utilizada para controle interno do fluxo
- Pode ser utilizada para padronização ou compatibilidade com integrações existentes

---

### 🟦 3. Inicialização de variáveis

O fluxo inicializa duas variáveis principais:

#### 📌 Body
- Armazena o conteúdo da requisição recebida
- Contém as informações principais sobre os jobs e alertas

#### 📌 Attachments
- Armazena possíveis anexos enviados na requisição
- Utilizado para envio de mensagens estruturadas (ex: Adaptive Cards)

---

### 🟦 4. Validação condicional

**Condição:** `Attachments is null`

O fluxo verifica se existem anexos na mensagem recebida.

---

## 🔀 Execução condicional

### ✅ Caminho 1 — Sem anexos (Verdadeiro)

- Condição: `Attachments = null`
- Ação:
  - Envio de mensagem simples para o Microsoft Teams
  - Canal: **Monitoria de JOBS**

📌 Utilizado para notificações diretas, sem formatação avançada.

---

### ❌ Caminho 2 — Com anexos (Falso)

- Condição: `Attachments != null`
- Ação:
  - Envio de mensagem estruturada com anexos
  - Canal: **Monitoria de Jobs**

📌 Utilizado para:
- Adaptive Cards
- Mensagens com múltiplas informações
- Alertas mais ricos visualmente

---

## 🔔 Saída do processo

Em ambos os cenários, o fluxo realiza:

- Envio de notificações automáticas para o Microsoft Teams
- Centralização dos alertas em um canal dedicado
- Suporte a mensagens simples e estruturadas
