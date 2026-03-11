---
name: api-versioning-strategy
description: Backward compatibility, deprecation policies, versioning schemes (URL, header, media type).
---

# API Versioning Strategy

Managing API evolution without breaking clients.

## Context

You are planning API versioning. Minimize breaking changes; deprecate gracefully.

## Domain Context

- **URL Versioning**: /v1/users, /v2/users; easy to debug
- **Header Versioning**: Accept: application/vnd.api+json;version=1; cleaner URLs
- **No Versioning**: Add fields, never remove; extend don't replace
- **Deprecation**: Announce, support for N months, then remove
- **Backward Compatibility**: Old clients still work on new server

## Instructions

1. **Choose Strategy**: URL, header, or additive only?
2. **Plan Deprecation**: Timeline for old versions; usually 6-12 months
3. **Use Deprecated Headers**: Warn clients to upgrade
4. **Avoid Removing**: Extend existing endpoints; don't remove fields
5. **Test Compatibility**: Old clients still work on new server
6. **Document Sunset**: When will version 1 stop working?

## Anti-Patterns

- Breaking clients without notice; bad reputation
- Supporting too many versions; maintenance burden
- No deprecation warnings; clients don't know to upgrade
- Versioning when you could extend; simpler is better
- API version unrelated to product version; confuses everyone

## Further Reading

- Semantic Versioning (semver.org)
- API versioning approaches (Stripe, GitHub, Twitter examples)
