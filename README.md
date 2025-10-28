# -Explorando-Workflows-Automatizados-com-AWS-Step-Functions

# 🌀 AWS Step Functions - Desafio Prático

## 🎯 Objetivo
Este repositório foi criado como parte do desafio prático para consolidar o aprendizado sobre **AWS Step Functions**, com foco na criação e documentação de workflows automatizados.

---

## 🧠 O que são AWS Step Functions?
O **AWS Step Functions** é um serviço que permite orquestrar fluxos de trabalho compostos por diferentes serviços da AWS — como **Lambda**, **SQS**, **SNS**, **DynamoDB** e outros — tudo isso de forma **visual e automatizada**, sem precisar gerenciar servidores.

Cada parte do fluxo é chamada de **estado**, e cada estado executa uma ação, podendo depender do resultado anterior. Isso torna o processo muito mais organizado e confiável.

---

## ⚙️ Estrutura do Workflow Criado

O workflow desenvolvido neste laboratório segue as seguintes etapas:

1. **Lambda Function** – Responsável por processar ou validar dados.
2. **Step Function** – Gerencia o fluxo das funções, decidindo o próximo passo com base no resultado.
3. **SNS Topic** – Envia notificações ao final da execução.
4. **S3 Bucket (opcional)** – Armazena logs ou dados de saída.

> Exemplo de diagrama do fluxo:
![Workflow Diagram](./images/step-functions-diagram.png)

---

## 🚀 Etapas Realizadas

1. Criação de uma função Lambda no console da AWS.
2. Desenvolvimento do fluxo principal no **AWS Step Functions (Workflow Studio)**.
3. Configuração dos estados, transições e condições de erro.
4. Integração com SNS para envio de mensagens após a execução.
5. Teste prático do fluxo e análise de logs.

---

## 🧩 Exemplo de Definição do Workflow (JSON)

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

