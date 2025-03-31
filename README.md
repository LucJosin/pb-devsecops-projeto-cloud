<h3 align="center">< Projeto Cloud /></h3>

<h1 align="center">
    <img align="center" src="https://logospng.org/download/uol/logo-uol-icon-256.png" width="30" height="30" /> Compass UOL - DevSecOps
</h1>

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

- Ambiente Kubernetes
- Banco de dados gerenciado (PaaS e Multi-AZ)
- Backup de dados
- Sistema para persistência de objetos (imagens, vídeos etc.)
- Requisitos de segurança avançados

## Migração

### Planejamento para a Migração

Comparando os serviços:

| Serviço        | On premise       | AWS           | Descrição |
| -------------- | ---------------- | ------------- | --------- |
| Frontend       | Servidor (React) | EC2           | Descrição |
| Banco de Dados | Servidor (MySQL) | RDS (MySQL)   | Descrição |
| NGinx          | Servidor (NGinx) | Load Balancer | Descrição |
| Arquivos       | Servidor         | S3            | Descrição |

Serviços extras:

| Serviço                    | Descrição |
| -------------------------- | --------- |
| DMS                        | Descrição |
| MGN                        | Descrição |
| EBS                        | Descrição |
| VPC (Subnets, Route Table) | Descrição |

### Passo a passo

#### Preparação dos Serviços

#### Migração do Banco de Dados

1. Preparação
2. Migração

#### Migração dos Aplicação + Arquivos

1. Preparação
2. Migração

## Modernização

## Referências

- https://docs.aws.amazon.com/mgn/
- https://docs.aws.amazon.com/dms/
- https://www.youtube.com/watch?v=8CABO6FdzwU&ab_channel=AmazonWebServices
- https://www.youtube.com/watch?v=bJCmZn9fASM&ab_channel=DigitalCloudTraining

> Apagar depois

## Migração

- MGN
- DMS
- S3
- EC2
- RDS
- EBS

## Serviços

- Application Migration Service
- Database Migration Service
- DataSync
- S3
- EC2
- RDS
- Elastic Block Store
- Load Balance
- NAT Gateway
- Internet Gateway
- WAF
- Route 53
- CloudFront
- CloudWatch
