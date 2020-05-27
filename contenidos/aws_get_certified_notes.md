# AWS Get Certified - AWS Certified Developer - Associate

* The Exam - What to Expect
  * Domain 1 - Deployment (22%)
  * Domain 2 - Security (26%)
  * Domain 3 - Developing with AWS (30%)
  * Domain 4 - Refactoring (10%)
  * Domain 5 - Monitoring and Troubleshooting (12%)

(You can fail individual domains) [Más info](https://www.testpreptraining.com/blog/how-to-pass-aws-certified-developer-associate-exam/)

---

# 1. Deployment
* Learning pipelines, CI/CD tools
* Deploy applications using AWS Elastic Beanstalk
* Deploy serverless applications

### Release process
1. Source
2. Build (Compile + Unit tests)
3. Test (Integration tests)
4. Deploy
5. Monitor

#### CI/CD
* Continuous Deployment = Continuous Integration + Continuous Delivery

## Code services
1. Source -> AWS CodeCommit
2. Build  -> AWS CodeBuild
3. Test
4. Deploy -> AWS CodePipeline
5. Monito -> AWS X-Ray

* Todas estas fases pueden ser abarcadas por **AWS CodePipeline**

## AWS Elastic Beanstalk

### Components
* Environment
* Application versions
* Configuration

### Permission Model
* Service role
* Instance role

(...)

## AWS CloudFormation (IaaC -> Infrastructure as Code)

### Templates
* Define the structure to create
* JSON or YAML
* Sections
  * Version
  * Description
  * Metadata
  * Mappings
  * Conditions
  * **Resources** (Es la única obligatoria)
  * Parameters
  * Outputs
  * (...)

### Stack
* Rollback Policy

## Serverless Computing
### Compute
* AWS Lambda

### APIProxy
* Amazon API Gateway

### Storage
* Amazon S3

### Database
* Amazon DynamoDB

### Interprocess Messaging
* Amazon SNS
* Amazon SQS

### Orchestration
* AWS Step Functions

### Analytics
* Amazon Kinesis
* Amazon Athena

### Developer Tools
* Tooling (...)


## AWS Serverless Application Model (SAM)
(...)

## AWS Lambda

### Event Sources That Triggers AWS Lambda
* Data Stores
  * S3
  * DynamoDB
  * Kinesis
  * Cognito

* Endpoints
  * API Gateway
  * IoT
  * Step Functions
  * Alexa

* Development and management tools
  * CloudFormation
  * CloudTrail
  * CodeCommit
  * CloudWatch 

* Event and Message Services
  * SES
  * SNS
  * Cron events
  * SQS

## Scaling
* Scaling out is better then scaling up
  * Vertical Scaling vs Horizontal Scaling

--- 

# 2. Security

## Virtual Private Cloud (VPC)
* Subnet
* Network ACL
* Route table
* Security group
* VPN
* VPC flow logs


## Data and Application

* Server-side encryption
  * HTTPS
* Client-side encryption
  * Amazon S3 - Managed Keys SSE-S3
  * KMS - Managed Keys SSE-KMS ($$)
  * Customer - Managed Keys SSE-C

* AWS Key Management Service
  * Permite Key Rotation

## Identity Access Management (IAM)
* Users
* Groups
* Roles
* Policy

> Es una mala práctica utilizar la cuenta ROOT

## Security Token Service

### Identity Federation
 * External identities (sin necesidad de crear usuarios de IAM)
 * SSO Federation Using SAML

## Keep in mind
* Prefer IAM Roles to access keys
* Security groups only allow

---

# 3. Development with AWS
* Know how to deploy code
* Know how to use CLI

## S3
* Choose the Bucket closest to you
* Each **Object** has **unique key** (Max. size 5 Gb de una sola vez)

### ACLs (Access Control List)
* Give Bucket policies to users (*What Actions to Which Resources*)
*arn:aws:SERVICE:NUMBER:/...*

## Dynamo DB
* NoSQL
* Tablas
  * Items -> Rows/Registros
  * Attributes -> Columns
  * Partition Key (*Index/Clave ÚNICA*)
  * Sort Key (*clave por la que se puede buscar*)
  * Secondary Indexes (clave alternativa)

### Keep In Mind
* Data consistency
* Características
  * Read Capacity Unit (RCUs): 1 RCU/s -> 4 KB/s
  * Write Capacity Unit (WCUs): 1 WCU/s -> 1 KB/s
  * **Eventually consistent** -> significa la **MITAD**

### Streams
### Data Replication
* Répica de datos (con **STREAMS** entre tablas de **distintas regiones**)


* **SCAN vs QUERY**
  * SCAN: Busca por **TODOS** los elementos de la tabla
  * QUERY: Buscar por la partition key


## SNS
* Topic, subscriber
* PUB-SUB (publisher-subscriber)
* Message not persistent


## SQS
* 1 - 1 (1 sender 1 reciever)
* Polling
* Message persistent

* RecieveMessageWaitTime -> how long waits until is avaiable~

## StepFunctions
* Uses Amazon States Language (JSON)

## API Gateway
* Es una de las maneras de conectar tus servicios de AWS con *el mundo*.

## CloudFront
* *Cache* de contenido estático (de un S3)
  * *ElastiCache*
    * Lazy Loading -> Guarda en caché únicamente cuando es necessario
    * Write Through -> Cada vez que se actualizan los datos, se actualiza la caché


## ECS (Elastic Container Services)
* Deploy Containers

## Development Tools
* SDKs
* Command Line Tools

---

# 4. Refactoring

* Optimize application
* Migrate existing application

### Anti-pattern
* Los usuarios experiencian un crash y manualmente avisan al admin que éste revisa manualmente el error (...)

### Best practices
* **Cloudwatch** detecta los posibles crashes y notifica al admin  (...)

## Diseñar servicios, no servidores
* No limitar la infrastructura a los servidores

### Anti-pattern
* Application running on persistent servers
* Application communicate with each other
* Static web assets are stored locally on instances
* Instances handle user authentication

### Best practices
* Serverless solutions
* Message queue to handle communication between applications
* Static web assets stored external services like Amazon S3
* AWS handles user authentication

## Avoid Single points of Failure
* Tener réplicas que puedan realizar el trabajo

## Caching
* Use CloudFront to distribute the cached files (It autodetects the zone to deliver the files)
* Do **NOT** use S3 to distribute files (and having multiple Buckets depending on the Zones)

## The 6 R's
* Rehost
* Replatform
* Repurchase
* Refactor
* Retain
* Retire
  
## Microservicios
* Descomponer una aplicación *Monolítica* en microservicios.
  * **NO** tener un único servidor que realiza todas las funciones
  * **SI** tener pequeños servicios que se comunican entre ellos y que realizan pequeñas tareas formando una aplicación en su conjunto.

## Keep In Mind
* **Durabilidad vs Disponibilidad**
  * Durabilidad: Que tus datos perduren, no se puedan perder
  * Disponibilidad: Asegurarte que siempre que quieras vas a poder consultar tus datos
* **Escalabilidad vs Elasticidad**
  * Escalabilidad: Como se puede "mejorar" la aplicación en cuanto a demanda
  * Elasticidad: Cómo puede estar sujeta a cambios la aplicación
* Migrar a **microservicios**!

---

# 5. Monitoring and Troubleshooting 

## General
* Visualizar los errors obtenidos por AWS

## CloudWatch
* Resource monitoring
* Standard and custom metrics

## CloudTrail
* Histórico de cambios/modificaciones de la cuenta de AWS
* Registro de actividad

---


# Q&A

1. 
    * **Q:**
        What would be the advantages of using an Elastic Beanstalk solution over deploying an application using Api Gateway and Lambda Functions?
    * **A:**
        @arturo - Lambda has an execution limit of 15 min

---
2. 
    * **Q:**
        Is AWS CLI based questions are asked in the Developer Associate exam?
    * **A:** 
        I would familiarize yourself with it but no super specific questions will be asked