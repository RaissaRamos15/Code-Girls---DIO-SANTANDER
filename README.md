Desafios AWS — DIO

Este repositório foi criado para armazenar materiais de aprendizado e desafios práticos da plataforma DIO relacionados à Amazon Web Services (AWS).
Aqui estão reunidos estudos sobre EC2, Step Functions, CloudFormation e Lambda com S3, com foco em praticar, documentar e entender a fundo o funcionamento dos serviços da nuvem AWS.

🚀 Desafio EC2 na AWS — Aprendizado na Prática
👋 Introdução

Este projeto registra meus estudos e experiências com o Amazon EC2, o serviço de máquinas virtuais da AWS.
O objetivo foi compreender como criar, configurar e gerenciar instâncias, aplicando conceitos de infraestrutura elástica na prática.

🧠 O que é o Amazon EC2?

O Amazon Elastic Compute Cloud (EC2) permite criar e gerenciar instâncias virtuais configuradas sob medida.
Você define CPU, memória, rede, armazenamento e sistema operacional — e paga apenas pelo tempo de uso.

Principais componentes:

CPU: número de núcleos e tipo de processador.

Memória: quantidade de RAM conforme a aplicação.

Armazenamento: local ou EBS (Elastic Block Store).

Rede: IP público ou privado.

SO: Linux, Windows, Amazon Linux, etc.

🧩 EC2 e o modelo IaaS

O EC2 é um serviço IaaS (Infrastructure as a Service) — a AWS gerencia a infraestrutura física e a virtualização, enquanto o usuário gerencia o sistema operacional, aplicações e dados.

⚙️ Tipos de Instância EC2
Família	Ideal para...
T (uso geral)	Aplicações leves, testes e desenvolvimento
C (computação)	Processamento intensivo
R (memória)	Bancos de dados e apps com alta RAM
M (balanceada)	Equilíbrio entre CPU e memória
P / G (GPU)	Machine Learning, renderização gráfica

Exemplo: t3.micro, c5.large, r6.xlarge

✅ Conclusão

O desafio EC2 ajudou a entender a base da infraestrutura AWS.
Dica: teste, leia a documentação e registre tudo — aprender na prática é o caminho!

📘 Documentação Oficial do EC2

⚙️ Workflows Automatizados com AWS Step Functions
🌩️ O que é AWS Step Functions

O Step Functions é um orquestrador de fluxos de trabalho serverless, que conecta serviços AWS (como Lambda, S3, DynamoDB e SNS) por meio de uma máquina de estados visual.

🔍 Principais Características

✅ Criação visual e monitoramento de fluxos
✅ Integração nativa com serviços AWS
✅ Tratamento de erros e exceções (retry/catch)
✅ Alta disponibilidade e escalabilidade
✅ Definição em JSON ou YAML

🧩 Exemplo de Workflow
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

🐍 Exemplo de Função Lambda
def lambda_handler(event, context):
    if "id" in event:
        return {"status": "ok", "mensagem": "Validação concluída com sucesso"}
    else:
        return {"status": "erro", "mensagem": "Campo 'id' ausente"}

⚡ Executando o Workflow

Acesse o AWS Management Console

Vá em Step Functions → Create state machine

Cole o JSON

Associe as funções Lambda

Clique em Start Execution

📘 Documentação Oficial do AWS Step Functions

🤖 Tarefas Automatizadas com AWS Lambda e Amazon S3
☁️ O que é o AWS Lambda

O AWS Lambda permite executar código sem precisar gerenciar servidores.
Você apenas define o que deve acontecer quando algo ocorre — por exemplo, o upload de um arquivo no S3.

O Lambda é amplamente usado para tarefas automatizadas, como:

Processamento de imagens e vídeos.

Geração de logs.

Movimentação e transformação de dados.

Integração entre serviços.

🧠 Exemplo Prático — Integração com S3

Neste exemplo, o Lambda é configurado para executar automaticamente toda vez que um arquivo for adicionado ao Amazon S3.

🔧 Etapas:

Criar um bucket S3.

Criar uma função Lambda.

Definir um gatilho (trigger) do S3 → evento “ObjectCreated”.

Testar enviando um arquivo ao bucket.

🐍 Exemplo de Código Lambda (Python)
import json

def lambda_handler(event, context):
    bucket = event['Records'][0]['s3']['bucket']['name']
    arquivo = event['Records'][0]['s3']['object']['key']

    print(f"Novo arquivo detectado: {arquivo} no bucket {bucket}")

    return {
        'statusCode': 200,
        'body': json.dumps(f"Processamento concluído para {arquivo}")
    }


🪄 O que acontece:

Quando um arquivo é enviado ao S3, o Lambda é acionado.

Ele identifica o bucket e o nome do arquivo.

Pode processar o conteúdo, mover, converter, ou registrar logs automaticamente.

📈 Benefícios da Automação com Lambda + S3

✅ Processamento automático sem servidores.
✅ Alta escalabilidade e baixo custo.
✅ Integração fácil com outros serviços AWS.
✅ Ideal para pipelines de dados e automação de rotinas.

📘 Documentação AWS Lambda

📗 Documentação Amazon S3

🏗️ Infraestrutura como Código com AWS CloudFormation
☁️ O que é o CloudFormation

O AWS CloudFormation automatiza a criação e o gerenciamento de recursos AWS usando templates em YAML ou JSON.
Você define toda a infraestrutura como código (IaC), garantindo padronização e versionamento.

🔧 Conceitos-Chave

Template: define os recursos (EC2, S3, VPC, etc.)

Stack: conjunto de recursos criados a partir do template

Change Set: visualização prévia das alterações

🧠 Exemplo simples de Template
AWSTemplateFormatVersion: "2010-09-09"
Description: Exemplo simples de Stack no AWS CloudFormation

Resources:
  MeuBucketS3:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: meu-bucket-exemplo-cloudformation

🪜 Criando uma Stack no Console

Acesse AWS CloudFormation

Clique em Create Stack → With new resources (standard)

Envie o template YAML/JSON

Escolha o nome da Stack

Clique em Create stack

Aguarde o status CREATE_COMPLETE

🔒 Exemplo — Stack de Firewall
AWSTemplateFormatVersion: "2010-09-09"
Description: Stack de Firewall no AWS CloudFormation

Resources:
  MeuFirewallPolicy:
    Type: AWS::NetworkFirewall::FirewallPolicy
    Properties:
      FirewallPolicyName: FirewallPolicyExemplo
      FirewallPolicy:
        StatelessDefaultActions:
          - aws:forward_to_sfe
        StatelessFragmentDefaultActions:
          - aws:forward_to_sfe

  MeuFirewall:
    Type: AWS::NetworkFirewall::Firewall
    Properties:
      FirewallName: FirewallExemplo
      FirewallPolicyArn: !Ref MeuFirewallPolicy
      VpcId: vpc-1234567890abcdef
      SubnetMappings:
        - SubnetId: subnet-abcdef1234567890
      DeleteProtection: false


💡 Dica: substitua os IDs de VPC e Subnet pelos seus valores reais antes da execução.

💻 Criando Stack via CLI
aws cloudformation create-stack \
  --stack-name stack-firewall-exemplo \
  --template-body file://firewall-template.yaml \
  --capabilities CAPABILITY_NAMED_IAM


Ver status:

aws cloudformation describe-stacks --stack-name stack-firewall-exemplo


Excluir Stack:

aws cloudformation delete-stack --stack-name stack-firewall-exemplo

🧾 Boas Práticas

✅ Versione seus templates com Git
✅ Use Parameters e Outputs
✅ Valide templates antes do deploy
✅ Combine com Step Functions para automação

📘 Documentação AWS CloudFormation

📗 AWS Network Firewall Documentation

🧭 Conclusão

Esses desafios da DIO proporcionaram uma visão prática sobre computação em nuvem, automação e infraestrutura como código.
Juntos, EC2, Lambda + S3, Step Functions e CloudFormation representam pilares essenciais para o desenvolvimento moderno em ambientes serverless e escaláveis.
