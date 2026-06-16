# Mulholland

Internal engineering. Our infrastructure is split into three repositories by scope:

- **[marzy](https://github.com/Mulholland-Inc/marzy)** — the multi-tenant SaaS
  platform. Each tenant gets an isolated setup (own VPC, database, and Cloud Run
  service) driven from one Terraform root.

- **[marzy-healthcare](https://github.com/Mulholland-Inc/marzy-healthcare)** — a
  HIPAA-isolated healthcare product: a headless Sikka → Google Healthcare API
  (FHIR) eligibility pipeline. It lives in its own project so regulated data
  stays separate from the SaaS platform.

- **[marzy-platform](https://github.com/Mulholland-Inc/marzy-platform)** —
  org-wide control plane: shared compliance and security infrastructure that
  spans the other projects.

Each repo owns its own Terraform and remote state. See each repo's README for details.
