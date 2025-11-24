# das-2-2025-2

Resumo da disciplina Design e Arquitetura de Software II (2025/2)  
Projeto prático: AWS Cloud Architecting

---

## AWS Well-Architected Framework

- **Pilares:**

  - Operational Excellence: melhoria contínua, automação, infra como código
  - Security: identidade forte, criptografia, rastreabilidade, segurança em todas as camadas
  - Reliability: recuperação rápida, tolerância a falhas, escalabilidade
  - Performance Efficiency: uso eficiente de recursos, auto scaling, novas tecnologias
  - Cost Optimization: monitorar, eliminar desperdícios, pagar pelo uso
  - Sustainability: uso sustentável dos recursos

- **Well-Architected Tool:** avalia se a arquitetura está adequada para a nuvem
- **Trade-offs:** abrir mão de consistência por performance, escalabilidade x custo

---

## Infraestrutura Global AWS

- **Regiões:** áreas geográficas com várias AZs (Availability Zones)
- **AZ:** conjunto de data centers interconectados, alta disponibilidade
- **Local Zone:** regiões menores, conectadas a uma AZ principal
- **Wavelength:** servidores próximos a antenas 5G
- **Edge Locations / PoPs:** pontos de presença para CDN (CloudFront), baixa latência

---

## Segurança na AWS

### Resource Based Policy

Políticas associadas diretamente a recursos (ex: buckets S3, filas SQS), permitindo definir quem pode acessar ou modificar aquele recurso, independente da identidade do usuário. Exemplo: política de acesso público ou restrito em um bucket S3.

### Identity Based Policy

Políticas associadas diretamente a usuários, grupos ou roles dentro do IAM Policies. Definem permissões específicas para identidades, controlando o que cada usuário pode acessar ou modificar na AWS.

### Determinação de Permissões (Deny)

Ao avaliar permissões no momento da requisição, se houver qualquer política com "Deny" explícito, a ação é negada, independentemente de outras permissões "Allow". O "Deny" sempre prevalece.

- **Modelo de responsabilidade compartilhada:** AWS x Cliente
- **IaaS, PaaS, SaaS:** níveis de responsabilidade
- **Princípios de segurança:**

  - Privilégio mínimo
  - MFA
  - Rotação de credenciais
  - Proteção do usuário root
  - CloudTrail (auditoria)
  - AWS Organizations
  - Criptografia em trânsito e em repouso
  - Segurança em todas as camadas
  - Automação de processos de segurança

- **IAM:**

  - Users, Groups, Roles, Policies
  - MFA
  - Permissões granulares (identity/resource based)
  - Roles para credenciais temporárias

- **Autenticação x Autorização:**
  - Autenticação: quem é você (senha, MFA, etc)
  - Autorização: o que pode fazer (policies)

---

## Armazenamento AWS

### S3 (Simple Storage Service)

- **Tipos:** Block, File, Object Storage (foco em Object)
- **Características:**
  - Virtualmente ilimitado
  - Buckets globais, mas localizados em regiões
  - 5TB por objeto
  - URL única por objeto
  - Prefixos simulam pastas
  - Versionamento (opcional, não pode ser desabilitado)
  - Storage Classes: Standard, Intelligent Tiering, Infrequent Access, Glacier, etc
  - Multipart upload, Transfer Acceleration
  - CORS: controle de acesso entre domínios
  - Inventário S3: relatório de objetos
  - Usos: sites estáticos, backup, disaster recovery

### EBS (Elastic Block Store)

- **Disco persistente** para EC2, pode ser movido entre instâncias, monitoramento de saúde, backup

### Instance Store

- **Disco temporário** (cache, buffer), não persiste após desligar a VM

### EFS (Elastic File System)

- **File share elástico** para Linux, NFS, petabytes, multi-AZ, leitura/escrita simultânea

### FSx

- **File share multipropósito** (Windows, NetApp, OpenZFS, Luster HPC), não elástico automático

---

## Computação AWS

### EC2 (Elastic Compute Cloud)

- **Máquinas virtuais** (VMs), escalabilidade vertical/horizontal, tipos de instância, AMI, SSH

* **Máquinas virtuais** (VMs), escalabilidade vertical/horizontal, tipos de instância (Linux e Windows), AMI, SSH

- **Máquinas virtuais** (VMs), escalabilidade vertical/horizontal, tipos de instância, AMI, SSH
- **Modelos de preço:** On-demand, Reserved, Spot, Savings Plans
- **Placement Groups:** Cluster (alta performance), Spread (alta disponibilidade), Partition (meio termo)

### Acesso via SSH

## Permite acessar e administrar instâncias EC2 de forma segura, utilizando chaves públicas/privadas. Fundamental para operações em servidores Linux e também possível em instâncias Windows (via RDP ou SSH, se habilitado).

## Labs e Exercícios

- [Module 2 Knowledge Check (IAM)](https://awsacademy.instructure.com/courses/113113/assignments/1270651?module_item_id=10653588)
- [Guided Lab: Exploring AWS Identity and Access Management (IAM)](https://awsacademy.instructure.com/courses/113113/assignments/1270605?module_item_id=10653616)
- [Module 3 Knowledge Check](https://awsacademy.instructure.com/courses/113113/assignments/1270652?module_item_id=10653624)
- [Lab: Creating a Static Website for the Cafe (S3)](https://awsacademy.instructure.com/courses/129676/assignments/1485129?module_item_id=12389220)
- [Guided lab: Introducing Amazon Elastic File System (Amazon EFS)](https://awsacademy.instructure.com/courses/129676/assignments/1485164?module_item_id=12389242)

---

## Exemplo de configuração de ambiente Python no VSCode

Arquivo `.vscode/launch.json` para rodar scripts Python com variáveis de ambiente AWS:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Python: Current File",
      "type": "python",
      "request": "launch",
      "program": "${file}",
      "console": "integratedTerminal",
      "env": {
        "AWS_ACCESS_KEY_ID": "",
        "AWS_SECRET_ACCESS_KEY": ""
      },
      "envFile": "${workspaceFolder}/.env"
    }
  ]
}
```

### Containers

- **EKS/ECS:** Kubernetes/Containers gerenciados
- **Fargate:** Serverless para containers

### VPS

- **LightSail:** VPS simplificado

## **Virtual Private Server (VPS):** servidor virtual compartilhado, onde múltiplos usuários utilizam recursos isolados em um mesmo hardware físico. Exemplo: LightSail (AWS).

## Conceitos e Comandos Úteis

- **ps ax:** comando Linux para listar todos os processos/programas em execução no sistema.

- **Isolamento Lógico na AWS:**

  - A AWS utiliza camadas de isolamento lógico, como Cloud, Região e VPC (Virtual Private Cloud), para garantir separação, segurança e controle de recursos entre diferentes ambientes e clientes.

- **LightSail:** VPS simplificado

### PaaS

- **Elastic Beanstalk:** ambiente gerenciado para apps

### Serverless

- **Lambda:** funções sob demanda, sem gerenciar servidores

---

## Observabilidade e Monitoramento

- **CloudWatch:** logs, métricas, alarmes
- **Monitorar:** uso de recursos, custos, saúde dos discos, segurança

---

## Boas Práticas Gerais

- Projetar serviços, não servidores
- Evitar pontos únicos de falha (replicação, multi-AZ)
- Medir e otimizar custos (desligar recursos não usados, usar serviços gerenciados)
- Escolher corretamente tipo/tamanho de storage e instância
- Usar roles e policies adequadas para cada necessidade

---

## Comandos úteis (exemplo Python)

```sh
cd s3
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

---

## Links úteis

- [AWS Well-Architected Framework](https://aws.amazon.com/pt/architecture/well-architected/)
- [AWS CANVAS](https://awsacademy.instructure.com/courses/129676)

* [Repositório da turma](#)

- [AWS Well-Architected Framework](https://aws.amazon.com/pt/architecture/well-architected/)
- [AWS CANVAS](https://awsacademy.instructure.com/courses/129676)

---

## 24/09 - creating a network environment

- VPC
  - Subnet
    - Privada (FileShare, DB etc)
      - Totalmente isolada
      - NAT (Network Address Translator) Gateway
        - EC2(Subnet Privada) -> private subnet route
          table -> NAT Gateway (Subnet publica) -> public subnet route table -> internet gateway
    - Publica
      - Conecta com ‘internet’ via `internet gateway` (NAT Gateway)
      - Necessita de um IP publico (elastic IP - ip elástico)
- Firewall
  - Porta -> Recurso do sistema operacional que permite que um programa faça requisições para ‘internet’
  - Proteção de rede
  - Network Access Control List (NACL)
    - Estatico e stateless
  - Security Group
    - Taggeia os pacotes, caso a conexão seja feita
    - statefull

-22/10/2025

-route 53 routing policies:

- Simple routing policy: uma única resposta para cada consulta DNS.
- Weighted routing policy: distribui o tráfego entre várias instâncias com base em pesos definidos.
- Latency routing policy: direciona o tráfego para a região com menor latência.
- Failover routing policy: redireciona o tráfego para uma instância de backup em caso de falha.
- Geolocation routing policy: direciona o tráfego com base na localização geográfica do usuário.
- Geoproximity routing policy (with traffic bias): semelhante à geolocation, mas permite ajustar o tráfego com base na proximidade.
- Multi-value answer routing policy: permite retornar várias respostas para uma única consulta DNS.

- route 53 public and private hosted zones:

  - public hosted zone: gerencia o tráfego DNS para um domínio acessível publicamente na internet.
    record sets:
    record types:

    - A (Address) record: mapeia um nome de domínio para um endereço IPv4.
    - AAAA record: mapeia um nome de domínio para um endereço IPv6.
    - CNAME (Canonical Name) record: mapeia um nome de domínio para outro nome de domínio.
    - MX (Mail Exchange) record: especifica os servidores de e-mail responsáveis por receber e-mails para o domínio.
    - TXT (Text) record: armazena informações de texto, frequentemente usado para verificação de domínio e políticas de e-mail.
    - NS (Name Server) record: especifica os servidores DNS autoritativos para o domínio.
    - SRV (Service) record: define a localização de serviços específicos, como servidores SIP ou LDAP.
    - PTR (Pointer) record: usado para mapeamento reverso, associando um endereço IP a um nome de domínio.

  - private hosted zone: gerencia o tráfego DNS para um domínio acessível apenas dentro de uma VPC (Virtual Private Cloud).

- Automating your architecture

  - IaC overview
    - IaC benefits
      Template (json, yaml): stack1, 2 e 3, tem como configurar no git(gitops)

  AWS IaC services that use CloudFormation:
  AWS CloudFormation:

  - Aws Elastic Beanstalk (pé de feijao) (((( bastante importante))))
  - AWS quick starts
  - AWS serverless application model (aws sam) (((( bastante importante))))
  - AWS Amplify
  - AWS Cloud development Kit (AWS CDK)

## Aula 29/10
- Caching content
    - Cache Estático (CloudFront) -> pega conteúdo da edge location mais próxima
    - Cache Dinâmico / Banco de Dados -> pega conteúdo de uma camada de banco de dados em memória
    - Caching com Cloudfront
        - Content Delivery Network -> rede global de servidores para entregar serviços comumente acessados
        - Cache principalmente de: Imagens, html css e js, vídeos
        - Provê uma camada com cache para evitar realizar consultas diretas com a AWS
        - User -> Edge Location -> edge cache regional -> origem
        - Permite a maior parte do caminho ser feita dentro da rede da aws
        - TTL do cache do cloudfront é 24h, mas esse valor é configurável
        - Mitigação de DDoS integrada
    - ElastiCache
        - Ideal para acelerar suas consultas de banco
        - Colocado em uma camada na frente do banco
        - Memcahed -> chave valor, alta performance, básico
        - Redis -> escreve em disco, suporta tipos de dados complexos, publish/subscribe, ordenaçãoe ranqueamento
        - Valkey -> fork do Redis antes dele ficar pago
        - Lazy loading -> busca informação no cache, se não tiver, procura na camada sucessiva
        - Write through -> escreve no BD e depois atualiza o cache.

## Aula 12/11
- Serverless
    - Lambda (compute), fargate, cognito, amplify, cloudfront, api gateway, appsync, sns, sqs, eventbridge, functions, s3, efs, neptune, dynamodb, aurora, redshift, opensearch
    - Microsserviços
    - Lambda
        - Serviço computacional serverless
        - Limite de 15 min
        - Limite de 10gb de memória
        - Funciona com base de uma micro vm gerada com o firecracker
        - A lambda se integra com sua rede (vpc)
        - Lambda@Edge: dentro do cloudfront, permite configurar requisições antes de entregá-las
        - Processamento síncrono (api) e assíncrono (eventos) e streaming
    - Contâiner
        - Elastic Container Registry, Elastic Container Service, Elastic Kubernetes Service
    - Fargate
        - Abstrai as complexidades do docker
        - Cria a imagem no ecr -> ECS: cluster task definition-> ECS: cria a task ou serviço (conjunto de tasks) -> Fargate: Container
        - ECR: imagem -> EKS: PodSpec -> Fargate: Pod com contâineres -> EKS: Service
        - ECS: Simplicidade, EKS: Complexo
    - Step Function
        - Serverless workflow
        - Low code, no code
    - API Gateway
        - Na frente da API
        - Expõe o API gateway para conectar ao backend
        - REST, Http e Web Socket
      
