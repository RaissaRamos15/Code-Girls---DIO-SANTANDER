
```markdown
# 🤖 Tarefas Automatizadas com AWS Lambda e Amazon S3

Este projeto mostra como automatizar processos usando **AWS Lambda** em conjunto com **Amazon S3** para processamento automático de arquivos e dados.

---

## ☁️ AWS Lambda
Serviço serverless que executa código sem precisar de servidores.  
Pode ser acionado por eventos do S3, CloudWatch, API Gateway, entre outros.

### Benefícios
✅ Execução automática baseada em eventos  
✅ Escalabilidade automática  
✅ Baixo custo  
✅ Integração nativa com outros serviços AWS  

---

## 🌩️ Integração Lambda + S3

### Passos
1. Criar bucket S3  
2. Criar função Lambda  
3. Configurar trigger do S3 (ObjectCreated)  
4. Testar enviando arquivo ao bucket  

### Exemplo Lambda (Python)
```python
import json

def lambda_handler(event, context):
    bucket = event['Records'][0]['s3']['bucket']['name']
    arquivo = event['Records'][0]['s3']['object']['key']

    print(f"Novo arquivo detectado: {arquivo} no bucket {bucket}")

    return {
        'statusCode': 200,
        'body': json.dumps(f"Processamento concluído para {arquivo}")
    }
O que acontece
Ao enviar arquivo para S3 → Lambda é acionada

Lambda lê bucket e arquivo

Pode processar, mover, transformar ou gerar logs

📚 Referências:

AWS Lambda

Amazon S3
