# **Índice**

1. **Introdução ao Projeto**
   - Visão Geral
   - Objetivos do Projeto
2. **Módulo 1: Preparação do Ambiente de Desenvolvimento**
   - 1.1. Instalação das Ferramentas Necessárias
     - Visual Studio Code (VSCode)
     - Docker Desktop
     - Terraform
     - AWS CLI
   - 1.2. Configuração do AWS CLI
3. **Módulo 2: Conceitos Fundamentais**
   - 2.1. Introdução à AWS
   - 2.2. Conceitos de Rede (VPC, Sub-redes, Internet Gateway)
   - 2.3. Serviços AWS Utilizados (ECS, RDS, ALB, WAF)
   - 2.4. Infraestrutura como Código (Terraform)
   - 2.5. Contêineres e Docker
   - 2.6. GitHub Actions
4. **Módulo 3: Desenvolvimento Local com Docker**
   - 3.1. Criando o Diretório do Projeto
   - 3.2. Criando o Dockerfile
   - 3.3. Construindo e Testando a Imagem Docker Localmente
5. **Módulo 4: Definição e Provisionamento da Infraestrutura com Terraform**
   - 4.1. Estrutura do Projeto Terraform
   - 4.2. Configurando o Provedor AWS
   - 4.3. Definindo Variáveis e Outputs
   - 4.4. Criando a VPC e Sub-redes
   - 4.5. Configurando o Internet Gateway e Rotas
   - 4.6. Configurando Grupos de Segurança (Security Groups)
   - 4.7. Configurando o Banco de Dados RDS
   - 4.8. Configurando o Amazon ECS e ECR
   - 4.9. Configurando o Application Load Balancer (ALB)
   - 4.10. Configurando o AWS WAF
   - 4.11. Inicializando e Aplicando o Terraform
6. **Módulo 5: Enviando a Imagem Docker para o Amazon ECR**
   - 5.1. Autenticando-se no ECR
   - 5.2. Marcando e Enviando a Imagem
   - 5.3. Atualizando a Definição de Tarefa do ECS
7. **Módulo 6: Configurando o Pipeline de CI/CD com GitHub Actions**
   - 6.1. Conceitos do GitHub Actions
   - 6.2. Configurando o Repositório no GitHub
   - 6.3. Configurando as Credenciais da AWS no GitHub
   - 6.4. Criando o Workflow do GitHub Actions
   - 6.5. Testando o Pipeline
8. **Módulo 7: Aquisição de Domínio e Configuração de DNS**
   - 7.1. Adquirindo um Domínio
   - 7.2. Configurando o DNS com o Amazon Route 53
9. **Módulo 8: Configurando SSL/TLS com o AWS Certificate Manager**
   - 8.1. Solicitando um Certificado SSL/TLS
   - 8.2. Configurando o ALB para Usar HTTPS
   - 8.3. Redirecionando Tráfego HTTP para HTTPS
10. **Módulo 9: Finalização e Testes**
    - 9.1. Acessando o Site via HTTPS
    - 9.2. Concluindo a Instalação do WordPress
    - 9.3. Testando Funcionalidades
11. **Módulo 10: Manutenção e Próximos Passos**
    - 10.1. Monitoramento e Otimização
    - 10.2. Segurança e Backups
    - 10.3. Escalabilidade e Auto Scaling
    - 10.4. Aprimoramentos Futuros
12. **Conclusão**

---

# **Introdução ao Projeto**

## **Visão Geral**

Neste projeto, vamos desenvolver um site de e-commerce para uma empresa de joias em prata, utilizando o **WordPress** como plataforma. O site será hospedado na **AWS**, aproveitando serviços gerenciados para garantir escalabilidade, segurança e alta disponibilidade.

Usaremos o **Docker** para containerizar a aplicação, o **Terraform** para definir a infraestrutura como código e o **GitHub Actions** como ferramenta de CI/CD para automatizar o processo de build e deploy. Também integraremos o **AWS WAF** para aumentar a segurança da aplicação.

## **Objetivos do Projeto**

- Configurar um ambiente de desenvolvimento local.
- Criar uma imagem Docker personalizada do WordPress.
- Definir e provisionar a infraestrutura na AWS usando o Terraform.
- Enviar a imagem Docker para o Amazon ECR.
- Configurar um pipeline de CI/CD com GitHub Actions.
- Adquirir um domínio personalizado e configurar o DNS.
- Implementar SSL/TLS com o AWS Certificate Manager.
- Integrar o AWS WAF para proteção contra ameaças web.
- Testar e validar a funcionalidade do site.
- Preparar o ambiente para manutenção e futuros aprimoramentos.

---

# **Módulo 1: Preparação do Ambiente de Desenvolvimento**

## **1.1. Instalação das Ferramentas Necessárias**

Para desenvolver e implantar nosso projeto, precisaremos das seguintes ferramentas:

### **1.1.1. Visual Studio Code (VSCode)**

**O que é?**

Um editor de código-fonte gratuito e leve, com suporte a extensões e recursos avançados.

**Como instalar:**

1. Acesse [https://code.visualstudio.com/download](https://code.visualstudio.com/download).
2. Baixe a versão para o seu sistema operacional (Windows, macOS ou Linux).
3. Execute o instalador e siga as instruções.

**Dicas:**

- Instale extensões úteis como **Docker**, **Terraform**, **YAML**, e **GitHub Actions** para facilitar o desenvolvimento.

### **1.1.2. Docker Desktop**

**O que é?**

Uma plataforma para desenvolver, enviar e executar aplicações em contêineres.

**Como instalar:**

1. Acesse [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop).
2. Baixe a versão para o seu sistema operacional.
3. Execute o instalador e siga as instruções.
   - No Windows, habilite o WSL 2 (Windows Subsystem for Linux) se solicitado.

**Verificação:**

- Abra um terminal e execute `docker --version` para confirmar a instalação.

### **1.1.3. Terraform**

**O que é?**

Uma ferramenta para definir e provisionar infraestrutura usando arquivos de configuração declarativos.

**Como instalar:**

1. Acesse [https://www.terraform.io/downloads.html](https://www.terraform.io/downloads.html).
2. Baixe o pacote para o seu sistema operacional.
3. Extraia o executável e adicione-o ao PATH do sistema.

**Verificação:**

- Abra um terminal e execute `terraform --version` para confirmar a instalação.

### **1.1.4. AWS CLI**

**O que é?**

Uma ferramenta para gerenciar serviços da AWS via linha de comando.

**Como instalar:**

1. Acesse [https://aws.amazon.com/pt/cli/](https://aws.amazon.com/pt/cli/).
2. Baixe e execute o instalador para o seu sistema operacional.
3. Siga as instruções do instalador.

**Verificação:**

- Execute `aws --version` no terminal para confirmar a instalação.

---

## **1.2. Configuração do AWS CLI**

### **1.2.1. Criar uma Conta na AWS**

Se você ainda não possui uma conta AWS:

1. Acesse [https://aws.amazon.com/pt/](https://aws.amazon.com/pt/).
2. Clique em **Criar uma conta da AWS** e siga as instruções.
   - Você precisará fornecer informações pessoais e um cartão de crédito para verificação.
   - A AWS oferece um nível gratuito que pode ser útil para testes.

### **1.2.2. Criar um Usuário IAM com Acesso Programático**

1. Acesse o **Console de Gerenciamento da AWS**.
2. Navegue para o serviço **IAM** (Gerenciamento de Identidade e Acessos).
3. Clique em **Usuários** no menu à esquerda.
4. Clique em **Adicionar usuário**.
5. Defina um nome de usuário, por exemplo, `terraform-user`.
6. Selecione **Acesso programático**.
7. Clique em **Próximo: Permissões**.
8. Anexe a política **AdministratorAccess**.
   - **Atenção:** Em produção, atribua apenas as permissões necessárias.
9. Clique em **Próximo: Tags**, depois **Próximo: Revisar** e **Criar usuário**.
10. Anote o **ID da chave de acesso** e a **Chave de acesso secreta**.

### **1.2.3. Configurar o AWS CLI com as Credenciais**

1. Abra um terminal.
2. Execute `aws configure`.
3. Insira:
   - **AWS Access Key ID:** (ID da chave de acesso)
   - **AWS Secret Access Key:** (Chave de acesso secreta)
   - **Default region name:** `us-east-1` (ou sua região preferida)
   - **Default output format:** `json` (ou deixe em branco)

**Verificação:**

- Execute `aws sts get-caller-identity` para confirmar que as credenciais estão funcionando.

---

# **Módulo 2: Conceitos Fundamentais**

## **2.1. Introdução à AWS**

A Amazon Web Services (AWS) é uma plataforma de computação em nuvem que oferece serviços de infraestrutura e plataforma sob demanda. Vamos utilizar vários serviços da AWS para hospedar nossa aplicação.

## **2.2. Conceitos de Rede**

- **VPC (Virtual Private Cloud):** Rede virtual privada onde você define seu próprio espaço de endereço IP.
- **Sub-redes:** Segmentos dentro da VPC para organizar recursos.
  - **Sub-rede Pública:** Acessível pela internet.
  - **Sub-rede Privada:** Não acessível diretamente pela internet.
- **Internet Gateway:** Permite comunicação entre a VPC e a internet.
- **Roteamento e Tabelas de Rotas:** Controlam o fluxo de tráfego dentro da VPC.

## **2.3. Serviços AWS Utilizados**

- **Amazon ECS (Elastic Container Service):** Orquestração de contêineres Docker.
- **AWS Fargate:** Permite executar contêineres sem gerenciar servidores.
- **Amazon RDS (Relational Database Service):** Banco de dados gerenciado.
- **Application Load Balancer (ALB):** Balanceamento de carga de nível de aplicação.
- **AWS WAF (Web Application Firewall):** Proteção contra ameaças web.
- **Amazon ECR (Elastic Container Registry):** Armazenamento de imagens Docker.
- **Amazon Route 53:** Gerenciamento de DNS.
- **AWS Certificate Manager (ACM):** Gerenciamento de certificados SSL/TLS.

## **2.4. Infraestrutura como Código (Terraform)**

- Permite definir a infraestrutura usando arquivos de configuração.
- Facilita a replicação, gerenciamento e versionamento da infraestrutura.

## **2.5. Contêineres e Docker**

- **Docker:** Plataforma para criar, implantar e executar aplicações em contêineres.
- **Imagens Docker:** Pacotes que contêm tudo o que é necessário para executar uma aplicação.

## **2.6. GitHub Actions**

- Plataforma de automação integrada ao GitHub.
- Permite criar pipelines de CI/CD para automatizar builds, testes e deploys.
- Integra-se facilmente com repositórios do GitHub.

---

# **Módulo 3: Desenvolvimento Local com Docker**

## **3.1. Criando o Diretório do Projeto**

1. Escolha um local no seu computador para o projeto, por exemplo, `C:\projetos\meu-ecommerce`.
2. Abra o VSCode e abra a pasta do projeto.

## **3.2. Criando o Dockerfile**

1. Na raiz do projeto, crie um arquivo chamado `Dockerfile`.
2. Adicione o seguinte conteúdo:

   ```dockerfile
   # Usar a imagem oficial do WordPress
   FROM wordpress:latest

   # Expor a porta 80
   EXPOSE 80
   ```

   **Explicação:**

   - `FROM wordpress:latest`: Usa a imagem oficial do WordPress.
   - `EXPOSE 80`: Indica que o contêiner escuta na porta 80.

## **3.3. Construindo e Testando a Imagem Docker Localmente**

1. Abra um terminal no VSCode.
2. Navegue até o diretório do projeto.
3. Construa a imagem:

   ```bash
   docker build -t meu-wordpress .
   ```

4. Execute o contêiner:

   ```bash
   docker run -d -p 8000:80 meu-wordpress
   ```

5. Abra o navegador e acesse `http://localhost:8000`.

**Nota:** Sem um banco de dados configurado, a instalação do WordPress não será concluída. Nesta etapa, estamos apenas testando se o contêiner está funcionando.

---

# **Módulo 4: Definição e Provisionamento da Infraestrutura com Terraform**

## **4.1. Estrutura do Projeto Terraform**

1. Dentro da pasta do projeto, crie uma pasta chamada `terraform`.
2. Crie os seguintes arquivos dentro de `terraform`:
   - `main.tf`
   - `variables.tf`
   - `outputs.tf`
   - `provider.tf`

## **4.2. Configurando o Provedor AWS**

No `provider.tf`, adicione:

```hcl
provider "aws" {
  region  = var.aws_region
  version = "~> 3.0"
}

variable "aws_region" {
  description = "Região AWS"
  default     = "us-east-1"
}
```

## **4.3. Definindo Variáveis e Outputs**

### **4.3.1. Variáveis**

No `variables.tf`, adicione:

```hcl
variable "project_name" {
  description = "Nome do projeto"
  default     = "meu-ecommerce"
}

variable "vpc_cidr" {
  description = "CIDR da VPC"
  default     = "10.0.0.0/16"
}

variable "public_subnet_cidr" {
  description = "CIDR da sub-rede pública"
  default     = "10.0.1.0/24"
}

variable "private_subnet_cidr" {
  description = "CIDR da sub-rede privada"
  default     = "10.0.2.0/24"
}

variable "db_username" {
  description = "Usuário do banco de dados"
  default     = "wpuser"
}

variable "db_password" {
  description = "Senha do banco de dados"
  default     = "wppassword"
}

variable "db_name" {
  description = "Nome do banco de dados"
  default     = "wordpressdb"
}
```

### **4.3.2. Outputs**

No `outputs.tf`, adicione:

```hcl
output "alb_dns_name" {
  description = "DNS do Application Load Balancer"
  value       = aws_lb.alb.dns_name
}
```

## **4.4. Criando a VPC e Sub-redes**

No `main.tf`, adicione a configuração da VPC e sub-redes.

**VPC:**

```hcl
resource "aws_vpc" "main_vpc" {
  cidr_block           = var.vpc_cidr
  enable_dns_support   = true
  enable_dns_hostnames = true
  tags = {
    Name = "${var.project_name}-vpc"
  }
}
```

**Sub-rede Pública:**

```hcl
resource "aws_subnet" "public_subnet" {
  vpc_id                  = aws_vpc.main_vpc.id
  cidr_block              = var.public_subnet_cidr
  map_public_ip_on_launch = true
  availability_zone       = "${var.aws_region}a"
  tags = {
    Name = "${var.project_name}-public-subnet"
  }
}
```

**Sub-rede Privada:**

```hcl
resource "aws_subnet" "private_subnet" {
  vpc_id            = aws_vpc.main_vpc.id
  cidr_block        = var.private_subnet_cidr
  availability_zone = "${var.aws_region}a"
  tags = {
    Name = "${var.project_name}-private-subnet"
  }
}
```

## **4.5. Configurando o Internet Gateway e Rotas**

**Internet Gateway:**

```hcl
resource "aws_internet_gateway" "igw" {
  vpc_id = aws_vpc.main_vpc.id
  tags = {
    Name = "${var.project_name}-igw"
  }
}
```

**Tabela de Rotas Pública:**

```hcl
resource "aws_route_table" "public_route_table" {
  vpc_id = aws_vpc.main_vpc.id
  tags = {
    Name = "${var.project_name}-public-rt"
  }
}

resource "aws_route" "public_route" {
  route_table_id         = aws_route_table.public_route_table.id
  destination_cidr_block = "0.0.0.0/0"
  gateway_id             = aws_internet_gateway.igw.id
}

resource "aws_route_table_association" "public_subnet_association" {
  subnet_id      = aws_subnet.public_subnet.id
  route_table_id = aws_route_table.public_route_table.id
}
```

## **4.6. Configurando Grupos de Segurança (Security Groups)**

**Security Group para o ALB:**

```hcl
resource "aws_security_group" "alb_sg" {
  name        = "${var.project_name}-alb-sg"
  description = "Security group for ALB"
  vpc_id      = aws_vpc.main_vpc.id

  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port   = 443
    to_port     = 443
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name = "${var.project_name}-alb-sg"
  }
}
```

**Security Group para o ECS:**

```hcl
resource "aws_security_group" "ecs_sg" {
  name        = "${var.project_name}-ecs-sg"
  description = "Security group for ECS tasks"
  vpc_id      = aws_vpc.main_vpc.id

  ingress {
    from_port       = 80
    to_port         = 80
    protocol        = "tcp"
    security_groups = [aws_security_group.alb_sg.id]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name = "${var.project_name}-ecs-sg"
  }
}
```

**Security Group para o RDS:**

```hcl
resource "aws_security_group" "rds_sg" {
  name        = "${var.project_name}-rds-sg"
  description = "Security group for RDS"
  vpc_id      = aws_vpc.main_vpc.id

  ingress {
    from_port       = 3306
    to_port         = 3306
    protocol        = "tcp"
    security_groups = [aws_security_group.ecs_sg.id]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name = "${var.project_name}-rds-sg"
  }
}
```

## **4.7. Configurando o Banco de Dados RDS**

**Grupo de Sub-redes do RDS:**

```hcl
resource "aws_db_subnet_group" "db_subnet" {
  name       = "${var.project_name}-db-subnet-group"
  subnet_ids = [aws_subnet.private_subnet.id]
  tags = {
    Name = "${var.project_name}-db-subnet-group"
  }
}
```

**Instância RDS:**

```hcl
resource "aws_db_instance" "wordpress_db" {
  allocated_storage      = 20
  storage_type           = "gp2"
  engine                 = "mysql"
  engine_version         = "5.7"
  instance_class         = "db.t3.micro"
  name                   = var.db_name
  username               = var.db_username
  password               = var.db_password
  parameter_group_name   = "default.mysql5.7"
  skip_final_snapshot    = true
  db_subnet_group_name   = aws_db_subnet_group.db_subnet.name
  vpc_security_group_ids = [aws_security_group.rds_sg.id]
  multi_az               = false
  publicly_accessible    = false
  storage_encrypted      = true
  tags = {
    Name = "${var.project_name}-db-instance"
  }
}
```

## **4.8. Configurando o Amazon ECS e ECR**

**Cluster ECS:**

```hcl
resource "aws_ecs_cluster" "ecs_cluster" {
  name = "${var.project_name}-cluster"
}
```

**Repositório ECR:**

```hcl
resource "aws_ecr_repository" "wordpress_repo" {
  name = "${var.project_name}-repo"
}
```

**Role IAM para o ECS:**

```hcl
resource "aws_iam_role" "ecs_task_execution_role" {
  name = "${var.project_name}-ecs-task-execution-role"

  assume_role_policy = jsonencode({
    Version = "2012-10-17",
    Statement = [{
      Action = "sts:AssumeRole",
      Effect = "Allow",
      Principal = {
        Service = "ecs-tasks.amazonaws.com"
      }
    }]
  })
}

resource "aws_iam_role_policy_attachment" "ecs_task_execution_role_policy" {
  role       = aws_iam_role.ecs_task_execution_role.name
  policy_arn = "arn:aws:iam::aws:policy/service-role/AmazonECSTaskExecutionRolePolicy"
}
```

**Definição de Tarefa ECS:**

```hcl
resource "aws_ecs_task_definition" "wordpress_task" {
  family                   = "${var.project_name}-task"
  network_mode             = "awsvpc"
  requires_compatibilities = ["FARGATE"]
  cpu                      = "256"
  memory                   = "512"

  execution_role_arn = aws_iam_role.ecs_task_execution_role.arn
  task_role_arn      = aws_iam_role.ecs_task_execution_role.arn

  container_definitions = jsonencode([
    {
      name      = "wordpress"
      image     = "${aws_ecr_repository.wordpress_repo.repository_url}:latest"
      essential = true
      portMappings = [
        {
          containerPort = 80
          hostPort      = 80
          protocol      = "tcp"
        }
      ]
      environment = [
        {
          name  = "WORDPRESS_DB_HOST"
          value = aws_db_instance.wordpress_db.address
        },
        {
          name  = "WORDPRESS_DB_USER"
          value = var.db_username
        },
        {
          name  = "WORDPRESS_DB_PASSWORD"
          value = var.db_password
        },
        {
          name  = "WORDPRESS_DB_NAME"
          value = var.db_name
        }
      ]
    }
  ])
}
```

**Serviço ECS:**

```hcl
resource "aws_ecs_service" "wordpress_service" {
  name            = "${var.project_name}-service"
  cluster         = aws_ecs_cluster.ecs_cluster.id
  task_definition = aws_ecs_task_definition.wordpress_task.arn
  launch_type     = "FARGATE"
  desired_count   = 1

  network_configuration {
    subnets         = [aws_subnet.private_subnet.id]
    security_groups = [aws_security_group.ecs_sg.id]
    assign_public_ip = false
  }

  load_balancer {
    target_group_arn = aws_lb_target_group.wordpress_tg.arn
    container_name   = "wordpress"
    container_port   = 80
  }

  depends_on = [aws_lb_listener.http]
}
```

## **4.9. Configurando o Application Load Balancer (ALB)**

**ALB:**

```hcl
resource "aws_lb" "alb" {
  name               = "${var.project_name}-alb"
  load_balancer_type = "application"
  subnets            = [aws_subnet.public_subnet.id]
  security_groups    = [aws_security_group.alb_sg.id]
  tags = {
    Name = "${var.project_name}-alb"
  }
}
```

**Target Group:**

```hcl
resource "aws_lb_target_group" "wordpress_tg" {
  name        = "${var.project_name}-tg"
  port        = 80
  protocol    = "HTTP"
  target_type = "ip"
  vpc_id      = aws_vpc.main_vpc.id
  health_check {
    path                = "/"
    interval            = 30
    timeout             = 5
    unhealthy_threshold = 2
    healthy_threshold   = 5
    matcher             = "200-399"
  }
  tags = {
    Name = "${var.project_name}-tg"
  }
}
```

**Listener HTTP:**

```hcl
resource "aws_lb_listener" "http" {
  load_balancer_arn = aws_lb.alb.arn
  port              = "80"
  protocol          = "HTTP"

  default_action {
    type             = "forward"
    target_group_arn = aws_lb_target_group.wordpress_tg.arn
  }
}
```

## **4.10. Configurando o AWS WAF**

**Web ACL do WAF:**

```hcl
resource "aws_wafv2_web_acl" "waf" {
  name        = "${var.project_name}-waf"
  description = "WAF para proteger o ALB"
  scope       = "REGIONAL"
  default_action {
    allow {}
  }
  visibility_config {
    sampled_requests_enabled    = true
    cloudwatch_metrics_enabled  = true
    metric_name                 = "${var.project_name}-waf"
  }
  rule {
    name     = "AWS-AWSManagedRulesCommonRuleSet"
    priority = 1
    override_action {
      none {}
    }
    statement {
      managed_rule_group_statement {
        vendor_name = "AWS"
        name        = "AWSManagedRulesCommonRuleSet"
      }
    }
    visibility_config {
      sampled_requests_enabled    = true
      cloudwatch_metrics_enabled  = true
      metric_name                 = "awsCommonRules"
    }
  }
}
```

**Associação do WAF ao ALB:**

```hcl
resource "aws_wafv2_web_acl_association" "waf_association" {
  resource_arn = aws_lb.alb.arn
  web_acl_arn  = aws_wafv2_web_acl.waf.arn
}
```

## **4.11. Inicializando e Aplicando o Terraform**

1. Navegue até a pasta `terraform` no terminal.
2. Inicialize o Terraform:

   ```bash
   terraform init
   ```

3. Verifique a configuração:

   ```bash
   terraform validate
   ```

4. Visualize o plano de execução:

   ```bash
   terraform plan -out=tfplan
   ```

5. Aplique as mudanças:

   ```bash
   terraform apply tfplan
   ```

6. Aguarde a conclusão do provisionamento.

---

# **Módulo 5: Enviando a Imagem Docker para o Amazon ECR**

## **5.1. Autenticando-se no ECR**

No terminal, execute:

```bash
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com
```

Substitua `<AWS_ACCOUNT_ID>` pelo ID da sua conta AWS.

## **5.2. Marcando e Enviando a Imagem**

1. Marque a imagem:

   ```bash
   docker tag meu-wordpress:latest <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/meu-ecommerce-repo:latest
   ```

2. Envie a imagem para o ECR:

   ```bash
   docker push <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/meu-ecommerce-repo:latest
   ```

## **5.3. Atualizando a Definição de Tarefa do ECS**

Certifique-se de que a definição de tarefa no Terraform está apontando para a imagem no ECR com a tag `latest`.

---

# **Módulo 6: Configurando o Pipeline de CI/CD com GitHub Actions**

## **6.1. Conceitos do GitHub Actions**

- **Workflows:** Processos automatizados definidos em arquivos YAML.
- **Jobs:** Conjunto de etapas que serão executadas em um runner.
- **Steps:** Comandos individuais dentro de um job.
- **Actions:** Tarefas reutilizáveis que podem ser usadas nos steps.

## **6.2. Configurando o Repositório no GitHub**

1. Crie um repositório no GitHub para o projeto.
2. Faça o push do código (Dockerfile, arquivos Terraform, etc.) para o repositório.

## **6.3. Configurando as Credenciais da AWS no GitHub**

1. No repositório, vá em **Settings** > **Secrets and variables** > **Actions** > **Secrets**.
2. Adicione os seguintes secrets:
   - **AWS_ACCESS_KEY_ID**
   - **AWS_SECRET_ACCESS_KEY**
   - **AWS_REGION**
   - **ECR_REPOSITORY:** Nome do repositório ECR (por exemplo, `meu-ecommerce-repo`)
   - **ECS_CLUSTER_NAME:** Nome do cluster ECS
   - **ECS_SERVICE_NAME:** Nome do serviço ECS

## **6.4. Criando o Workflow do GitHub Actions**

Crie a pasta `.github/workflows` na raiz do repositório e, dentro dela, crie o arquivo `ci-cd.yml` com o seguinte conteúdo:

```yaml
name: CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ${{ secrets.AWS_REGION }}

      - name: Login to Amazon ECR
        id: login-ecr
        uses: aws-actions/amazon-ecr-login@v1

      - name: Build, tag, and push Docker image to ECR
        env:
          ECR_REGISTRY: ${{ steps.login-ecr.outputs.registry }}
          ECR_REPOSITORY: ${{ secrets.ECR_REPOSITORY }}
          IMAGE_TAG: latest
        run: |
          docker build -t $ECR_REGISTRY/$ECR_REPOSITORY:$IMAGE_TAG .
          docker push $ECR_REGISTRY/$ECR_REPOSITORY:$IMAGE_TAG

      - name: Update ECS service
        uses: aws-actions/amazon-ecs-deploy-task-definition@v1
        with:
          aws-region: ${{ secrets.AWS_REGION }}
          cluster: ${{ secrets.ECS_CLUSTER_NAME }}
          service: ${{ secrets.ECS_SERVICE_NAME }}
          task-definition: ecs-task-def.json
          wait-for-service-stability: true
```

**Notas:**

- **ecs-task-def.json:** Arquivo de definição de tarefa atualizado com a nova imagem. Você pode exportar a definição atual usando `aws ecs describe-task-definition` e atualizar o campo da imagem.

## **6.5. Testando o Pipeline**

1. Faça um commit e push das alterações.
2. No GitHub, vá até a aba **Actions** e verifique se o workflow está sendo executado.
3. Certifique-se de que todas as etapas são concluídas com sucesso.

---

# **Módulo 7: Aquisição de Domínio e Configuração de DNS**

## **7.1. Adquirindo um Domínio**

1. Acesse o **Amazon Route 53** no console da AWS.
2. Clique em **Registrar domínios**.
3. Pesquise pelo domínio desejado e siga as instruções para registrá-lo.
   - **Nota:** O registro pode levar alguns minutos a horas para ser concluído.

## **7.2. Configurando o DNS com o Amazon Route 53**

1. No Route 53, vá em **Zonas Hospedadas** e clique na zona do seu domínio.
2. Crie um registro **A** com o nome do seu domínio e configure-o como um **Alias** para o ALB.
   - Selecione o ALB na lista de destinos.

---

# **Módulo 8: Configurando SSL/TLS com o AWS Certificate Manager**

## **8.1. Solicitando um Certificado SSL/TLS**

1. Acesse o **AWS Certificate Manager** (ACM) no console da AWS.
2. Clique em **Solicitar um certificado**.
3. Escolha **Solicitar um certificado público** e clique em **Próximo**.
4. Insira o seu domínio (por exemplo, `seu-dominio.com`) e variações (como `www.seu-dominio.com`).
5. Escolha o método de validação **DNS**.
6. Revise as informações e clique em **Confirmar e solicitar**.
7. Na próxima tela, clique em **Criar registro no Route 53** para validar o domínio automaticamente.

## **8.2. Configurando o ALB para Usar HTTPS**

No `main.tf`, atualize o listener do ALB para incluir HTTPS:

```hcl
# Listener HTTPS
resource "aws_lb_listener" "https" {
  load_balancer_arn = aws_lb.alb.arn
  port              = "443"
  protocol          = "HTTPS"
  ssl_policy        = "ELBSecurityPolicy-2016-08"
  certificate_arn   = aws_acm_certificate.cert.arn

  default_action {
    type             = "forward"
    target_group_arn = aws_lb_target_group.wordpress_tg.arn
  }
}
```

**Nota:** Você precisará importar o certificado no Terraform:

```hcl
resource "aws_acm_certificate" "cert" {
  domain_name       = "seu-dominio.com"
  validation_method = "DNS"
}
```

## **8.3. Redirecionando Tráfego HTTP para HTTPS**

Atualize o listener HTTP para redirecionar para HTTPS:

```hcl
# Listener HTTP
resource "aws_lb_listener" "http" {
  load_balancer_arn = aws_lb.alb.arn
  port              = "80"
  protocol          = "HTTP"

  default_action {
    type = "redirect"
    redirect {
      protocol   = "HTTPS"
      port       = "443"
      status_code = "HTTP_301"
    }
  }
}
```

---

# **Módulo 9: Finalização e Testes**

## **9.1. Acessando o Site via HTTPS**

- Abra o navegador e acesse `https://seu-dominio.com`.
- Verifique se o certificado SSL está válido e que a conexão é segura.

## **9.2. Concluindo a Instalação do WordPress**

- Siga as instruções na tela para configurar o WordPress.
  - Escolha o idioma.
  - Defina o título do site, nome de usuário, senha e e-mail.

## **9.3. Testando Funcionalidades**

- Faça login no painel de administração.
- Crie posts, páginas e teste temas e plugins.
- Verifique se todas as funcionalidades estão operando corretamente.

---

# **Módulo 10: Manutenção e Próximos Passos**

## **10.1. Monitoramento e Otimização**

- Utilize o **Amazon CloudWatch** para monitorar métricas.
- Configure alarmes para CPU, memória e tráfego.
- Analise os logs do WAF para identificar possíveis ameaças.

## **10.2. Segurança e Backups**

- Habilite backups automáticos no RDS.
- Mantenha o WordPress e plugins atualizados.
- Considere implementar plugins de segurança adicionais.

## **10.3. Escalabilidade e Auto Scaling**

- Configure o ECS para escalar automaticamente com base em métricas.
- Utilize múltiplas zonas de disponibilidade para alta disponibilidade.

## **10.4. Aprimoramentos Futuros**

- Implementar um CDN como o **Amazon CloudFront** para melhorar a performance.
- Otimizar imagens e conteúdo estático.
- Integrar ferramentas de analytics e SEO.

---

# **Conclusão**

Parabéns! Você concluiu a implantação de um site WordPress na AWS utilizando práticas modernas de desenvolvimento e infraestrutura. Este guia detalhado abrange desde a preparação do ambiente, desenvolvimento local, provisionamento de infraestrutura com Terraform, envio da imagem Docker para o ECR, configuração de um pipeline de CI/CD com GitHub Actions, até a configuração de segurança com o AWS WAF.

Este material pode servir como uma referência completa para estudantes e profissionais interessados em aprender sobre desenvolvimento web, contêineres, infraestrutura como código e serviços em nuvem.