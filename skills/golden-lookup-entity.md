---
name: Look up an entity and its properties
description: Find entities in the Golden knowledge graph and retrieve a single entity's citation-backed properties.
api: openapi/golden-openapi-original.json
operations:
  - public_api_entities_list
  - public_api_entities_retrieve
---

# Look up an entity and its properties

Use this skill to search the Golden knowledge graph for entities and read a
single entity's properties.

## Auth
Send your API key in the `apikey` header on every request.

## Steps
1. To find entities, call `public_api_entities_list`:
   `GET /api/v2/public/entities/`
   Narrow the set with query parameters:
   - `ids` — comma-separated entity ids
   - `entityTypeIds` — restrict to entity types (from the schema endpoints)
   - `predicateIds` — restrict which properties are returned
   - `filterPredicateId` + `filterValue` — filter by a predicate value
   - `cursor`, `pageSize` — cursor pagination
2. To read one entity, call `public_api_entities_retrieve`:
   `GET /api/v2/public/entities/{id}/`
3. Parse `properties[]`: each `PublicAPIEntityProperty` has a `predicateId`
   and `instances[]`; each instance carries a value and `citations[]`
   (title + url). Always surface the citations.

## Notes
- Resolve `predicateId`/`entityTypeIds` via the schema-explore skill first.
- Handle `403`/`404`/`429` per errors/golden-problem-types.yml; page via `next`.
