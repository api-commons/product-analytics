# Product Analytics

The common product-analytics vocabulary -- the events a product tracks, the people and profiles they belong to, the cohorts those people are grouped into, and the funnels, insights and dashboards built on top -- distilled from the APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Customer Data Platform, CDP, Product Analytics, Web Analytics, Mobile Analytics, Event Tracking, Behavioral Analytics, Digital Analytics in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| event | 40 | 35 |  | events 25, track 12, event 10, batch 2 |
| profile | 15 | 13 | traits 62%, user_id 54% | identify 6, profiles 4, people 2, profile 2 |
| cohort | 14 | 12 | id 75%, name 75%, description 67%, created_at 58% | segments 9, cohorts 2, segment 2, cohort 2 |
| dashboard | 4 | 3 | id 100%, name 100% | dashboards 3, dashboard 2 |
| funnel | 7 | 6 | name 50% | funnels 4, funnel 3 |

Cohort: 80 providers with harvested OpenAPI, 40 crosswalks. Of the providers exposing a event: 75% create, 40% list, 25% fetch, 2% update, 8% delete. Generated 2026-11-10 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- An event agrees on nothing outright: user, properties and timestamp sit at 37-43%. Tracking APIs share a shape -- event name, properties, user, time -- but publish it as a request body with names that vary (event, event_type, name; distinct_id, userId), and several document the endpoint without a schema at all.
- A cohort agrees on id, name, description and created_at; segments and cohorts are one concept across CDPs and analytics tools.
- A profile agrees on a user id and its traits -- the Segment `identify` model.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- The bare Analytics tag is not used: it covers business intelligence, data platforms and market analytics, not product event tracking.
- `track`, `capture`, `collect` and batch-beneath-track are events; `identify`, persons, people and profiles are profiles; segments are cohorts.
- Everything but the event `requires: [event]`, so a marketing tool's `/segments` counts only if it also tracks events.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
