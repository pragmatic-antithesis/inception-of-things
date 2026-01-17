# Inception of Things (IoT)

Este repositório contém a implementação do projeto **Inception of Things**, cujo objetivo é fornecer uma **introdução prática ao Kubernetes**, utilizando **K3s**, **K3d**, **Vagrant** e **Argo CD**.

O projeto é dividido em três partes obrigatórias (p1, p2 e p3) e uma parte bônus opcional.

---

## 🎯 Objetivos do Projeto

- Entender os conceitos fundamentais de **Kubernetes**
- Criar e gerenciar **máquinas virtuais com Vagrant**
- Implantar aplicações em um cluster **K3s**
- Configurar **Ingress** para roteamento HTTP
- Utilizar **K3d** para clusters Kubernetes baseados em Docker
- Implementar **GitOps** com **Argo CD**

> ⚠️ Este projeto **não tem como objetivo dominar Kubernetes**, mas sim apresentar seus conceitos essenciais na prática.

---

## 🧱 Estrutura do Repositório

.
├── p1/
│   ├── Vagrantfile
│   ├── scripts/
│   └── confs/
├── p2/
│   ├── Vagrantfile
│   ├── scripts/
│   └── confs/
├── p3/
│   ├── scripts/
│   └── confs/
└── bonus/        # opcional
    ├── Vagrantfile
    ├── scripts/
    └── confs/

- **scripts/**: scripts de provisionamento e instalação  
- **confs/**: arquivos de configuração (Kubernetes, ingress, etc.)

---

## 📦 Parte 1 — K3s e Vagrant (p1)

### Objetivo
Criar um **cluster K3s com dois nós**, utilizando **Vagrant**.

### Requisitos
- 2 máquinas virtuais Linux
- Recursos mínimos:
  - 1 CPU
  - 1024 MB de RAM

### Configuração

| Máquina | Hostname | IP |
|--------|----------|----|
| Server | `<login>S` | 192.168.56.110 |
| Worker | `<login>SW` | 192.168.56.111 |

### Tarefas
- Criar um `Vagrantfile` com duas VMs
- Configurar IP fixo e hostname
- Garantir acesso SSH sem senha
- Instalar:
  - K3s em modo **server** no nó principal
  - K3s em modo **agent** no nó worker
- Instalar e utilizar `kubectl`

---

## 🌐 Parte 2 — K3s e Três Aplicações Web (p2)

### Objetivo
Executar **três aplicações web** em um cluster K3s e expô-las via **Ingress**, usando roteamento por HOST.

### Ambiente
- 1 VM Linux
- K3s em modo **server**
- IP fixo: `192.168.56.110`

### Comportamento esperado

| HOST | Aplicação |
|-----|-----------|
| app1.com | app1 |
| app2.com | app2 (3 réplicas) |
| qualquer outro | app3 (default) |

### Conceitos aplicados
- Deployments
- Services
- Replicas
- Ingress Controller
- Regras de host

---

## 🔄 Parte 3 — K3d e Argo CD (p3)

### Objetivo
Criar um ambiente Kubernetes sem Vagrant, utilizando **K3d**, e implementar **CI/CD com Argo CD**.

### Requisitos
- Docker
- K3d
- Script de instalação automática das dependências

### Estrutura
- Dois namespaces:
  - `argocd`
  - `dev`

### GitOps
- Criar um repositório público no GitHub
- Nome do repositório deve conter o login de um membro do grupo
- O Argo CD deve:
  - Monitorar o repositório
  - Implantar automaticamente a aplicação no namespace `dev`

### Aplicação
- Deve possuir **duas versões**: `v1` e `v2`
- Opções:
  - Usar a imagem `wil42/playground`
  - Criar sua própria imagem Docker pública

### Validação
- Alterar a versão no repositório Git
- Verificar sincronização automática no Argo CD
- Confirmar que a aplicação foi atualizada

---

## ⭐ Bônus — GitLab (opcional)

### Objetivo
Adicionar uma instância **GitLab local** integrada ao cluster.

### Requisitos
- Namespace dedicado: `gitlab`
- GitLab rodando localmente
- Integração com o fluxo do Argo CD
- Uso de ferramentas adicionais permitido (ex: Helm)
