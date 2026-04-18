# kubepave-tenant-requests

⚠️ **This repository is managed by Crossplane. Do not edit manually.**

This repository is the GitOps entry point for submitting tenant requests in Kubepave.

Users define desired tenants by creating TenantRequest manifests, which are validated and processed by the platform.

## Flow
```
kubepave-tenant-requests (Git)
        ↓
Argo CD
        ↓
Kubernetes (TenantRequest)
        ↓
Crossplane Function
  - Validate
        ↓
Approval Gate (manual or automated)
        ↓
Crossplane Function
  - Generate tenant configuration
  - Push to kubepave-tenants repository
        ↓
kubepave-tenants (Git)
        ↓
Argo CD
        ↓
Helm (rendering)
        ↓
Kubernetes (Tenant resources)
```

## Structure
```
requests/<tenant-name>/request.yaml
```

## Notes

- This repository is **user-managed**
- Each file represents a TenantRequest
- Requests are validated before being accepted and transformed into tenant configurations
- Changes here trigger the tenant provisioning workflow
