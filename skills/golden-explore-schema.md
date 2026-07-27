---
name: Explore the Golden schema (entity types and predicates)
description: Resolve the Golden knowledge-graph schema — entity types and predicates — to build valid entity/query filters.
api: openapi/golden-openapi-original.json
operations:
  - public_api_schema_entityTypes_list
  - public_api_schema_entityTypes_retrieve
  - public_api_schema_predicates_list
  - public_api_schema_predicates_retrieve
---

# Explore the Golden schema

Entity and query filtering depends on **entity type ids** and **predicate
ids**. Use this skill to resolve the schema before filtering entities.

## Auth
Send your API key in the `apikey` header on every request.

## Steps
1. List entity types with `public_api_schema_entityTypes_list`:
   `GET /api/v2/public/schema/entityTypes/`
   Each `PublicAPIEntityType` has an `id`, `properties`, and the `predicates`
   that apply to it.
2. Inspect one type with `public_api_schema_entityTypes_retrieve`:
   `GET /api/v2/public/schema/entityTypes/{id}/`
3. List predicates with `public_api_schema_predicates_list`:
   `GET /api/v2/public/schema/predicates/`
   Each `PublicAPIPredicate` has `id`, `name`, `type`, `objectEntityTypes`,
   `objectChoices`, and `isFilterable`.
4. Inspect one predicate with `public_api_schema_predicates_retrieve`:
   `GET /api/v2/public/schema/predicates/{id}/`
5. Use the resolved ids as `entityTypeIds` / `predicateIds` /
   `filterPredicateId` when calling the entity and query skills. Only
   predicates with `isFilterable: true` can be used in `filterPredicateId`.

## Notes
- Responses are cursor-paginated (`next`/`previous`/`results`).
- Handle `403`/`404`/`429` per errors/golden-problem-types.yml.
