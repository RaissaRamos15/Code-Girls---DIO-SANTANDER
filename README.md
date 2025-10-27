# Code-Girls---DIO-SANTANDER
Esse repositório é para armazenamento de materiais de aprendizagens e cumprimento de desafios da plataforma DIO.

# 🚀 Desafio EC2 na AWS — Aprendizado na Prática

Oi! 👋 Seja bem-vindo(a) ao meu repositório do desafio EC2 da DIO. Aqui você vai encontrar minhas anotações, aprendizados e experiências enquanto explorava o mundo das instâncias EC2 na AWS. Se você também está começando, relaxa — esse material foi feito pra ser simples, direto e fácil de entender. Bora aprender junto?

---

## 📚 Sobre o Desafio

Esse desafio tem como objetivo colocar em prática tudo que foi aprendido sobre EC2, o serviço da AWS que permite criar máquinas virtuais na nuvem. A ideia é entender como funciona, testar na prática e documentar tudo de forma clara.

---

## 🧠 O que é EC2?

Imagina que você precisa de um computador potente, mas não quer (ou não pode) comprar um físico. O EC2 resolve isso: você "aluga" uma máquina virtual na nuvem da AWS e configura ela do jeitinho que quiser — sistema operacional, memória, CPU, rede, armazenamento... tudo!

Você só paga pelo tempo que usar, e pode ligar, desligar ou deletar a instância quando quiser. Bem flexível!

---

## 🔍 Componentes de uma Instância EC2

Quando você cria uma instância EC2, pode escolher:

- **CPU**: número de núcleos e tipo de processador
- **Memória RAM**: depende da carga que sua aplicação vai ter
- **Armazenamento**: pode ser disco local ou EBS (armazenamento em bloco)
- **Rede**: largura de banda, IP público ou privado
- **Sistema Operacional**: Linux, Windows, Amazon Linux, etc.

---

## 🧩 EC2 e o modelo IaaS

O EC2 é um exemplo de IaaS — Infrastructure as a Service. Isso quer dizer que a AWS cuida da infraestrutura (hardware, rede, virtualização), e você cuida do resto:

- Instalar e configurar o sistema operacional
- Gerenciar os aplicativos
- Proteger os dados e acessos
- Monitorar o desempenho

É ótimo pra quem quer controle total sobre o ambiente.

---

## 🛠️ Tipos de Instância EC2

A AWS tem várias famílias de instâncias, cada uma pensada pra um tipo de uso:

| Família | Ideal para... |
|--------|----------------|
| T (uso geral) | Aplicações leves, testes, dev |
| C (computação otimizada) | Processamento pesado, cálculos |
| R (memória otimizada) | Bancos de dados, apps que usam muita RAM |
| M (balanceada) | Equilíbrio entre CPU e memória |
| P / G (GPU) | Machine learning, renderização gráfica |

Exemplos de tipos: `t3.micro`, `c5.large`, `r6.xlarge`...

## 📝 Conclusão

Esse desafio foi uma ótima forma de entender como funciona o EC2 na prática. Aprendi a criar, configurar e gerenciar instâncias, além de entender melhor como a AWS organiza seus serviços.

Se você está começando agora, minha dica é: não tenha medo de errar! Teste bastante, leia a documentação oficial (link abaixo) e documente tudo que aprender. Isso ajuda demais!

📎 [Documentação oficial EC2](https://docs.aws.amazon.com/pt_br/toolkit-for-visual-studio/latest/user-guide/tkv-ec2-ami.html)



# ⚙️ Workflows Automatizados com AWS Step Functions

Este projeto tem como objetivo apresentar o funcionamento e as possibilidades do **AWS Step Functions**, um serviço da AWS utilizado para **criar, orquestrar e automatizar workflows** com integração entre diferentes recursos da nuvem, como funções Lambda, DynamoDB, SNS, entre outros.

---

## 🌩️ Conhecendo o AWS Step Functions

O **AWS Step Functions** é um orquestrador de fluxos de trabalho serverless que permite combinar vários serviços AWS em aplicações distribuídas e processos automatizados.  
Por meio de uma **máquina de estados (State Machine)**, é possível modelar graficamente e definir a sequência de tarefas, decisões e exceções de forma simples e escalável.

### 🔍 Principais Características
- **Modelo visual de execução:** facilita o entendimento e a depuração dos fluxos.  
- **Integração nativa:** conecta-se diretamente com Lambda, S3, DynamoDB, SNS, entre outros.  
- **Gerenciamento de erros e exceções:** permite definir políticas de *retry* e *catch*.  
- **Totalmente gerenciado:** sem necessidade de provisionar servidores.  

---

## 🚀 Benefícios do AWS Step Functions

- ✅ **Automação simplificada** de processos complexos.  
- ✅ **Escalabilidade automática** e alta disponibilidade.  
- ✅ **Monitoramento em tempo real** com logs integrados no CloudWatch.  
- ✅ **Facilidade de integração** com outros serviços AWS.  
- ✅ **Redução de código** — fluxos podem ser definidos em JSON ou YAML.  

---

## 🧩 Projeto Modelo no AWS Step Functions

O projeto exemplo consiste em um **workflow automatizado** que executa uma sequência de tarefas com base em funções Lambda e validações.  
O fluxo proposto segue a seguinte lógica:

1. **Receber entrada** de dados.  
2. **Executar validação** por uma função Lambda.  
3. **Processar dados válidos** com outra função Lambda.  
4. **Encerrar o fluxo** com sucesso ou falha.

### 🧠 Exemplo de Definição (JSON)

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
🧾 Realizando Validações no AWS Step Functions
As validações são fundamentais para garantir que os dados sigam o caminho correto no fluxo.
No Step Functions, isso é feito com o estado Choice, que permite criar bifurcações lógicas.

🧮 Exemplo:
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
Se a condição for atendida, o fluxo segue para ProcessarDados; caso contrário, vai para ErroValidacao.

🧰 Criando e Executando Lambda no AWS Step Functions
As funções Lambda são responsáveis por executar as tarefas do workflow.
Elas podem ser escritas em Python, Node.js, Java, entre outras linguagens.

Exemplo em Python:
python
Copiar código
def lambda_handler(event, context):
    if "id" in event:
        return {"status": "ok", "mensagem": "Validação concluída com sucesso"}
    else:
        return {"status": "erro", "mensagem": "Campo 'id' ausente"}
Depois de criar a função Lambda, copie o ARN e adicione-o à definição da sua máquina de estados no Step Functions.

⚡ Executando o Workflow
Acesse o AWS Management Console.

Vá até Step Functions → Create state machine.

Escolha Author with code snippets e cole o JSON acima.

Associe as funções Lambda criadas anteriormente.

Clique em Start Execution para iniciar o fluxo.

Acompanhe a execução visualmente no painel do Step Functions.

📚 Referências
Documentação Oficial do AWS Step Functions

AWS Lambda – Documentação

Tutorial AWS: Criando sua primeira State Machine



















Infraestrutura como Código com AWS CloudFormation

Este projeto tem como objetivo apresentar o funcionamento do **AWS CloudFormation**, um dos principais serviços da AWS voltado para a **automação da infraestrutura como código (IaC)**.  
Aqui você aprenderá como **criar e gerenciar Stacks**, além de um exemplo prático de **Stack de Firewall** implementado via CloudFormation.

---

## ☁️ Conhecendo o AWS CloudFormation

O **AWS CloudFormation** é um serviço que permite **modelar, provisionar e gerenciar recursos da AWS** por meio de **templates declarativos** escritos em **YAML ou JSON**.  
Em vez de criar recursos manualmente pelo console, é possível definir toda a arquitetura da aplicação em um arquivo de configuração — o que garante **padronização, repetibilidade e versionamento**.

### 🔍 Conceito-chave
- **Template:** arquivo que descreve os recursos a serem criados (ex.: EC2, S3, VPC, Security Groups, etc.).  
- **Stack:** conjunto de recursos criados a partir de um template.  
- **Change Set:** visualização prévia das alterações antes da aplicação.

---

## 🚀 Benefícios do AWS CloudFormation

✅ **Automatiza a criação e atualização de infraestrutura.**  
✅ **Evita erros manuais** ao provisionar recursos.  
✅ **Permite versionar configurações** junto ao código da aplicação.  
✅ **Integra-se com outros serviços AWS**, como IAM, EC2, S3 e Lambda.  
✅ **Permite rollback automático** em caso de falha na criação da Stack.  

---

## 🧩 Criando Stacks no AWS CloudFormation

Uma **Stack** é uma coleção de recursos AWS que são criados e gerenciados como uma unidade.  
Cada vez que você envia um template para o CloudFormation, ele cria (ou atualiza) uma Stack com base nesse modelo.

### 🧠 Exemplo simples de Template (YAML)

```yaml
AWSTemplateFormatVersion: "2010-09-09"
Description: Exemplo simples de Stack no AWS CloudFormation

Resources:
  MeuBucketS3:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: meu-bucket-exemplo-cloudformation
🪜 Criando uma Stack no Console AWS
Acesse o AWS CloudFormation no console.

Clique em Create stack → With new resources (standard).

Envie o template YAML ou JSON.

Escolha um nome para a Stack.

Revise e clique em Create stack.

Aguarde a criação e visualize o status no painel (estado CREATE_COMPLETE).

🔒 Criando Stacks de Firewall no CloudFormation
Com o CloudFormation, também é possível provisionar regras de segurança e firewalls gerenciados automaticamente.
Abaixo está um exemplo de Stack que cria um AWS Network Firewall dentro de uma VPC.

🧱 Exemplo de Template (Firewall)
yaml
Copiar código
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
💡 Esse exemplo cria uma política e um firewall básico associado a uma VPC existente.
Substitua os IDs de VPC e Subnet pelos seus valores reais antes da execução.

⚙️ Criando Stacks via CLI
Você também pode criar a Stack usando o AWS CLI, com o comando:

bash
Copiar código
aws cloudformation create-stack \
  --stack-name stack-firewall-exemplo \
  --template-body file://firewall-template.yaml \
  --capabilities CAPABILITY_NAMED_IAM
Para verificar o status:

bash
Copiar código
aws cloudformation describe-stacks --stack-name stack-firewall-exemplo
E para excluir a Stack:

bash
Copiar código
aws cloudformation delete-stack --stack-name stack-firewall-exemplo
🧾 Boas Práticas
Versão no controle de código (Git): mantenha seus templates versionados.

Use parâmetros (Parameters) para criar templates reutilizáveis.

Utilize outputs (Outputs) para expor informações úteis, como IDs de recursos.

Combine com AWS Step Functions para automatizar fluxos de provisionamento complexos.

Valide seus templates antes de enviar:

bash
Copiar código
aws cloudformation validate-template --template-body file://template.yaml
📚 Referências
Documentação Oficial do AWS CloudFormation

AWS Network Firewall Documentation

Guia: Criando Stacks pelo Console AWS


