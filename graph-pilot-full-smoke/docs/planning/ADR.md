# ADR — {nome-do-projeto}

**Data de criação:** YYYY-MM-DD  
**Skill orquestradora:** esteira-condutora

---

## Estado Atual

**Lifecycle:** construcao
**Arquétipo:** AS2I
**Playbook:** AS2I-construcao.yaml
**Step atual:** roadmap
**Fase:** 3
**Modo:** AUTOMATION  
**GitHub actor:** am-esteira-helpe[bot]  
**Org:** A-M-App-Hub  
**Repositório:** A-M-App-Hub/graph-pilot-full-smoke  
**Status solução:** ACTIVE  
**Próxima ação:** render-brief + classify  
**Última atualização:** YYYY-MM-DD HH:MM

---

## Premissas e Mapeamento Inicial

- **Repositório**: `A-M-App-Hub/{repo-name}`
- **Topologia alvo**: {Minimal | Pattern_A} + INTERNAL_CAS
- **SSO**: CAS
- **Persistência**: {none | api_stateless}
- **Stack frontend**: {React | N/A}
- **Stack backend**: {FastAPI | N/A}
- **FinOps**: Desativado (v1)
- **PostHog**: Desativado (v1)

---

## Artefatos de Referência

| Artefato | Path | Preenchido por | Data |
|----------|------|----------------|------|
| Solution Brief | `docs/planning/solution-brief.yaml` | render-brief.sh | |
| PRD | `docs/planning/*-prd.md` | doc-workshop | |
| Blueprint | `docs/planning/blueprints/*.md` | render-blueprint.sh | |
| Roadmap | `docs/planning/roadmap_equilibrado.md` | roadmap-engineer | |
| User Status | `docs/planning/user-status.md` | esteira-condutora | |

---

## Histórico de Fases

| Data | Hora | Transição | Observações |
|------|------|-----------|-------------|
| | | | |

---

## Notas para o Agente

- Recovery: ler **Estado Atual** + invocar `detect-entry.sh`
- Atualizar ADR após cada step via `adr.sh update`
