# PRD — test graph pilot forge

---

## Metadados do Projeto

| Campo | Valor |
|-------|-------|
| **Projeto / Feature** | test graph pilot forge |
| **Data** | 2026-08-20 |
| **Status** | <!-- INFERIDO: Draft / Inicial --> |
| **Responsável pelo preenchimento** | Doc Workshop Agent |
| **Stakeholders envolvidos** | pfroes@alvarezandmarsal.com |
| **Prazo esperado (MVP)** | N/A |
| **Link do protótipo (Figma, Lovable, URL)** | N/A |
| **Link do Discovery / documento de referência** | `docs/planning/solution-brief.yaml` |
| **PO / responsável por validar regras de negócio** | pfroes@alvarezandmarsal.com |

---

## PARTE A — PRODUTO

---

## 1. Visão Geral do Produto

### 1.1 Resumo Executivo

O projeto "test graph pilot forge" consiste em uma API REST simples com o objetivo exclusivo de validar a esteira WK2 até o hub/deploy. A solução é do tipo AS2I, voltada para uso interno pelos consultores da A&M.

### 1.2 Problema

- Necessidade de validar o fluxo de CI/CD, esteira WK2 e deploy automatizado no A-M-App-Hub.
- Garantir que a infraestrutura baseada no arquétipo AS2I esteja provisionada e funcionando corretamente.

### 1.3 Proposta de Valor

| Dimensão | Impacto esperado |
|----------|-----------------|
| Técnico | Homologação do processo de esteira e deploy em ambiente hub. |
| Negócio | Garantir estabilidade para futuros projetos baseados no arquétipo AS2I. |

### 1.4 Usuários-Alvo

| Perfil | Descrição | Necessidade principal |
|--------|-----------|----------------------|
| **Primário** | Consultores A&M / Desenvolvedores | Validar a chamada da API após o deploy. |

---

## 2. Escopo e Features

### 2.1 Lista de Features

| # | Feature | MVP? | Prioridade (P0-P3) | Complexidade (S/M/L/XL) | Descrição |
|---|---------|------|--------------------|--------------------------|-----------|
| 1 | API REST Simples | Sim | P0 | S | Endpoints básicos para teste de conectividade e resposta. |

### 2.2 Escopo do MVP

**Incluso no MVP:**
- Criação e deploy de uma API REST (FastAPI) sem persistência.
- Autenticação via INTERNAL_CAS.

**Fora do escopo MVP (futuro):**
- Persistência de dados (desativada no brief).
- Interface de usuário (desativada no brief).
- FinOps / PostHog.

---

## 3. Jornadas do Usuário

### 3.1 Personas

| Persona | Descrição | Ações principais |
|---------|-----------|-----------------|
| **Consultor A&M (Dev/Tester)** | Responsável pela validação do projeto | Fazer requisições HTTP para a API |

### 3.2 Fluxos Principais

#### Fluxo: Validação da API

**Persona:** Consultor A&M
**Objetivo:** Obter resposta de sucesso do endpoint deployado.
**Passos:**
1. Autenticar usando SSO CAS.
2. Fazer requisição ao endpoint `/api/...` da solução no hub.
3. Receber resposta HTTP 200/OK.

---

## 4. Métricas de Sucesso (KPIs)

### 4.1 KPIs de Negócio e Produto

| Métrica | Target |
|---------|--------|
| Sucesso de Deploy | 100% de automação do WK2 até hub |
| Disponibilidade API | Resposta 200 OK pós-deploy |

---

## 5. Backlog Futuro

| Feature | Categoria | Justificativa do diferimento |
|---------|-----------|------------------------------|
| N/A | Piloto de teste | Trata-se de uma aplicação "throwaway" ou de teste contínuo. |

---

## PARTE B — TÉCNICO ESSENCIAL

---

## 6. Plataforma e Infraestrutura

### 6.1 Stack Tecnológica

| Camada | Tecnologia | Justificativa |
|--------|-----------|---------------|
| **Backend** | FastAPI | Definido na ADR para padrão AS2I sem persistência. |
| **Frontend** | N/A | `has_user_interface: false` |
| **Banco de Dados** | N/A | `needs_persistence: false` (api_stateless) |

### 6.2 Infraestrutura

**Hub App Space (AS2I — padrão esteira-condutora):**

| Campo | Valor |
|-------|-------|
| Topologia | FastAPI_Mixed + INTERNAL_CAS |
| Deploy | app-space-infra + Bootstrap Hub + Deploy Solution |
| Auth | CAS (auth-proxy hub) |
| OpenAPI | openapi/hub-fragment.yaml + register-hub |
| Persistência | none |

### 6.3 FinOps

| Campo | Valor |
|-------|-------|
| Orçamento estimado (MVP) | FinOps Desativado (v1) |
| Responsável por acompanhar custos | pfroes@alvarezandmarsal.com |

---

## 7. Acessos e segurança (alto nível)

| Pergunta | Resposta |
|----------|----------|
| Onde / como fica a autenticação? | CAS (auth-proxy) |
| Exposição da aplicação / APIs | Restrito (App Hub / Rede interna da A&M) |
| Método de autenticação do usuário | SSO CAS |

### Perfis (enxuto)

| Perfil | Descrição (o que pode fazer) |
|--------|------------------------------|
| **Usuário Padrão** | Pode invocar a API para teste |

### Compliance / dados sensíveis (resumo)

| LGPD, PII, retenção ou restrições relevantes |
|----------------------------------------------|
| N/A (projeto piloto de teste de infraestrutura sem dados reais) |

---

## 8. Requisitos Funcionais

### 8.1 APIs de Saída (alto nível)

<!-- INFERIDO: Apenas endpoints básicos de saúde para a validação proposta. -->

| Endpoint | Método | Descrição |
|----------|--------|-----------|
| `/api/test-graph-pilot-forge/health` | GET | Endpoint de validação e health check da API |
| `/api/test-graph-pilot-forge/test` | GET | Endpoint REST simples de validação do WK2 |

---

## 9. Design System e UI/UX

*Projeto sem interface de usuário (`has_user_interface: false`). Esta seção não se aplica.*

---

## 10. Riscos e Dependências

### 10.1 Riscos Principais

| Risco | Impacto | Probabilidade | Mitigação | Responsável |
|-------|---------|---------------|-----------|-------------|
| Falha no deploy hub | Alto | Média | Acompanhar logs do GitHub Actions para debug imediato | Tech Lead |

### 10.2 Dependências

| Dependência | Tipo | Prazo esperado | Impacto no cronograma |
|-------------|------|----------------|----------------------|
| A-M-App-Hub proxy e CAS | Externa | Imediato | Bloqueia testes da API se estiver fora do ar |

---

## 11. Aprovação

| Área | Responsável | Status | Data |
|------|------------|--------|------|
| Produto/PO | pfroes@alvarezandmarsal.com | ( ) Aprovado ( ) Pendente | |
| Tech Lead | | ( ) Aprovado ( ) Pendente | |

**Resultado final:** ( ) Aprovado para desenvolvimento
