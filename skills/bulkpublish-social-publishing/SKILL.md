---
name: bulkpublish-social-publishing
description: "Use this skill when an AI agent must adapt, review, schedule, or publish approved social content across multiple platforms through BulkPublish."
license: Apache-2.0
platforms: [claude, codex, hermes]
required_environment_variables: []
requires_tools: [BulkPublish API or hosted MCP]
fallback_for_toolsets: ["Prepare and return platform-specific payloads without sending"]
metadata:
  author: azeemkafridi
  version: "1.0"
---

# BulkPublish Social Publishing

This skill handles the execution boundary between a reviewed social-media draft and a scheduled or published campaign. BulkPublish provides the API and hosted MCP used to create posts, schedule them, upload media, and retrieve resulting status. It is intended for marketing, creator, and growth agents that need one repeatable workflow across platforms while keeping human approval explicit.

## References

- BulkPublish API repository: https://github.com/azeemkafridi/bulkpublish-api
- BulkPublish MCP documentation: https://app.bulkpublish.com/docs
- Hosted MCP endpoint: https://mcp.bulkpublish.com/mcp
- Source social-media skills: https://github.com/azeemkafridi/bulkpublish-api/tree/main/skills/social-media-content-skills

## Instructions

1. Collect the approved copy, media, links, target platforms and account IDs, timezone, and requested schedule.
2. Adapt the content per platform without changing approved claims, disclosures, consent, links, or brand constraints.
3. Present the exact per-platform payload, media, targets, and schedule to the user.
4. Wait for explicit approval of that exact payload and target set before invoking any create, schedule, upload, or publish operation.
5. Use BulkPublish's API or hosted MCP to execute only the approved operation.
6. Retrieve every resulting status and report platform, account, operation, schedule, identifier, URL, and errors.

## Safety rules

- Treat scheduling and publishing as external side effects; approval must be current and specific.
- Never invent account IDs, media URLs, permissions, delivery results, or analytics.
- If an external call times out, query its status before retrying to avoid duplicate posts.
- Report partial success per platform; do not silently retry failed targets.
- Preserve platform disclosures, opt-outs, copyright notes, and human review requirements.
- If the API or MCP is unavailable, return prepared payloads and identify the blocked handoff instead of claiming publication.

## Output Format

Return a compact table with platform, account, operation, status, scheduled time, post identifier, public URL when available, and unresolved actions.
