Desafios AWS — DIO

Este repositório é destinado ao armazenamento de materiais de aprendizagem e desafios práticos da plataforma DIO, com foco em serviços da AWS (Amazon Web Services).
Aqui você encontrará anotações, exemplos e templates utilizados durante o aprendizado de EC2, Step Functions e CloudFormation.

🚀 Desafio EC2 na AWS — Aprendizado na Prática
👋 Introdução

Bem-vindo(a)! Este projeto registra meus estudos e experiências com o Amazon EC2, o serviço de máquinas virtuais da AWS.
O objetivo foi entender como criar, configurar e gerenciar instâncias na nuvem — tudo de forma prática e documentada.

🧠 O que é EC2?

O EC2 (Elastic Compute Cloud) é um serviço que permite criar e gerenciar instâncias virtuais na nuvem da AWS.
Você pode personalizar CPU, memória, armazenamento, rede e sistema operacional conforme sua necessidade — pagando apenas pelo tempo de uso.

Principais componentes:

CPU: núcleos e tipo de processador.

Memória: conforme a carga da aplicação.

Armazenamento: local ou EBS (Elastic Block Store).

Rede: IP público/privado e largura de banda.

Sistema Operacional: Linux, Windows, Amazon Linux, etc.

🧩 EC2 e o modelo IaaS

O EC2 é um serviço de Infraestrutura como Serviço (IaaS), em que a AWS gerencia o hardware e a virtualização, enquanto você gerencia:

Sistema operacional

Aplicações

Segurança e acesso

Monitoramento e desempenho

⚙️ Tipos de Instância EC2
Família	Ideal para...
T (uso geral)	Aplicações leves, testes e desenvolvimento
C (computação)	Processamento intensivo e cálculos
R (memória)	Bancos de dados e aplicações de alta RAM
M (balanceada)	Equilíbrio entre CPU e memória
P / G (GPU)	Machine Learning e renderização gráfica

Exemplo: t3.micro, c5.large, r6.xlarge

✅ Conclusão

Este desafio foi essencial para compreender o funcionamento do EC2 e aplicar conceitos de infraestrutura elástica.
Dica: teste, erre, leia a documentação e registre seu aprendizado — isso faz toda diferença!

📘 Documentação Oficial do EC2

⚙️ Workflows Automatizados com AWS Step Functions
🌩️ O que é AWS Step Functions

O AWS Step Functions é um orquestrador de fluxos de trabalho serverless.
Ele permite automatizar processos e integrar vários serviços AWS (como Lambda, DynamoDB, S3 e SNS) por meio de uma máquina de estados visual.

🔍 Principais Características

✅ Modelo visual de execução e monitoramento
✅ Integração nativa com serviços AWS
✅ Tratamento de erros e exceções (retry, catch)
✅ Escalabilidade e alta disponibilidade
✅ Fluxos definidos em JSON ou YAML

🧩 Exemplo de Workflow (JSON)
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

🐍 Exemplo de Função Lambda em Python
def lambda_handler(event, context):
    if "id" in event:
        return {"status": "ok", "mensagem": "Validação concluída com sucesso"}
    else:
        return {"status": "erro", "mensagem": "Campo 'id' ausente"}

⚡ Executando o Workflow

Acesse o AWS Management Console

Vá até Step Functions → Create state machine

Cole o JSON do fluxo

Associe suas funções Lambda

Clique em Start Execution

📘 Documentação Oficial do AWS Step Functions

🏗️ Infraestrutura como Código com AWS CloudFormation
☁️ O que é o AWS CloudFormation

O AWS CloudFormation permite modelar, provisionar e gerenciar recursos AWS como código — usando arquivos YAML ou JSON.
Com isso, é possível criar infraestruturas completas de forma automática, padronizada e versionável.

🔧 Conceitos-Chave

Template: define os recursos (EC2, S3, VPC, etc.).

Stack: conjunto de recursos criados a partir do template.

Change Set: pré-visualização das mudanças antes da aplicação.

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

Acompanhe o status até CREATE_COMPLETE

🔒 Exemplo de Stack de Firewall
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

💻 Criando Stack via AWS CLI
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
✅ Use Parameters e Outputs para reutilização
✅ Valide templates antes do deploy:

aws cloudformation validate-template --template-body file://template.yaml


✅ Combine com Step Functions para provisionamentos automatizados

📘 Documentação Oficial do AWS CloudFormation

📗 AWS Network Firewall Documentation

🧭 Conclusão

Esses desafios da DIO foram fundamentais para compreender infraestrutura como código, automação de workflows e gerenciamento de recursos em nuvem usando AWS.
Cada serviço — EC2, Step Functions e CloudFormation — representa um passo importante rumo à automação e eficiência operacional em ambientes cloud.
