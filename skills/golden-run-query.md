---
name: Run a Golden Query and read its results
description: Fetch the entity results of a Golden Query (by permalink or id) and page through them with citations.
api: openapi/golden-openapi-original.json
operations:
  - public_api_queries_permalink_list
  - public_api_queries_results_list
---

# Run a Golden Query and read its results

A Golden **Query** returns a curated, citation-backed list of entities (for
example, "companies in the artificial intelligence industry"). Use this skill
to fetch a query's results and page through them.

## Auth
Send your API key in the `apikey` header on every request. There is no OAuth.

## Steps
1. If you have a query **permalink** (e.g. `companies-in-the-artificial-intelligence-ai-industry-EP58R`),
   call `public_api_queries_permalink_list`:
   `GET /api/v2/public/queries/permalink/{permalink}/`
2. If you have a query **id**, call `public_api_queries_results_list`:
   `GET /api/v2/public/queries/{id}/results/`
3. Read `results[]` (entities). Each entity carries `properties[]`, where each
   property value has `instances[]` with `citations[]` (title + url) — surface
   the citations, do not present values as unsourced facts.
4. Page with cursor pagination: follow the `next` URL (opaque `cursor`), and
   set `pageSize` to control page length. Stop when `next` is null.

## Error & rate-limit handling
- `403 permission_denied` — key missing/invalid or plan lacks access.
- `404 not_found` — the permalink/id does not exist.
- `429 throttled` — back off and retry after the throttle window.
- Errors are JSON with `code` / `detail` / `attr` (see errors/golden-problem-types.yml).
