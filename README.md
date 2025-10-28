# -Explorando-Workflows-Automatizados-com-AWS-Step-Functions

# 🌀 AWS Step Functions - Desafio Prático

## 🎯 Objetivo
Este repositório foi criado como parte do desafio prático para consolidar o aprendizado sobre **AWS Step Functions**, com foco na criação e documentação de workflows automatizados.

---

## 🧠 O que são AWS Step Functions?
O **Step Functions** é um serviço da AWS que permite orquestrar vários serviços em fluxos de trabalho visuais. Ele ajuda a coordenar funções Lambda, tarefas em fila (SQS), notificações (SNS) e muito mais — tudo sem precisar gerenciar servidores.

---

## ⚙️ Estrutura do Workflow
O workflow criado neste laboratório inclui:
1. **Lambda Function** — responsável por executar uma tarefa (ex: processar um pedido ou validar dados).
2. **Step Function** — orquestra o fluxo das funções, controlando o que acontece em caso de sucesso ou erro.
3. **SNS Topic** — envia notificações ao final da execução.
4. **S3 Bucket (opcional)** — para armazenar logs ou resultados.

> Exemplo de diagrama do fluxo:
![Workflow Diagram](./images/step-functions-diagram.png)

---

## 🚀 Etapas Realizadas
1. Criação das funções Lambda na AWS.
2. Configuração do Step Functions no modo visual (Workflow Studio).
3. Definição dos estados e transições.
4. Teste e execução do fluxo.
5. Análise dos resultados no console.

---

## 🧩 Exemplo de Definição do Workflow
```json
{
  "Comment": "Exemplo de fluxo de aprovação com Step Functions",
  "StartAt": "Validar Dados",
  "States": {
    "Validar Dados": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:REGION:ACCOUNT_ID:function:ValidaDados",
      "Next": "Aprovar ou Reprovar"
    },
    "Aprovar ou Reprovar": {
      "Type": "Choice",
      "Choices": [
        {
          "Variable": "$.status",
          "StringEquals": "APROVADO",
          "Next": "Enviar Notificação"
        }
      ],
      "Default": "Encerrar"
    },
    "Enviar Notificação": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:REGION:ACCOUNT_ID:function:EnviarNotificacao",
      "End": true
    },
    "Encerrar": {
      "Type": "Fail",
      "Cause": "Processo reprovado"
    }
  }
}
