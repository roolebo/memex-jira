# memex-jira

A [memex] adapter for the `tracker` role in JIRA. The role is specified
in memex's [tracker.md].

## Reaching JIRA

ADDR is the base URL of the server. The adapter uses `/rest/api/2/`.
With credentials, from JIRA_USER and JIRA_PASSWORD (the password or API
token) or else from `~/.netrc` for ADDR's host, it logs in with them;
without them, it reads what JIRA shows anyone.

`detect` prints nothing.

## Commands

    issue ISSUE     issue/ISSUE and its comment
    search          search on Server, search/jql on Cloud, as
                    serverInfo's deploymentType says; the QUERY is JQL
    comment ISSUE   POST issue/ISSUE/comment
    transition ISSUE STATUS
                    POST issue/ISSUE/transitions, the transition whose
                    `to.name` is STATUS

All capabilities are true.

## Issue

- ISSUE is the issue key.
- `title`: `summary`; `type`, `status`, `priority`: their `name`.
- `closed`: `status.statusCategory.key` is `done`.
- `url`: ADDR/browse/ISSUE.
- `text`: `description`.
- `related`: `issuelinks`, TYPE their `outward` or `inward` name
  as seen from ISSUE, e.g. `is blocked by`; `parent`, TYPE `parent`;
  `subtasks`, TYPE `subtask`.
- `basis`: `updated`.
- `links`: `issue`.

## Open questions

- Personal access tokens on Server?
- API v3 with ADF on Cloud, or v2 with wiki markup?
- `change` and `commit` in `links`: from remote links?
- `closed` from `statusCategory`, or from `resolution`?

[memex]: https://github.com/roolebo/memex
[tracker.md]: https://github.com/roolebo/memex/blob/main/tracker.md
