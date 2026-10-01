
**Instrutor / Aluno:** Guilherme  
**Módulo:** Cultura e Ferramentas DevOps  
**Data:** 2026  

---

## 📋 Sumário
1. [Objetivos da Aula](#1-objetivos-da-aula)
2. [O Ciclo de Vida DevOps](#2-o-ciclo-de-vida-devops)
3. [Integração Contínua (CI - Continuous Integration)](#3-integração-contínua-ci---continuous-integration)
4. [Entrega e Implantação Contínua (CD - Continuous Delivery/Deployment)](#4-entrega-e-implantação-contínua-cd)
5. [Estratégias de Deployment](#5-estratégias-de-deployment)
6. [Exemplo Prático: Pipeline de CI/CD (GitHub Actions)](#6-exemplo-prático-pipeline-de-cicd-github-actions)
7. [Integrando Ferramentas no Ecossistema](#7-integrando-ferramentas-no-ecossistema)
8. [Atividade Prática e Desafio](#8-atividade-prática-e-desafio)

---

## 1. Objetivos da Aula

Nesta décima aula, o foco é compreender como integrar ferramentas, processos e equipes para automatizar todo o ciclo de vida do desenvolvimento de software.

Ao final desta aula, você será capaz de:
* Compreender os pilares da Integração Contínua (CI) e Entrega Contínua (CD).
* Construir pipelines automatizados de build, teste e deploy.
* Integrar ferramentas de versionamento, comunicação e monitoramento.
* Aplicar estratégias seguras de implantação em produção.

---

## 2. O Ciclo de Vida DevOps

O ecossistema DevOps é contínuo e interconectado. As etapas de integração englobam:

```
[ Planejar ] ➔ [ Codificar ] ➔ [ Build ] ➔ [ Testar ]
     ▲                                          │
     │                                          ▼
[ Monitorar ] ◄─ [ Operar ] ◄─ [ Deploy ] ◄─ [ Release ]
```

---

## 3. Integração Contínua (CI - Continuous Integration)

A Integração Contínua é a prática de mesclar todas as cópias de trabalho dos desenvolvedores em um barramento centralizado (ex: branch `main`) várias vezes ao dia.

### Benefícios
* Detecta bugs precocemente (*Fail Fast*).
* Reduz o "inferno da mesclagem" (*Merge Hell*).
* Garante que o código no repositório sempre seja compilável e testado.

### Principais Ferramentas de CI
* **GitHub Actions**
* **GitLab CI/CD**
* **Jenkins**
* **Azure DevOps Pipelines**

---

## 4. Entrega e Implantação Contínua (CD)

| Conceito | Descrição | Intervenção Humana |
| :--- | :--- | :---: |
| **Continuous Delivery (Entrega Contínua)** | O código é automaticamente preparado, testado e empacotado para produção. | **Sim** (Aprovação manual para deploy) |
| **Continuous Deployment (Implantação Contínua)** | Cada alteração aprovada nos testes vai diretamente para produção sem pausas. | **Não** (Totalmente automatizado) |

---

## 5. Estratégias de Deployment

Para garantir alta disponibilidade durante as integrações, utilizamos estratégias como:

1. **Canary Deployment:** O novo código é liberado para uma pequena porcentagem de usuários antes de ser implantado para todos.
2. **Blue-Green Deployment:** Dois ambientes idênticos (Blue = Atual, Green = Novo). O tráfego do roteador é alterado do Blue para o Green instantaneamente.
3. **Rolling Update:** Os nós/containers da aplicação são atualizados gradualmente em lotes.

---

## 6. Exemplo Prático: Pipeline de CI/CD (GitHub Actions)

Abaixo está o exemplo de um arquivo `.github/workflows/main.yml` configurado para automação de testes e deploy de uma aplicação Node.js:

```yaml
name: Pipeline CI/CD - Aula 10 Guilherme

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build-and-test:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout do Código
      uses: actions/checkout@v3

    - name: Configurar Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'

    - name: Instalar Dependências
      run: npm ci

    - name: Executar Linter
      run: npm run lint

    - name: Executar Testes Unitários
      run: npm test

  deploy:
    needs: build-and-test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'

    steps:
    - name: Notificar início do Deploy
      run: echo "Iniciando implantação no ambiente de Produção..."

    - name: Executar Deploy no Servidor
      run: |
        # Exemplo de comando de deploy via SSH/Docker
        echo "Aplicação implantada com sucesso!"
```

---

## 7. Integrando Ferramentas no Ecossistema

As integrações em DevOps funcionam através de **Webhooks** e **APIs REST**.

* **Git + Jira / Trello:** Associa commits e Pull Requests a tarefas/cards automaticamente.
* **CI/CD + Slack / Microsoft Teams:** Notifica o canal da equipe se um build falhar ou se um deploy for realizado com sucesso.
* **CI/CD + SonarQube:** Análise estática do código (*SAST*) para medição de qualidade e cobertura de testes.
* **Deploy + Prometheus / Grafana:** Monitoramento contínuo das métricas após cada nova versão lançada.

---

## 8. Atividade Prática e Desafio

### Exercício Individual:
1. Crie um repositório no GitHub para o seu projeto.
2. Configure um **Workflow de CI** com GitHub Actions que:
   - Seja disparado a cada `push`.
   - Valide a sintaxe do seu código.
   - Execute testes automatizados.
3. Integre uma notificação simples em caso de falha no pipeline.

---

> **Anotações da Aula:**  
> *Lembre-se: Automação sem testes confiáveis apenas acelera a entrega de bugs para o usuário final!*