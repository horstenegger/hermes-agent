# Claude Code Review instructions

## Review goal

Find correctness, security, data integrity, deployment, and product behavior bugs introduced by the PR. Prefer fewer high-confidence findings over broad advice.

## What counts as Important

Mark a finding Important only when it is likely to break production behavior, leak or expose private data, weaken authentication or authorization, corrupt data, break deployment, damage SEO/indexing, or make rollback harder.

## Nits

Report at most five Nits per review. Do not comment on formatting, lint, spelling, import order, or style that CI already enforces. If all findings are nits, lead the summary with `No blocking issues.`

## Always check

- Secrets, tokens, API keys, auth bypasses, unsafe logs, and PII exposure.
- Edge cases around empty data, permissions, concurrency, retries, and partial failures.
- GitHub Actions token permissions, unsafe `pull_request_target` use, and untrusted checkout patterns.
- Web and SEO repos: canonical URLs, noindex/robots behavior, hreflang, structured data, redirects, city or intent page routing, and Cloudflare deployment behavior.
- Database or migration changes: backwards compatibility, data loss, rollback safety, and tenant scoping.
- Missing tests only when the changed behavior is risky enough that a real bug could ship unnoticed.

## Do not report

- Generated files, build output, minified assets, vendored code, or lockfiles unless the dependency change itself is suspicious.
- Pure formatting diffs.
- Refactors that are only taste preferences.
- Existing issues not made worse by the PR, except as Pre-existing.

## Verification bar

Before posting a finding, cite the exact file and line evidence and explain the user-visible or production consequence. If uncertain, do not post an inline comment.
