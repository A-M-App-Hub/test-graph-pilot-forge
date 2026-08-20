# Blueprint: test-graph-pilot-forge (AS2I)

**Arquétipo:** AS2I — Backend/API interno  
**Topologia:** Pattern_A + INTERNAL_CAS  
**Data:** 2026-08-20

---

## 1. Visão Geral

### Objetivos
- Ver solution-brief.yaml

### Escopo MVP
- API REST headless interna A&M
- Sem UI pública — clientes via API Gateway + API key
- Acesso admin/CAS via auth-proxy onde aplicável

---

## 2. Arquitetura

**Topologia:** Pattern_A ([webapp-topologies.md §2.3](../../references/webapp-topologies.md))  
**Acesso:** INTERNAL_CAS ([access-topologies.md §4.5.1 #7](../../references/access-topologies.md))

### tfvars congelados (dev)

```hcl
frontend_container_count = 0
mixed_container_count    = 0
backend_container_count  = 1
access_topology          = "internal_corp"
access_pattern           = "INTERNAL_CAS"
enable_auth_proxy        = true
sso_provider             = "CAS"
```

---

## 3. Stack

| Camada | Tecnologia |
|--------|------------|
| API | FastAPI + uv |
| Gateway | API Gateway + x-api-key |
| Auth | CAS (auth-proxy) + OpenAPI scheme `cas_jwt` |
| BD | Stateless v1; externo se story exigir |

---

## 4. SSO / OpenAPI

**SSO: CAS** — rotas com `cas_jwt` em securitySchemes (OAS 3.0.3)

---

## 5. FinOps / PostHog

**Desativado** (v1 AS2I)
