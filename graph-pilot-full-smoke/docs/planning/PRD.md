# PRD — Graph Pilot Full Smoke

<!-- INFERIDO: Documentação enxuta baseada em projeto do tipo 'Internal' com baixa complexidade (Simple REST API para smoke test) -->
<!-- PREMISSA: Nenhuma regra de negócio avançada necessária, focando estritamente na validação técnica de CI/CD e hub/deploy -->

---

## Metadados do Projeto

| Campo | Valor |
|-------|-------|
| **Projeto / Feature** | graph pilot full smoke |
| **Data** | 20-08-2026 |
| **Status** | Em Construção |
| **Responsável pelo preenchimento** | Doc Workshop Agent |
| **Stakeholders envolvidos** | pfroes@alvarezandmarsal.com |
| **Prazo esperado (MVP)** | N/A (Smoke Test) |
| **Link do protótipo (Figma, Lovable, URL)** | N/A |
| **Link do Discovery / documento de referência** | `solution-brief.yaml` e `ADR.md` |
| **PO / responsável por validar regras de negócio** | pfroes@alvarezandmarsal.com |

---

## PARTE A — PRODUTO

### 1. Visão Geral do Produto

#### 1.1 Resumo Executivo
Uma API REST simples desenvolvida exclusivamente para validar o funcionamento da esteira WK2 até o hub/deploy. O produto servirá como "smoke test" da infraestrutura e integrações, atendendo os consultores da A&M na garantia de qualidade da esteira.

#### 1.2 Problema
- Necessidade de validar o fluxo fim-a-fim (WK2 até deploy).
- Ausência de um artefato leve, sem interface e sem persistência, exclusivo para testes de carga/deployment.

#### 1.3 Proposta de Valor
| Dimensão | Impacto esperado |
|----------|-----------------|
| Confiabilidade | Garantir que o ambiente de deploy Hub/WK2 está operacional. |

#### 1.4 Usuários-Alvo
- **Consultores A&M**: Usuários primários da validação, garantindo que o deploy seja feito corretamente na infraestrutura interna.

---

### 2. Escopo e Features

#### 2.1 Em Escopo (MVP)
1. **API REST Base**: Endpoints simples (ex.: health check, hello world) para validação de conectividade.
2. **Deploy via Hub (AS2I)**: Integração fluida com o app-space-infra.

#### 2.2 Fora de Escopo
- Interface de Usuário (UI).
- Persistência de Dados (Banco de Dados / Storage).
- Integrações externas complexas.

---

### 3. Jornadas Principais

#### 3.1 Jornada 1: Validação de Health / Smoke
- **Ator**: Consultor A&M / Pipeline CI
- **Gatilho**: Requisição HTTP aos endpoints da API REST.
- **Fluxo Principal**: 
  1. Acessa o endpoint via protocolo HTTP(S).
  2. Recebe a resposta de status 200 OK informando saúde da API.
- **Erros Mapeados**: 5xx em caso de falha de provisionamento no Cloud Run.

---

### 4. Métricas de Sucesso

| KPI / Métrica | Propósito | Meta / Referência |
|---------------|-----------|------------------|
| Deploy Concluído | Garantir a entrega de valor aos consultores A&M | 100% de sucesso no pipeline de CI/CD WK2. |

---

### 5. Backlog Futuro (Pós-MVP)
- A ser definido (projeto atualmente de escopo fechado apenas para testes).

---

## PARTE B — TÉCNICO ESSENCIAL

### 6. Plataforma e Infraestrutura

#### 6.1 Stack Base
| Componente | Tecnologia |
|------------|------------|
| Linguagem / Framework | Python (FastAPI) ou equivalente padrão (definido pelo Forge) |
| Repositório | `graph-pilot-full-smoke` |
| Infraestrutura | A-M-App-Hub/app-space-infra + Cloud Run |
| Ambientes | dev (d), qa (q), prod (p) |
| CI/CD | GitHub Actions via `base_tf_generator` / Hub pipeline |

#### 6.2 Topologia Hub (Arquétipo AS2I)
- **Topologia**: Deploy interno via manifest do hub (`hub/solution.manifest.yaml`).
- **Comunicação**: Rotas expostas em `/api/*`.
- **FinOps**: Charge code designado como `P002675BR06.1.1` associado a `pfroes@alvarezandmarsal.com`, gerenciado pela plataforma Hub.

---

### 7. Acessos e Segurança

#### 7.1 Modelo de Autenticação
- **Autenticação**: CAS no auth-proxy do hub (Padrão AS2I - `INTERNAL_CAS`).
- **Exposição**: Interna.

#### 7.2 Perfis de Acesso (RBAC)
| Perfil | Descrição e Permissões |
|--------|------------------------|
| Consultor A&M | Acesso de leitura/validação para o smoke test. |

---

### 8. Requisitos Funcionais (NFRs)

#### 8.1 API e Integrações
- Fornecer respostas HTTP padronizadas.
- Não necessita de persistência (DB, Caching).

---

### 9. Design System e UI/UX
- **Conformidade com Design System**: Não aplicável (projeto headless `has_user_interface: false`).

---

### 10. Riscos e Dependências

#### 10.1 Riscos Principais
| Risco | Impacto | Probabilidade | Mitigação | Responsável |
|-------|---------|---------------|-----------|-------------|
| Falha no Deploy Hub | Alto | Média | Utilização da esteira padrão WK2 testada iterativamente. | PO |

#### 10.2 Dependências
| Dependência | Tipo | Prazo esperado | Impacto no cronograma |
|-------------|------|----------------|----------------------|
| A-M-App-Hub | Externa | Imediato | Alto |

---

### 11. Aprovação

| Área | Responsável | Status | Data |
|------|------------|--------|------|
| Produto/PO | pfroes@alvarezandmarsal.com | ( ) Aprovado ( ) Pendente | |
| Tech Lead | Agente Solution Designer | ( ) Aprovado ( ) Pendente | |
