# Database Modernization Pipeline

A proof-of-concept portfolio project that demonstrates automated database schema modernization. Changes flow from version control through CI/CD into a containerized Liquibase runner that applies migrations to MySQL.

## Architecture Flow

```
Developer → Git Push → GitHub Actions → Docker → Liquibase → MySQL
```

1. **Developer** commits schema changes (Liquibase changelogs) and pushes to GitHub.
2. **GitHub Actions** triggers the deployment workflow on push.
3. **Docker** builds or runs an image that packages the Liquibase CLI and project changelogs.
4. **Liquibase** connects to the target database and applies pending migrations.
5. **MySQL** receives the updated schema.

## Technologies Used

| Technology | Role |
|------------|------|
| GitHub Actions | CI/CD pipeline orchestration |
| Docker | Consistent Liquibase execution environment |
| Liquibase | Database schema change management and versioning |
| MySQL | Target relational database |

## Future Enhancements

This PoC runs locally and in GitHub Actions with a simple MySQL target. A production-style evolution could move the same pipeline pattern onto AWS:

- **Amazon RDS** — Managed MySQL (or compatible) instance as the migration target, replacing self-hosted or CI service containers.
- **Amazon ECS** — Run the Liquibase Docker image as a scheduled or on-demand task, triggered after image build in CI, instead of executing migrations only inside the Actions runner.

Other improvements (out of scope for this repo) might include environment-specific changelogs, approval gates, and integration with broader platform tooling. AWS resources are not provisioned here; they are documented only as a possible future-state architecture.
