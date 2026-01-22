# Infrastructure-Charts Territory Analysis Report

## Executive Summary

**Key Finding: Kenya and Nigeria are functionally identical in infrastructure-charts** - only naming differs. This confirms the infra-gitops analysis.

Pakistan has significant infrastructure differences (RapidCompute vs AWS), requiring separate configuration.

---

## 1. Service Inventory

**Total Services:** 46

```
admin-event-worker          api-admin                   api-billing
api-clinic-insurance        api-clinical-product        api-clinical-subscription
api-consultation            api-conversation            api-data-export
api-department              api-encounter               api-federation
api-imaging-study           api-insurance               api-inventory
api-investigation           api-legacy-authorisation    api-patient
api-patient-monstache       api-patient-queue           api-patient-register
api-patient-triage          api-payment                 api-prescription
api-price-list              api-reports-management      api-ui-default
api-visit                   audere-malaria-hourly       billing-event-worker
encounter-event-worker      facility-report-gen-monthly facility-report-gen-weekly
insurance-event-worker      inventory-event-worker      mfe-s3-gateway
observability-bigquery-ingestor  observability-gateway  orthanc
patient-register-worker     pouchii-funds-transfer-job  pouchii-kyc-status-job
primary-care-web-s3-gateway triage-event-worker         web-config-service
worker-prescription
```

---

## 2. Territory-Level Global Configuration

### Kenya vs Nigeria (IDENTICAL)
```yaml
# kenya.yaml
global:
  shortTerritory: 'ken'
  territory: 'kenya'

# nigeria.yaml
global:
  shortTerritory: 'nga'
  territory: 'nigeria'
```

**Difference:** Only the territory name. No feature flags, no infrastructure differences.

### Pakistan (DIFFERENT)
```yaml
global:
  shortTerritory: 'pak'
  territory: 'pakistan'
  cluster: rapidcompute-khi04-cluster          # Different cloud provider
  uniqueGateway:
    enabled: true
    name: edge-gateway
  imagePullSecrets:
  - name: ecr-credentials
  ssmPrefix: rapidcompute-khi04-cluster

primarycare-service:
  imagePullSecrets:
  - name: ecr-credentials
  vpa:
    enabled: true

web-s3-gateway:
  s3:
    server: rcns_ele-health.s3.rapidcompute.com  # RapidCompute S3
    server_proto: http                            # HTTP (not HTTPS)
    server_port: 80
    region: rc1                                   # RapidCompute region
```

### Ghana & Lebanon (DORMANT)
Only naming exists - no active deployments.

---

## 3. Services with Territory-Specific Overrides

### 3.1 api-conversation (CRITICAL DIFFERENCE)

| Territory | Status | Replicas |
|-----------|--------|----------|
| Kenya     | **DISABLED** | 0 |
| Nigeria   | **ENABLED** | 2 |
| Pakistan  | **DISABLED** | 0 |

**Impact:** WhatsApp/conversation functionality only runs in Nigeria.

### 3.2 mfe-s3-gateway (Pakistan only)
```yaml
# pakistan.yaml
web-s3-gateway:
  s3:
    bucket_name: mfe.elephantprimarycare.com
    server: rcns_ele-health.s3.rapidcompute.com
    server_proto: http
    server_port: 80
    region: rc1
  externalSecret:
    ssmKey: /rapidcompute-khi04-cluster/...
```

### 3.3 primary-care-web-s3-gateway (Pakistan only)
```yaml
# pakistan.yaml
web-s3-gateway:
  s3:
    bucket_name: primarycarewebelephantprimarycarecom
    server: rcns_ele-health.s3.rapidcompute.com
    server_proto: http
    server_port: 80
    region: rc1
  externalSecret:
    ssmKey: /rapidcompute-khi04-cluster/...
```

---

## 4. Territory-Agnostic Services (43 services)

All other services use only environment-level configs (`acceptance.yaml`, `production.yaml`) with no territory-specific overrides:

- All API services (except api-conversation)
- All event workers
- All cron jobs
- Observability stack
- Orthanc (imaging)

---

## 5. Cluster-Level Configurations

| Cluster | Territory | Key Settings |
|---------|-----------|--------------|
| amazon-acceptance-kaiho9 | Kenya/Nigeria | ESO secrets, edge-gateway |
| amazon-production-echot7 | Kenya/Nigeria | ESO secrets, replica_count: 0 (default) |
| pakistan-acceptance | Pakistan | ESO secrets, RapidCompute SSM prefix |
| pakistan-production | Pakistan | ESO secrets, VPA disabled |

---

## 6. Consolidation Recommendations

### Can Be Unified (Kenya + Nigeria)

| Item | Action |
|------|--------|
| Global territory config | Remove kenya.yaml, use single AWS config |
| All 43 territory-agnostic services | No changes needed - already unified |
| Cluster configs | Already shared (amazon-*) |

### Requires Decision (api-conversation)

**Current State:** Only enabled in Nigeria
**Options:**
1. Enable in Kenya if conversation feature is wanted
2. Keep disabled if Kenya doesn't need WhatsApp integration
3. If consolidating to single territory, just use Nigeria's config

### Must Remain Separate (Pakistan)

| Item | Reason |
|------|--------|
| Territory config | RapidCompute infrastructure |
| S3 gateway configs | Different S3 provider |
| Cluster configs | Different cloud entirely |

### Can Be Deleted (Dormant)

| Territory | Files to Remove |
|-----------|-----------------|
| Ghana | `territories/ghana.yaml` |
| Lebanon | `territories/lebanon.yaml` |

---

## 7. Summary Table

| Category | Kenya | Nigeria | Pakistan |
|----------|-------|---------|----------|
| Global config | Naming only | Naming only | Full infra diff |
| Services deployed | 46 | 46 | 46 |
| api-conversation | DISABLED | ENABLED | DISABLED |
| S3 gateways | AWS S3 | AWS S3 | RapidCompute S3 |
| Consolidation | **READY** | **READY** | **SEPARATE** |

---

## 8. Action Items

1. **Kenya/Nigeria consolidation:**
   - Decide on api-conversation (enable for both or keep Nigeria-only)
   - Territory naming is the only blocker - can be parameterized

2. **Clean up dormant territories:**
   - Delete `territories/ghana.yaml`
   - Delete `territories/lebanon.yaml`

3. **Pakistan:**
   - Must remain separate due to RapidCompute infrastructure
   - No consolidation possible with AWS territories
