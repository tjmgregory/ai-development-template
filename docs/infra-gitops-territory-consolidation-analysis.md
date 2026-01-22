# Territory Consolidation Analysis

**Generated:** 2026-01-21

---

## Executive Summary

AWS territories (Kenya, Nigeria, Ghana, Lebanon) are **functionally identical** - differences are limited to naming and SSL certificates. Consolidation to a single AWS deployment is straightforward.

Pakistan runs on separate RapidCompute infrastructure with genuine configuration differences.

---

## AWS Territory Comparison

### Kenya vs Nigeria: Production

**No functional differences.** All differences are naming substitutions:

| Field | Kenya | Nigeria |
|-------|-------|---------|
| territory | `kenya` | `nigeria` |
| shortTerritory | `ken` | `nga` |
| shorterTerritory | `ke` | `ng` |
| primarycareDomain | `kenya.elephantprimarycare.com` | `nigeria.elephantprimarycare.com` |
| patientHubDomain | `ke.ele.health` | `ng.ele.health` |
| sslCertificateArn | `...certificate/98cb3f2b-...` | `...certificate/f643b36f-...` |

Image tags, replica counts, and all other settings are **identical**.

### Kenya vs Nigeria: Acceptance

One inconsistency exists:

| Setting | Kenya | Nigeria |
|---------|-------|---------|
| `gateway.tls.enabled` | `true` | `false` |
| `gateway.tls.certificate.create` | `true` | not set |

This appears to be config drift, not intentional. Should be unified.

### Ghana & Lebanon

Identical structure to Kenya/Nigeria. Only naming differs. Currently dormant (not deployed).

---

## Pakistan Differences

Pakistan runs on RapidCompute infrastructure with genuine configuration differences:

| Setting | AWS Territories | Pakistan |
|---------|-----------------|----------|
| `ssmPrefix` | `amazon-eu-west-1-rah3ee` | `rapidcompute-khi04-cluster` |
| `enableKafkaSecrets` | `true` | `false` |
| `mongodbDistribution` | default | `percona` |
| `postgresDistribution` | default | `strimzi` |
| `elasticsearch.proxy_type` | default | `local` |
| `externalSecrets.esSidecar.type` | default | `local` |
| `sslCertificateArn` | AWS ACM ARN | `N/A` |
| `primary-care-api-auth.replica_count` | `1` | `0` (disabled) |
| `api-legacy-authorisation.config_env` | `production` | `development` |

These differences reflect infrastructure constraints, not feature toggles.

---

## Consolidation Plan: AWS Territories

### Target State

- **One AWS deployment** using Nigeria naming (currently the only active territory)
- **One RapidCompute deployment** for Pakistan

### Steps

1. **Fix acceptance TLS inconsistency**
   - Update Nigeria acceptance to match Kenya's TLS config (or vice versa)

2. **Remove dormant territory configs**
   ```
   elephant/elephantos-aoa/values/ghana-acceptance.yaml
   elephant/elephantos-aoa/values/ghana-production.yaml
   elephant/elephantos-aoa/values/kenya-acceptance.yaml
   elephant/elephantos-aoa/values/kenya-production.yaml
   elephant/elephantos-aoa/values/lebanon-acceptance.yaml
   elephant/elephantos-aoa/values/lebanon-production.yaml
   ```

3. **Clean ApplicationSet matrices**
   - `elephantos.yaml` - remove Kenya entries
   - `dataplatform/kafka-connectors.yaml` - remove Kenya entries
   - `dataplatform/components.yaml` - remove Kenya entries

4. **Remove commented territory entries**
   - `primarycare/primarycare-apps.yaml` - delete commented Ghana/Kenya/Lebanon/Nigeria blocks
   - `primarycare/primarycare-etls.yaml` - delete commented blocks

### No Changes Required

- Image tags (already shared across all AWS territories)
- Application code
- Infrastructure charts
- Pakistan configuration

---

## Risk Assessment

| Action | Risk | Mitigation |
|--------|------|------------|
| Delete dormant configs | None | Not deployed |
| Remove Kenya from matrices | Low | Verify no active Kenya deployments in ArgoCD |
| TLS config alignment | Low | Test in acceptance first |

---

## Files to Modify

### Delete (6 files)
```
elephant/elephantos-aoa/values/ghana-acceptance.yaml
elephant/elephantos-aoa/values/ghana-production.yaml
elephant/elephantos-aoa/values/kenya-acceptance.yaml
elephant/elephantos-aoa/values/kenya-production.yaml
elephant/elephantos-aoa/values/lebanon-acceptance.yaml
elephant/elephantos-aoa/values/lebanon-production.yaml
```

### Edit (5 files)
```
clusters/platform/tenants/argocd/applicationsets/elephantos.yaml
clusters/platform/tenants/argocd/applicationsets/dataplatform/kafka-connectors.yaml
clusters/platform/tenants/argocd/applicationsets/dataplatform/components.yaml
clusters/platform/tenants/argocd/applicationsets/primarycare/primarycare-apps.yaml
clusters/platform/tenants/argocd/applicationsets/primarycare/primarycare-etls.yaml
```
