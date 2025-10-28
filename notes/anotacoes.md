# 💡 Anotações e Insights – AWS Step Functions

## 🧠 Entendimento Geral
O **AWS Step Functions** é um serviço que permite criar **workflows automatizados** compostos por etapas chamadas **estados**, que podem executar funções Lambda, enviar mensagens SNS, acessar bancos de dados e muito mais.

Cada estado representa uma parte do processo e pode ter transições condicionais, loops e tratamento de erros. Isso torna o fluxo **visual, escalável e resiliente**.

---

## ⚙️ Estrutura do Workflow Criado
Durante o laboratório, o fluxo foi estruturado da seguinte forma:

1. **Função Lambda:** processa os dados de entrada.  
2. **Step Function:** coordena a execução da Lambda e decide o próximo passo.  
3. **SNS Topic:** envia uma notificação ao final da execução.  
4. **S3 (opcional):** usado para armazenar logs e resultados.

---

## 🚀 Etapas Realizadas
- Criação de uma função Lambda simples no console da AWS.  
- Desenvolvimento do workflow no **AWS Step Functions Workflow Studio**.  
- Configuração das transições entre estados e ações em caso de erro.  
- Teste de execução e análise de logs no console da AWS.  

---

## 💭 Dificuldades Encontradas
- Entender o formato JSON exato da definição do fluxo.  
- Ajustar permissões IAM para que o Step Functions conseguisse invocar a Lambda.  
- Interpretar mensagens de erro nas execuções.

---

## 🧩 Soluções Adotadas
- Consultei a **documentação oficial** da AWS.  
- Testei várias configurações diretamente no **Workflow Studio**.  
- Usei **CloudWatch Logs** para analisar o comportamento das execuções.  
- Ajustei as **políticas IAM** para incluir permissões `lambda:InvokeFunction` e `sns:Publish`.

---

## 📘 O que Aprendi
- O Step Functions é uma forma poderosa de **automatizar processos** sem precisar escrever toda a lógica de orquestração em código.  
- A visualização em gráfico facilita o entendimento do fluxo.  
- As integrações com **Lambda**, **SNS** e **S3** tornam o sistema altamente flexível.  
- Versionar o JSON no GitHub ajuda na **documentação e reuso** do fluxo.

---

## 🧠 Reflexão Final
Esse laboratório foi essencial para consolidar meu aprendizado sobre automação com AWS.  
A prática mostrou que entender **como os serviços da AWS se comunicam** é tão importante quanto escrever código.  
Agora tenho mais confiança para criar fluxos reais e documentar de forma técnica e organizada.
