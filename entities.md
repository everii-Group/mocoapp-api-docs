---
layout: default
title: Entities
has_children: true
---

# Entities

## Global Filters

All list/index endpoints offer a common set of filters.

### Filter `ids`

Usage: `GET /api/v1/entities?ids=123,456`

Allows you to filter by IDs and fetch multiple entities comma-separated

### Filter `updated_after`

Usage: `GET /api/v1/entities?updated_after=2022-04-20T09:17:58Z` (ISO8601 timestamp)

Enables you to give a timestamp for all entities that are created or updated after this timestamp, especially useful for synchronisation purposes.

Combine it with a [webhook subscription](webhooks) on DELETE for the entity to have a complete synchronisation.
