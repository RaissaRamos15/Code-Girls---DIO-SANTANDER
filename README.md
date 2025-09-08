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

