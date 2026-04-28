# Mulholland

Foundry-style data platform. Postgres is the platform; PostgREST is the
API; everything composes around them.

## Open-source pieces

These are the parts of the platform we develop in the open. Each is a
standalone npm package — point it at any Postgres and it works. Inside
our private monorepo they compose into a single deployable; outside,
they're independently usable.

| Package | What it does |
|---|---|
| [**core**](https://github.com/Mulholland-Inc/core) | Shared platform primitives: typed `Db` wrapper over the postgres driver, structured errors, logging, transactions. Every package below depends on it. |
| [**basin**](https://github.com/Mulholland-Inc/basin) | Postgres-backed data warehouse — typed entity tables + connector landing zone. |
| [**arroyo**](https://github.com/Mulholland-Inc/arroyo) | Connector framework. Pulls records from sources, lands them in basin. Ships with deterministic mock connectors for tests and demos. |
| [**atlas**](https://github.com/Mulholland-Inc/atlas) | Ontology builder. Derives entity types, attributes, and relations by introspecting `information_schema` + `pg_constraint` over basin (or any schema). |
| [**monorail**](https://github.com/Mulholland-Inc/monorail) | Postgres-backed agent runtime. Bring your own pg client; runs Anthropic-powered agents with tool use, channels, and a durable event log. |

## Conventions

- **Standalone-first.** Every package can `attach({ connectionString })`
  against any Postgres without the rest of the platform present.
  Soft-dep on auth helpers — RLS enforced when running inside the
  full stack, off otherwise.
- **PostgREST is the only HTTP listener.** Tables are reachable as
  `/<table>`; functions as `/rpc/<fn>`. RLS is the security boundary.
- **Roles.** `anonymous < viewer < editor < admin < owner`. No prefix.
- **TypeScript everywhere.** Strict (`@tsconfig/strictest`),
  ESM-only, Node 22+.

## License

MIT for everything in `packages/*` unless otherwise stated.

## Contact

[mulholland.inc](https://mulholland.inc)
