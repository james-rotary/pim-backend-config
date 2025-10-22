# pim-backend-config

Argo CD configuration repo for the PIM backend API.

Structure:
- `base/` – Core manifests (namespace, deployment, service, migration job, secret refs)
- `overlays/dev/` – Environment-specific patches (image tag, replicas, optional env vars)

Migrations:
- Schema migrations live in the source repo (`pim-backend-api`). This config repo includes a PreSync Job to run them before the Deployment rolls.

Secrets:
- Demo references a plain secret name `pim-backend-db-url`. Replace with SealedSecret or ExternalSecret integration for real environments.

Sync Order:
- PreSync migration job annotated; Argo CD runs it, then applies Deployment.