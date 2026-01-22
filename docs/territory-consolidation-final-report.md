# Territory Consolidation: Final Report

**Generated:** 2026-01-21
**Scope:** infra-gitops + infrastructure-charts

---

## Bottom Line

**Kenya and Nigeria can be consolidated into a single AWS deployment.** One service difference exists (api-conversation). Pakistan must remain separate.

---

## Territory Status

| Territory | Status | Infrastructure | Recommendation | Go/No Go |
|-----------|--------|----------------|----------------|----------|
| Nigeria | ACTIVE | AWS (Rancher) | **KEEP** - Primary AWS deployment | ✅ |
| Kenya | ACTIVE | AWS (Rancher) | **REMOVE** - Merge into Nigeria | ✅ |
| Pakistan | ACTIVE | RapidCompute | **KEEP** - Separate infra required | ✅ |
| Ghana | DORMANT | - | **DELETE** - Not deployed | ✅ |
| Lebanon | DORMANT | - | **DELETE** - Not deployed | ✅ |

---

## Service Comparison: Kenya vs Nigeria

### Identical (45 services)
All services except one have **zero configuration differences** between Kenya and Nigeria. Same images, same replicas, same settings.

### One Difference: api-conversation

| Territory | Status | Replicas | Feature |
|-----------|--------|----------|---------|
| Kenya | **DISABLED** | 0 | No WhatsApp/conversation |
| Nigeria | **ENABLED** | 2 | WhatsApp/conversation active |
| Pakistan | **DISABLED** | 0 | No WhatsApp/conversation |

**Decision required:** If consolidating to Nigeria, this resolves itself. If keeping both territory names, decide whether Kenya needs conversation functionality.

---

## Pakistan: Why It Must Stay Separate

| Setting | AWS | Pakistan |
|---------|-----|----------|
| Cloud provider | AWS | RapidCompute |
| S3 storage | AWS S3 | `rcns_ele-health.s3.rapidcompute.com` |
| S3 protocol | HTTPS | HTTP |
| Secrets prefix | `amazon-eu-west-1-rah3ee` | `rapidcompute-khi04-cluster` |
| MongoDB | Default | Percona |
| PostgreSQL | Default | Strimzi |
| Elasticsearch | Default | Local proxy |

**Not consolidatable** - fundamentally different infrastructure.

---

## Files to Delete

### infra-gitops (6 files) ✅
```
elephant/elephantos-aoa/values/ghana-acceptance.yaml
elephant/elephantos-aoa/values/ghana-production.yaml
elephant/elephantos-aoa/values/kenya-acceptance.yaml
elephant/elephantos-aoa/values/kenya-production.yaml
elephant/elephantos-aoa/values/lebanon-acceptance.yaml
elephant/elephantos-aoa/values/lebanon-production.yaml
```

### infrastructure-charts (2 files) ✅
```
primarycare-argo-apps/global-values/territories/ghana.yaml
primarycare-argo-apps/global-values/territories/lebanon.yaml
```

---

## Files to Edit

### infra-gitops (5 files) ✅
Remove Kenya entries from ApplicationSet matrices:

| File | Change |
|------|--------|
| `clusters/platform/tenants/argocd/applicationsets/elephantos.yaml` | Remove Kenya acceptance/production entries |
| `clusters/platform/tenants/argocd/applicationsets/dataplatform/kafka-connectors.yaml` | Remove Kenya entries |
| `clusters/platform/tenants/argocd/applicationsets/dataplatform/components.yaml` | Remove Kenya entries |
| `clusters/platform/tenants/argocd/applicationsets/primarycare/primarycare-apps.yaml` | Delete all commented territory blocks |
| `clusters/platform/tenants/argocd/applicationsets/primarycare/primarycare-etls.yaml` | Delete all commented territory blocks |

### infrastructure-charts (1 file) ✅
```
primarycare-argo-apps/global-values/territories/kenya.yaml  # Delete after infra-gitops changes
```

---

## Consolidation Checklist

### Phase 1: Clean Dormant Territories
- [ ] Delete Ghana configs (infra-gitops + infrastructure-charts)
- [ ] Delete Lebanon configs (infra-gitops + infrastructure-charts)
- [ ] Remove commented territory blocks from ApplicationSets

### Phase 2: Consolidate Kenya into Nigeria
- [ ] Verify no active Kenya deployments in ArgoCD
- [ ] Remove Kenya from elephantos.yaml ApplicationSet
- [ ] Remove Kenya from dataplatform ApplicationSets
- [ ] Delete Kenya value files from infra-gitops
- [ ] Delete Kenya territory file from infrastructure-charts

### Phase 3: Verify
- [ ] Confirm Nigeria acceptance/production still deploying correctly
- [ ] Confirm Pakistan acceptance/production unaffected
- [ ] Confirm no orphaned ArgoCD applications

---

## Risk Assessment

| Action | Risk | Notes |
|--------|------|-------|
| Delete Ghana/Lebanon | None | Never deployed |
| Remove Kenya | Low | Verify ArgoCD first |
| Pakistan changes | N/A | No changes proposed |

---

## Final State

| Deployment | Territories Served | Services |
|------------|-------------------|----------|
| AWS (Rancher) | Nigeria | 46 services |
| RapidCompute | Pakistan | 46 services |

Two deployments. Two territories. Clean.
