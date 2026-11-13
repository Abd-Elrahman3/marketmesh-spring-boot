# Getting Started

## 1. Prerequisites

Finish the first five starters. Choose Java 21+ and a supported stable Spring Boot release, record exact versions, and create your own Maven/Gradle build. Docker and a CI runner are needed for the specified integration tests.

## 2. Clone and read

```bash
git clone https://github.com/Abd-Elrahman3/marketmesh-spring-boot.git
cd marketmesh-spring-boot
git switch -c feature/m1-domain
```

Read README sections 1–5, then SHARED_MILESTONES.md. Use one branch per milestone and one small testable rule per commit.

## 3. Design before code

Create an ERD, API contract and a state-transition table from the README. Write ADRs for storage ownership, consistency and failure recovery. Build a walking skeleton with a health endpoint, one migration and one real-database test, then implement M1 in small steps. Add CI that builds and runs cumulative acceptance tests; document the exact commands here after choosing the build.

Keep this repository as your project: adding code during implementation is expected. The delivered starting repository intentionally contains only README and Markdown requirement documents. There is no script or build to run yet.

## Troubleshooting

- Dependency resolution: check JDK version, proxy/CA settings and access to Maven Central; never disable TLS verification.
- Database connection: inspect `docker compose ps`, port mapping and application variables. Use `docker compose logs postgres` for the specific error.
- Red learning tests: read the rule ID in the failure and implement the next missing behavior.
- Docker unavailable in CI: use a Docker-capable runner; do not replace database concurrency tests with mocks.
- Data reset: `docker compose down` preserves named volumes. `down -v` destroys local data; use it only when intentionally resetting your own development fixtures.
