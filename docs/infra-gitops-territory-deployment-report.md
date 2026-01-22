# Territory Deployment Report

**Generated:** 2026-01-21
**Scope:** infra-gitops repository only

---

## Summary

| Territory | Status | Cluster | Notes |
|-----------|--------|---------|-------|
| **Nigeria** | ACTIVE | AWS (Rancher) | Acceptance + Production |
| **Kenya** | ACTIVE | AWS (Rancher) | Acceptance + Production |
| **Pakistan** | ACTIVE | RapidCompute | Acceptance + Production (separate infra) |
| **Ghana** | DORMANT | - | Config exists, not deployed |
| **Lebanon** | DORMANT | - | Config exists, not deployed |

---

## Active Deployments by ApplicationSet

### 1. ElephantOS App-of-Apps (`elephantos.yaml`)
Primary application deployments per territory.

| Territory | Environment | Cluster | Status |
|-----------|-------------|---------|--------|
| Kenya | acceptance | amazon-acceptance-stateless-rancher | Active |
| Kenya | production | amazon-production-stateless-rancher | Active |
| Nigeria | acceptance | amazon-acceptance-stateless-rancher | Active |
| Nigeria | production | amazon-production-stateless-rancher | Active |
| Pakistan | acceptance | rapidcompute-acceptance-stateless-rc34 | Active |
| Pakistan | production | - | Not in elephantos (uses legacy path) |
| Ghana | * | - | Commented out |
| Lebanon | * | - | Commented out |

### 2. Kafka Connectors (`dataplatform/kafka-connectors.yaml`)
Data pipeline connectors per territory.

| Territory | Environments | Status |
|-----------|--------------|--------|
| Kenya | acceptance, production | Active |
| Nigeria | acceptance, production | Active |
| Pakistan | acceptance, production | Active |
| Ghana | - | Not configured |
| Lebanon | - | Not configured |

### 3. Data Platform Components (`dataplatform/components.yaml`)
Same matrix as Kafka connectors: Kenya, Nigeria, Pakistan only.

### 4. Primarycare Apps/ETLs (`primarycare/`)
Legacy ApplicationSet - only Pakistan production is active. All other territories (Ghana, Kenya, Lebanon, Nigeria) are commented out.

### 5. Shared Apps (`shared-apps.yaml`)
Schema registry deployments. Cluster-based, not territory-specific.

| Cluster | Environment | Status |
|---------|-------------|--------|
| pakistan-acceptance | acceptance | Active |
| pakistan-production | production | Active |
| amazon-acceptance-stateless-rancher | acceptance | Active |
| amazon-acceptance-kaiho9 | acceptance | Active |
| amazon-production-stateless-rancher | production | Active |

---

## Pakistan-Specific Infrastructure

Pakistan runs on separate RapidCompute infrastructure (not AWS).

**Flux-managed resources in `clusters/rapidcompute/`:**
- `pakistan-production.yaml` - Kustomization + TLS certificates
- `pakistan-production-mongodb.yaml` - MongoDB operator

**Stateful components in `elephant/rapidcompute/`:**
- PostgreSQL patches
- MongoDB patches
- Kafka configuration
- Elasticsearch patches

---

## What Can Be Removed

### Immediately Removable (No Active Deployments)

| Item | Location | Action |
|------|----------|--------|
| Ghana acceptance config | `elephant/elephantos-aoa/values/ghana-acceptance.yaml` | Delete |
| Ghana production config | `elephant/elephantos-aoa/values/ghana-production.yaml` | Delete |
| Lebanon acceptance config | `elephant/elephantos-aoa/values/lebanon-acceptance.yaml` | Delete |
| Lebanon production config | `elephant/elephantos-aoa/values/lebanon-production.yaml` | Delete |

### Requires Verification Before Removal

| Item | Location | Concern |
|------|----------|---------|
| Kenya configs | `elephant/elephantos-aoa/values/kenya-*.yaml` | Active in elephantos.yaml |
| Pakistan acceptance | Multiple locations | Active deployments |
| Commented entries in primarycare-apps.yaml | `clusters/platform/.../primarycare/` | Already inactive, can clean up |

### Pakistan Considerations

If Pakistan is to be kept, these are required:
- `clusters/rapidcompute/` - Flux configs
- `clusters/rapidcompute-acceptance-z3gh/` - Acceptance cluster
- `elephant/rapidcompute/` - Stateful component configs
- Pakistan entries in all active ApplicationSets

---

## Files Referencing Each Territory

```
Ghana:     10 files (all dormant config)
Kenya:     12 files (active deployments)
Lebanon:   10 files (all dormant config)
Nigeria:   12 files (active deployments)
Pakistan:  35 files (active, separate infrastructure)
```

---

## Recommended Cleanup Order

1. **Delete dormant territory configs** - Ghana and Lebanon value files
2. **Clean commented code** - Remove commented territory entries in ApplicationSets
3. **Assess Kenya** - If truly unused, remove from elephantos.yaml and dataplatform configs
4. **Pakistan decision** - Keep or migrate; significant infrastructure footprint

---

## Key Files to Modify

| File | Purpose |
|------|---------|
| `clusters/platform/tenants/argocd/applicationsets/elephantos.yaml` | Territory deployment matrix |
| `clusters/platform/tenants/argocd/applicationsets/dataplatform/*.yaml` | Data platform per-territory |
| `elephant/elephantos-aoa/values/*.yaml` | Territory-specific Helm values |
