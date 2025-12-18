# 🌐 Administração de Opções de Computação como PaaS no Azure

Este material apresenta um **resumo explicativo e organizado** sobre **Administração de Opções de Computação como PaaS no Microsoft Azure**, com foco em **Azure App Service, App Service Plans, escalabilidade, segurança, deployment slots e contêineres**, baseado no conteúdo estudado para a certificação **AZ-104**.

---

## 📦 Azure App Service (PaaS)

O **Azure App Service** é uma oferta de **Plataforma como Serviço (PaaS)** que permite criar, implantar e gerenciar:

- Aplicativos Web
- Aplicativos de API
- Aplicativos móveis
- Aplicativos de funções

Suporta diversas linguagens e tecnologias:
- **.NET, .NET Core, Java, Node.js, Python, PHP**
- **HTML**
- **Contêineres Docker personalizados**
- Execução em **Windows ou Linux**

A infraestrutura é totalmente gerenciada pela Microsoft, permitindo que os desenvolvedores foquem apenas no código e na lógica da aplicação.

Por padrão, o acesso ocorre via `azurewebsites.net`, mas é possível configurar **domínio personalizado** (o nome deve ser exclusivo).

---

## 🧠 App Service Plan – Conceito Central

O **App Service Plan** é o componente que:

- Define **desempenho**
- Define **preço**
- Define **recursos disponíveis**

Ele determina o **conjunto de recursos de computação** em que um aplicativo será executado.

### Dentro de um App Service Plan é possível definir:
- Região onde os recursos serão criados
- Sistema operacional (Windows ou Linux)
- Número de instâncias de máquinas virtuais
- Tamanho das instâncias (CPU, memória e disco)
- Modelo de instância (SKU)

👉 **Um ou mais aplicativos podem ser executados no mesmo App Service Plan**, compartilhando os recursos.

---

## 🏢 Tipos de Planos do Serviço de Aplicativo

<img width="584" height="207" alt="image" src="https://github.com/user-attachments/assets/c2f0460a-0671-42cc-b0b0-0f6cda74c181" />


### 🔹 Computação Compartilhada
- **Free (F1)** e **Shared**
- Aplicativos executam na mesma VM que outros clientes
- Recursos não podem ser expandidos
- Não suporta:
  - Escala automática
  - Múltiplas instâncias
  - Deployment slots
- Indicado para **testes e estudos**

### 🔹 Computação Dedicada
- **Basic, Standard e Premium**
- Aplicativos executam em **VMs dedicadas**
- Suporta:
  - Escalabilidade
  - Deployment slots
  - Backup
  - Monitoramento
- Indicado para **produção**

### 🔹 Isolated (I1, I2, I3)
- Executa aplicativos em **VMs dedicadas dentro de redes virtuais dedicadas**
- Alto nível de isolamento e segurança
- Indicado para **ambientes corporativos críticos**

---

## 🔁 Deployment Slots (Slots de Implantação)

Os **deployment slots** funcionam como ambientes paralelos (“caixinhas”) onde versões diferentes da aplicação podem ser executadas.

### Benefícios:
- Criar ambientes como **produção, staging e teste**
- Validar alterações antes de ir para produção
- Fazer **swap (troca)** sem downtime
- Evitar inicialização a frio
- Permitir rollback rápido

**Integração com**: GitHub, Azure Repos, Bitbucket, Git local e Docker Hub.

⚠️ Disponível apenas nos planos **Standard, Premium e Isolated**.

---

## 📈 Escalabilidade no App Service Plan

### 🔼 Escala Vertical (Scale Up)
- Altera o **plano do serviço**
- Mais:
  - CPU
  - Memória
  - Disco
  - Recursos avançados
- Exemplo: trocar de Standard para Premium

📌 Conceito: *“subindo a montanha”*

### ➕ Escala Horizontal (Scale Out)
- Aumenta ou reduz o **número de instâncias**
- Pode ser:
  - Manual (número fixo)
  - Automática (Auto Scale)

**Baseada em**:
- Porcentagem de CPU
- Porcentagem de memória
- Número de requisições HTTP
- Agendas (dias úteis, finais de semana, horários)

📌 Conceito: *“modelo elástico”*

⚠️ Boa prática: **não esquecer de reduzir a escala** quando a demanda cair.

---

## 🔐 Segurança no App Service

Recursos de segurança nativos:
- Autenticação integrada
- Microsoft **Entra ID (Azure AD)**
- Provedores externos: Google, GitHub, Facebook, Apple, Twitter
- HTTPS e certificados SSL
- Restrições de acesso por IP
- Logs de diagnóstico
- Armazenamento de segredos no **Azure Key Vault**

---

## 🌍 Domínio Personalizado

Para usar domínio próprio:
- O plano precisa oferecer suporte
- Criar registros DNS:
  - CNAME ou A
- Validar o domínio no portal do Azure

---

## 💾 Backup do App Service

- Disponível apenas nos planos **Standard ou Premium**
- Pode ser:
  - Manual
  - Agendado
- Inclui:
  - Arquivos da aplicação
  - Configurações
  - Banco de dados conectado
- Limite: **até 10 GB**
- Permite restauração ou criação de novo aplicativo

---

## 🖥️ Máquinas Virtuais e Contêineres

<img width="590" height="347" alt="image" src="https://github.com/user-attachments/assets/ae5a4f9e-c9fb-4bb7-9826-c5ab48ec64a1" />

### 🌐 Evolução da Infraestrutura – De Máquinas Físicas a Containers

#### 1️⃣ Máquinas Físicas (Tradicional)
- Uma aplicação por máquina (1:1)
- Subutilização de recursos
- Escalabilidade difícil (necessário trocar hardware)

#### 2️⃣ Virtualização
- Criação de várias **Máquinas Virtuais (VMs)** em um único servidor físico
- Uso de **hipervisor** (ex: Hyper-V, VMware)
- Cada VM:
  - É isolada
  - Possui seu próprio sistema operacional
- Melhor aproveitamento de recursos

#### 3️⃣ Modelo Monolítico
- Aplicação construída como um único bloco
- Dificuldade para escalar
- Atualizações exigem reinstalação completa

#### 4️⃣ Microserviços e Contêineres
- Aplicações divididas em pequenos serviços independentes
- Uso de **containers (ex: Docker)**
- Containers são leves, rápidos e portáveis
- Compartilham o SO do host, com isolamento
- Fáceis de escalar, atualizar e mover entre ambientes

---

## 📊 Comparação: Máquinas Virtuais vs Contêineres

| Característica | Máquinas Virtuais (VMs) | Contêineres |
|---|---|---|
| Isolamento | Completo | Parcial (kernel compartilhado) |
| Sistema Operacional | Um por VM | Compartilhado no host |
| Implantação | Lenta e pesada | Rápida e leve |
| Armazenamento Persistente | Manual | Volumes persistentes |
| Tolerância a Falhas | Alta (mais cara) | Alta com orquestração |

---

## ☁️ No Azure: Contêineres vs Máquinas Virtuais

| Característica | Contêineres (ACI, AKS) | Máquinas Virtuais |
|---|---|---|
| Inicialização | Segundos | Minutos |
| Leveza | Muito leves | Pesadas |
| Consumo de recursos | Baixo | Alto |
| Escalabilidade | Rápida (Kubernetes) | Mais lenta |
| Atualizações | Por serviço | Requer reinício |
| Uso ideal | Microsserviços e APIs | Aplicações legadas |
| Custos | Mais econômicos | Maior custo fixo |

---

## 🚀 Azure Container Instances (ACI)

- Serviço **PaaS**
- Containers iniciam em **segundos**
- Suporte a IP público e nome DNS
- Alocação de CPU e memória sob demanda
- Tamanhos personalizados
- Volumes persistentes
- Compatível com **Windows e Linux**
- **Grupos de contêineres**
- Integração com **VNet**

---

## 🚀 Azure Container Apps (ACA)

- Serviço **serverless** para contêineres
- Escalonamento automático (inclusive **escala zero**)
- Ideal para microsserviços e event-driven
- Sem gerenciamento de Kubernetes
- Integração com VNet
- Suporte a Linux e Windows

---

## 📦 Grupo de Contêineres

- Recurso de nível superior do ACI
- Contêineres no **mesmo host**
- Compartilham ciclo de vida, recursos, rede local e volumes

---

## 🐳 Plataforma Docker

<img width="595" height="257" alt="image" src="https://github.com/user-attachments/assets/90a62a11-6af0-4328-b967-6e0d6f8b69d9" />

- Docker não funciona apenas na nuvem
- Uso local ou no Azure
- Disponível para Linux e Windows
- Contêiner = unidade de software padronizada com tudo para executar a aplicação

---

## 📦 Gerenciamento de Contêineres

### Azure Container Registry (ACR)
- Registro **privado** de imagens
- Serviço gerenciado no Azure
- Integração com ACI, AKS e Azure Container Apps

---

## ☸️ Azure Kubernetes Service (AKS)

<img width="634" height="340" alt="image" src="https://github.com/user-attachments/assets/4efc5dfc-aadb-4a1a-8ca5-c4316ed398a7" />

- Orquestração completa de contêineres
- Ideal para grandes aplicações distribuídas
- Microsoft gerencia o **control plane**
- Você gerencia apenas os **nós de agente**
- Cobrança somente pelos nós de agente

### 📘 Terminologia Básica do AKS

<img width="589" height="278" alt="image" src="https://github.com/user-attachments/assets/fe83e00d-916c-4bc2-8aee-15411cee680c" />

- **Cluster**: conjunto de nós
- **Node**: máquina que executa contêineres
- **Node Pool**: grupo de nós semelhantes
- **Pod**: menor unidade (1+ contêineres)
- **Deployment**: controla versões e réplicas
- **Service**: exposição e comunicação
- **Autoscaling**: HPA e Cluster Autoscaler

---

## 🧠 Quando usar cada serviço?

- **VMs** → Aplicações legadas ou sistemas contínuos
- **ACI** → Contêiner único, rápido e isolado
- **ACA** → Microsserviços sem gerenciar Kubernetes
- **AKS** → Grandes aplicações distribuídas

---

## 🧠 Conclusão

O **Azure App Service** combinado com o **App Service Plan** permite modernizar aplicações com **alta disponibilidade**, **escala sob demanda** e **segurança corporativa**, apoiado por opções robustas de contêineres e orquestração no Azure.

---

## 🔗 Referências

- https://azure.microsoft.com/pricing/details/app-service/windows/
- https://docs.microsoft.com/azure/app-service/manage-scale-up
- https://learn.microsoft.com/pt-br/azure/azure-monitor/autoscale/autoscale-get-started
- https://docs.microsoft.com/azure/container-instances/container-instances-overview
- https://docs.microsoft.com/azure/container-instances/container-instances-quickstart-portal
- https://learn.microsoft.com/pt-br/virtualization/windowscontainers/about/
- https://mslearn.cloudguides.com/en-us/guides/AZ-900%20Exam%20Guide%20-%20Azure%20Fundamentals%20Exercise%202
- https://mslearn.cloudguides.com/en-us/guides/AZ-900%20Exam%20Guide%20-%20Azure%20Fundamentals%20Exercise%203
- https://mslabs.cloudguides.com/en-us/guides/AZ-104%20Exam%20Guide%20-%20Microsoft%20Azure%20Administrator%20Exercise%2013



