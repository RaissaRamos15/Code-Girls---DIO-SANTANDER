 Workflows Automatizados com AWS Step Functions

Este projeto apresenta o funcionamento e as possibilidades do **AWS Step Functions**, um serviço da AWS utilizado para **criar, orquestrar e automatizar workflows** entre diferentes recursos da nuvem, como funções Lambda, DynamoDB, SNS, entre outros.

---

## 🌩️ Conhecendo o AWS Step Functions

O **Step Functions** é um orquestrador de fluxos de trabalho serverless que permite combinar vários serviços AWS em aplicações distribuídas e processos automatizados.  
Por meio de uma **máquina de estados (State Machine)**, é possível modelar graficamente a sequência de tarefas, decisões e exceções.

### 🔍 Principais Características
- Modelo visual de execução para facilitar entendimento e depuração  
- Integração nativa com Lambda, S3, DynamoDB, SNS, entre outros  
- Gerenciamento de erros com políticas de retry e catch  
- Totalmente gerenciado, sem necessidade de provisionar servidores  

---

## 🚀 Benefícios
✅ Automação de processos complexos  
✅ Escalabilidade automática e alta disponibilidade  
✅ Monitoramento em tempo real via CloudWatch  
✅ Redução de código com fluxos definidos em JSON ou YAML  

---

## 🧩 Projeto Modelo

Fluxo de exemplo:

1. Receber entrada de dados  
2. Validar dados com função Lambda  
3. Processar dados válidos com outra Lambda  
4. Encerrar com sucesso ou falha  

### Exemplo de definição JSON
```json
{
  "Comment": "Exemplo de workflow com AWS Step Functions",
  "StartAt": "ValidarEntrada",
  "States": {
    "ValidarEntrada": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:REGIAO:ID_CONTA:function:validarEntrada",
      "Next": "ProcessarDados"
    },
    "ProcessarDados": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:REGIAO:ID_CONTA:function:processarDados",
      "Next": "Sucesso"
    },
    "Sucesso": {
      "Type": "Succeed"
    }
  }
}
🧾 Validações com Choice State
json
Copiar código
"ValidarEntrada": {
  "Type": "Choice",
  "Choices": [
    {
      "Variable": "$.status",
      "StringEquals": "ok",
      "Next": "ProcessarDados"
    }
  ],
  "Default": "ErroValidacao"
}
🐍 Criando e Executando Lambda
Exemplo em Python:

python
Copiar código
def lambda_handler(event, context):
    if "id" in event:
        return {"status": "ok", "mensagem": "Validação concluída com sucesso"}
    else:
        return {"status": "erro", "mensagem": "Campo 'id' ausente"}
⚡ Executando o Workflow
AWS Console → Step Functions → Create state machine

Escolher Author with code snippets

Colar JSON acima

Associar funções Lambda

Start Execution

📚 Referências:

AWS Step Functions

AWS Lambda
