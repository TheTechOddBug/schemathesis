# Schemathesis Trophy Case

Real-world defects uncovered by Schemathesis’ property-based testing engine.

## Bug Categories

| Type | Description |
| --- | --- |
| 💥 Server Crashes | 5xx responses or crashes triggered by unexpected inputs |
| 📋 Schema Violations | Responses that violate the published contract |
| 🚪 Validation Bypass | Invalid or malicious data accepted by the API |
| 🔗 Integration Issues | Incompatibilities between clients and servers |

## Submitting a Trophy

<div align="center" markdown>

[Submit a Trophy :fontawesome-solid-trophy:](https://github.com/schemathesis/schemathesis/issues/new?template=trophy-submission.yml){ .md-button .md-button--primary }

</div>

!!! info "What we're looking for"
    Bugs in APIs that other developers use or recognize (open-source projects with active communities, public SaaS APIs, popular tools).

    Security vulnerabilities should follow responsible-disclosure rules; only document them here once the fix is public.

## Discoveries

| Project | Type | What Schemathesis found |
| --- | --- | --- |
| [vLLM](https://github.com/vllm-project/vllm/issues/52088) | 💥 Server Crashes | `POST /v1/messages` returned 500 when `stop_sequences` carried more than four items. |
| [vLLM](https://github.com/vllm-project/vllm/pull/54402) | 💥 Server Crashes | An empty trace-replay token list returned 500 instead of a client error. |
| [Qdrant](https://github.com/qdrant/qdrant/pull/8762) | 💥 Server Crashes | Validation panicked when two sibling items failed at once, dropping the connection without a response. |
| [Qdrant](https://github.com/qdrant/qdrant/issues/9869) | 🚪 Validation Bypass | Write operations accepted `timeout=0` although the schema declares `minimum: 1`. |
| [OpenObserve](https://github.com/openobserve/openobserve/pull/14089) | 💥 Server Crashes | Two handler panics reachable from query parameters — a divide by zero on `?limit=0` and an `unwrap()` on `?query=`. |
| [OpenObserve](https://github.com/openobserve/openobserve/pull/13952) | 💥 Server Crashes | A control byte in a field name made header construction fail, replacing the handler's 400 with a bare 500. |
| [Ory Kratos](https://github.com/ory/kratos/issues/2963) | 📋 Schema Violations | A sweep of the public API found responses and status codes that the shipped OpenAPI definition does not describe. |
| [Goa](https://github.com/goadesign/goa/issues/2840) | 📋 Schema Violations | The framework's default error responses — 400, 408, 500, 503, 504 — never reach the generated document. |
| [TypeSpec](https://github.com/microsoft/typespec/issues/11747) | 📋 Schema Violations | The SSE emitter produced an unsatisfiable `oneOf` branch, so a conforming validator rejected every frame. |
| [Huma](https://github.com/danielgtaylor/huma/issues/1042) | 💥 Server Crashes | `uniqueItems` validation ran before type casting, crashing the server thread on certain primitive inputs. |
| [CivetWeb](https://github.com/civetweb/civetweb/issues/1422) | 🔗 Integration Issues | Unsupported HTTP methods answered 400 instead of 405. |
| [API Platform](https://github.com/api-platform/core/issues/3450) | 💥 Server Crashes | A large `page` value returned 500 — the offset overflowed into a float where an integer was required. |
| [Horse](https://github.com/HashLoad/horse/issues/500) | 🔗 Integration Issues | 405 responses omitted the `Allow` header required by RFC 9110. |
| [Vert.x OpenAPI](https://github.com/eclipse-vertx/vertx-openapi/issues/124) | 💥 Server Crashes | Query parameters were percent-decoded twice during validation, so `%25` reached the handler as a 500. |
