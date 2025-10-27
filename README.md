arkdown
# 🏗️ Infraestrutura como Código com AWS CloudFormation

Este projeto demonstra como usar o **AWS CloudFormation** para criar e gerenciar recursos AWS de forma automatizada, escalável e versionável.

---

## ☁️ Conceitos-Chave
- **Template:** arquivo YAML ou JSON que descreve os recursos (EC2, S3, VPC, Security Groups)  
- **Stack:** conjunto de recursos criados a partir de um template  
- **Change Set:** pré-visualização das alterações antes de aplicar  

---

## 🚀 Benefícios
✅ Criação e atualização automática de infraestrutura  
✅ Redução de erros manuais  
✅ Versionamento junto ao código da aplicação  
✅ Rollback automático em caso de falha  

---

## 🧩 Criando Stacks
### Exemplo de Template YAML
```yaml
AWSTemplateFormatVersion: "2010-09-09"
Description: Exemplo simples de Stack no CloudFormation

Resources:
  MeuBucketS3:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: meu-bucket-exemplo-cloudformation
Criando Stack via Console
AWS Console → CloudFormation → Create stack → With new resources (standard)

Enviar template YAML/JSON

Nomear Stack

Create stack → aguardar status CREATE_COMPLETE

🔒 Stack de Firewall
yaml
Copiar código
AWSTemplateFormatVersion: "2010-09-09"
Description: Stack de Firewall no CloudFormation

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
Criando via CLI
bash
Copiar código
aws cloudformation create-stack \
  --stack-name stack-firewall-exemplo \
  --template-body file://firewall-template.yaml \
  --capabilities CAPABILITY_NAMED_IAM

aws cloudformation describe-stacks --stack-name stack-firewall-exemplo
aws cloudformation delete-stack --stack-name stack-firewall-exemplo
📚 Referências:

CloudFormation

AWS Network Firewall
