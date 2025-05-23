<h3 align="center">< Projeto Cloud /></h3>

<h1 align="center">
    <img align="center" src="https://logospng.org/download/uol/logo-uol-icon-256.png" width="30" height="30" /> Compass UOL - DevSecOps
</h1>

👥 Integrantes do Grupo:

- Lucas Pinheiro Josino da Silva
- Fabiano Vandré Campelo de Medeiros

Projeto Cloud da trilha de **DevSecOps**, dividido em duas partes:

1. Migração para AWS:
2. Modernização:

## Contexto

A empresa **"Fast Engineering S/A"** gostaría de uma solução desenvolvida pela empresa terceira **"TI SOLUÇÕES INCRÍVEIS"**.

**Problema**: O e-commerce está crescendo e a solução atual não está atendendo a alta demanda de acessos e compras.

Atualmente é utilizado:

- **Banco de Dados**: MySQL (500GB de dados, 10GB de RAM, 3 Core CPU)
- **Frontend**: React (5GB de dados, 2GB de RAM, 1 Core CPU)
- **Backend**:
  - 3 APIs
  - Nginx como balanceador de carga
  - Armazena arquivos estáticos (5GB de dados, 4GB de RAM, 2 Core CP)

Diagrama da situação atual:

<div align="center">

![Diagrama](./assets/on-premise.png)

</div>

## Obejtivo Final

- Migração bem sucedida para AWS;
- Ambiente modernizado com Kubernetes;
- Banco de dados gerenciado (PaaS e Multi-AZ);
- Backup de dados;
- Sistema para persistência de objetos (imagens, vídeos etc.);
- Requisitos de segurança avançados;

## Migração

A migração será feita a partir do modo Lift-and-Shift (Rehosting), onde, toda a infraestrutura local será transferida para a núvem sem grandes mudanças nos sistemas e aplicações.

<div align="center">

<img src="https://community.nasscom.in/sites/default/files/inline-images/Migration.png" height="300px" />

Source: [nasscom.in](https://community.nasscom.in/communities/application/lift-and-shift-cloud-migration-application-modernization-comprehensive)

</div>

## Etapas

A migração vai ocorrer em diferentes etapas:

1. Planejamento
2. Preparação
3. Migração
   - Banco de Dados
   - Arquivos
   - Aplicação

### Planejamento

Definição das instâncias que serão utilizas na AWS:

- **Frontend**: Instâncias EC2 (tipo **t4g.small** / vCPU: 2, Memória: 2 GB).
- **Backend**: Instâncias EC2 (tipo **t4g.medium** / vCPU: 2, Memória: 4 GB).
- **Banco de Dados**: Amazon RDS MySQL (tipo **db.t4g.xlarge** / vCPU: 2, Memória: 16 GB).

> De início, os arquivos estáticos vão ser salvos no EBS

Análise e comparação dos serviços utilizando na empresa com as oferencidas pela AWS:

|                                                       -                                                        | Serviço       | On premise                  |
| :------------------------------------------------------------------------------------------------------------: | ------------- | --------------------------- |
|                    <img src="https://icon.icepanel.io/AWS/svg/Compute/EC2.svg" width="40">                     | EC2           | Servidor 1 (Frontend)       |
|                    <img src="https://icon.icepanel.io/AWS/svg/Database/RDS.svg" width="40">                    | RDS (MySQL)   | Servidor 2 (Banco de Dados) |
| <img src="https://icon.icepanel.io/AWS/svg/Networking-Content-Delivery/Elastic-Load-Balancing.svg" width="40"> | Load Balancer | Servidor 3 (API's + Nginx)  |

#### Serviços extras:

|                                                       -                                                       | Serviços                                                     |
| :-----------------------------------------------------------------------------------------------------------: | ------------------------------------------------------------ |
| <img src="https://icon.icepanel.io/AWS/svg/Security-Identity-Compliance/IAM-Identity-Center.svg" width="40">  | IAM                                                          |
|            <img src="https://icon.icepanel.io/AWS/svg/Storage/Elastic-Block-Store.svg" width="40">            | EBS <br> <sub>(Utilizado pelo AMS/MGN)</sub>                 |
| <img src="https://icon.icepanel.io/AWS/svg/Networking-Content-Delivery/Virtual-Private-Cloud.svg" width="40"> | VPC <br> <sub>+ Subnets, Route Table e Security Groups</sub> |

#### Serviços que serão utilizados durante a migração:

|                                                      -                                                       | Serviço                             |
| :----------------------------------------------------------------------------------------------------------: | ----------------------------------- |
|                  <img src="https://icon.icepanel.io/AWS/svg/Storage/Backup.svg" width="40">                  | AWS Backup                          |
|      <img src="https://icon.icepanel.io/AWS/svg/Networking-Content-Delivery/Client-VPN.svg" width="40">      | VPN/VPN Connection                  |
|       <img src="https://icon.icepanel.io/AWS/svg/Database/Database-Migration-Service.svg" width="40">        | Database Migration Service (DMS)    |
| <img src="https://icon.icepanel.io/AWS/svg/Migration-Transfer/Application-Migration-Service.svg" width="40"> | Application Migration Service (MGN) |

#### Diagrama de Migração:

<div align="center">

![Diagrama da Migração](./assets/AWS-Migration.png)

</div>

#### Custo (Migração)

|                                                      -                                                       | **Serviço**            |        **Custo (3 dias)** |
| :----------------------------------------------------------------------------------------------------------: | ---------------------- | ------------------------: |
|                   <img src="https://icon.icepanel.io/AWS/svg/Compute/EC2.svg" width="40">                    | AWS EC2 – Webapp       |                ~ 0.88 USD |
|                   <img src="https://icon.icepanel.io/AWS/svg/Compute/EC2.svg" width="40">                    | AWS EC2 – API's        |                ~ 1.76 USD |
|       <img src="https://icon.icepanel.io/AWS/svg/Database/Database-Migration-Service.svg" width="40">        | AWS DMS (1 instância)  |               ~ 16.62 USD |
| <img src="https://icon.icepanel.io/AWS/svg/Migration-Transfer/Application-Migration-Service.svg" width="40"> | AWS MGN (2 servidores) |                ~ 3.02 USD |
|      <img src="https://icon.icepanel.io/AWS/svg/Networking-Content-Delivery/Client-VPN.svg" width="40">      | VPN Site-to-site       |                ~ 1.00 USD |
|                  <img src="https://icon.icepanel.io/AWS/svg/Storage/Backup.svg" width="40">                  | AWS Backup             |                ~ 0.32 USD |
|           <img src="https://icon.icepanel.io/AWS/svg/Storage/Elastic-Block-Store.svg" width="40">            | RDS (MySQL) **\*\*\*** |               ~ 38.74 USD |
|                                                      -                                                       | TOTAL                  | **62.34 USD** (20.78/dia) |

> Link para a estimativa: [Migração para AWS](https://calculator.aws/#/estimate?id=29258dfa209b63ff6c0509c11bc9d354612c49ad).

> [!NOTE]
>
> - Os custos foram estimados com base no plano **on-demand** de 1 ano.
> - Região utilizada: **US East (N. Virginia/us-east-1)**.
>
> **\*\*\*: O RDS será utilizado durante a migração e modernização**

### Preparação

É durante a etapa de preparação que iremos configurar todas os nossos serviços para iniciar a migração dos dados e aplicações para a **AWS**:

| Serviço                                         | Configuração                                                                                             |
| ----------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| **IAM (Identity and Access Management)**        | Configuração do controle de acesso com políticas de menor privilégio e autenticação multifatorial (MFA). |
| **VPC, Subnets, Route Tables, Security Groups** | Configuração das regras de acesso e saída para maior segurança.                                          |
| **VPN/VPN Connection**                          | Configuração de VPN para conexão segura entre rede on premise e a AWS.                                   |
| **AWS Backup**                                  | Configuração de políticas de backup automatizado para bancos de dados, volumes EBS e instâncias EC2.     |
| **DMS (Database Migration Service)**            | Configuração para a migração do banco de dados.                                                          |
| **MGN (Application Migration Service)**         | Configuração para a replicação dos servidores.                                                           |

### Migração

| **Serviço/Etapa**                        | **Configuração/Descrição**                                                                                                 |
| ---------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| **Instalação do AWS MGN Agent**          | Instalação do **Agente AWS MGN (Application Migration Service)** nos servidores locais para replicação.                    |
| **AWS DMS (Database Migration Service)** | Utilização do **AWS DMS (Database Migration Service)** para migração do banco de dados MySQL do ambiente local para a AWS. |

## Modernização

A modernização será realizada em quatro fases:

1. Containerização das Aplicações

   - Containerizar as **API's** e **Frontend** utilizando **Containers**.
   - Criar **Dockerfile** para cada serviço e definir as dependências.
   - Armazenar e versionar as imagens de containers no **ECR** para facilitar o deploy no **EKS**.

2. Armazenamento e Persistência

   - Utilizar arquivos estáticos no **S3** com **CloudFront** para distribuição rápida.
   - Utilizar **RDS MySQL** _(Multi-AZ)_ com réplica para garantir tolerância a falhas.
   - Configurar **AWS Backup** para proteger os dados armazenados no **RDS** com políticas de backup automatizadas.

3. Segurança e Compliance

   - Controle de acesso com **IAM** e **Security Groups**.
   - Segurança na rede com **AWS WAF** e regras de **VPC** _(Subnet e Route Table)_.
   - Criptografia de dados com **KMS**.
   - Monitoramento de segurança com **CloudWatch**.
   - Configurar **SNS** para alertas em caso de falhas, segurança ou uso incorreto dos recursos.

4. Orquestração e Deploy no Amazon EKS

   - Criar clusters com **EKS** para gerenciar os containers.
   - Definir as configurações do **Kubernetes** _(Deployments, Services e ConfigMaps)_.
   - Configurar um **Application Load Balancer (ALB)** para gerenciar o tráfego.
   - Habilitar **Auto Scaling** para escalar automaticamente os pods conforme a demanda.

#### Diagrama de Modernização:

<div align="center">

![Diagrama da Modernização](./assets/AWS-Modernizacao.png)

</div>

#### Custo (Modernização)

|                                                       -                                                        | **Serviço**     | **Custo (Mensal)** | **Custo (Anual)** |
| :------------------------------------------------------------------------------------------------------------: | --------------- | -----------------: | ----------------: |
|       <img src="https://icon.icepanel.io/AWS/svg/Containers/Elastic-Kubernetes-Service.svg" width="40">        | EKS             |       ~ 146.00 USD |       ~ 1,752 USD |
|           <img src="https://icon.icepanel.io/AWS/svg/Storage/Simple-Storage-Service.svg" width="40">           | S3              |         ~ 0.58 USD |        ~ 6.96 USD |
| <img src="https://icon.icepanel.io/AWS/svg/Networking-Content-Delivery/Elastic-Load-Balancing.svg" width="40"> | ALB             |        ~ 22.27 USD |      ~ 267.24 USD |
|                    <img src="https://icon.icepanel.io/AWS/svg/Database/RDS.svg" width="40">                    | RDS (MySQL) (2) |     ~ 1,145.42 USD |   ~ 13,745.04 USD |
|                   <img src="https://icon.icepanel.io/AWS/svg/Storage/Backup.svg" width="40">                   | AWS Backup      |         ~ 1.08 USD |       ~ 12.96 USD |
| <img src="https://icon.icepanel.io/AWS/svg/Networking-Content-Delivery/Virtual-Private-Cloud.svg" width="40">  | VPC             |        ~ 83.00 USD |         ~ 996 USD |
|          <img src="https://icon.icepanel.io/AWS/svg/Security-Identity-Compliance/WAF.svg" width="40">          | WAF             |        ~ 44.00 USD |         ~ 528 USD |
|    <img src="https://icon.icepanel.io/AWS/svg/Security-Identity-Compliance/Secrets-Manager.svg" width="40">    | Secrets Manager |         ~ 0.40 USD |         ~ 4.8 USD |
|        <img src="https://icon.icepanel.io/AWS/svg/Containers/Elastic-Container-Service.svg" width="40">        | ECR             |         ~ 5.00 USD |          ~ 60 USD |
|    <img src="https://icon.icepanel.io/AWS/svg/App-Integration/Simple-Notification-Service.svg" width="40">     | SNS             |         ~ 3.32 USD |       ~ 39.84 USD |
|       <img src="https://icon.icepanel.io/AWS/svg/Networking-Content-Delivery/CloudFront.svg" width="40">       | CloudFront      |        ~ 11.87 USD |      ~ 142.44 USD |
|          <img src="https://icon.icepanel.io/AWS/svg/Management-Governance/CloudWatch.svg" width="40">          | CloudWatch      |         ~ 9.10 USD |       ~ 109.2 USD |
|        <img src="https://icon.icepanel.io/AWS/svg/Networking-Content-Delivery/Route-53.svg" width="40">        | Route 53        |         ~ 6.30 USD |          ~ 78 USD |
|                                                       -                                                        | TOTAL           |   **1,478.54 USD** | **17,742.48 USD** |

> Link para a estimativa: [Modernização na AWS](https://calculator.aws/#/estimate?id=0ad294f27823276c56b35c89bf9456e036e91fdb).

## Referências

- https://docs.aws.amazon.com/mgn/
- https://docs.aws.amazon.com/dms/
- https://www.youtube.com/watch?v=8CABO6FdzwU&ab_channel=AmazonWebServices
- https://www.youtube.com/watch?v=bJCmZn9fASM&ab_channel=DigitalCloudTraining
