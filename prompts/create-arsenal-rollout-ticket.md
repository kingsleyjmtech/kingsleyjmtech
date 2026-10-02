You are creating ONE ticket in Linear. Do not write code, open pull requests or change any repository. Your only output is the ticket.

## Goal of the ticket
Turn on every plugin from the `kingsleyjmtech/kjm-claude-arsenal` Claude Code plugin marketplace in every private repository owned by `kingsleyjmtech`. To do that, commit the settings below to each repo as `.claude/settings.json`. Claude Code (local and cloud sessions) then loads the plugins automatically in that repo.

## Steps
1. List every private repository owned by `kingsleyjmtech`. Use the GitHub tools if you have them. If you don't, use the list under "Known private repos" below. Do not guess or invent repo names.
2. Remove `kingsleyjmtech/kjm-claude-arsenal` from the list. It is the marketplace itself and already has its own settings.
3. Find the Linear team to file under. If there is exactly one team, use it. If there are several and none is obviously right, stop and ask me which team to use.
4. Search Linear for an existing open ticket about rolling out kjm-claude-arsenal settings. If one exists, stop and give me its link instead of creating a duplicate.
5. Create the ticket using the template below. Fill in the repo checklist from step 1. Copy the JSON exactly, character for character.
6. Reply with only the ticket's link and the number of repos in its checklist.

## Known private repos (fallback for step 1)
kjm-all-api-test, kjm-ansible, kjm-auth-ms, kjm-contact-forms-ms, kjm-cp-app, kjm-cp-app-e2e, kjm-devin-arsenal, kjm-emails-ms, kjm-faqs-ms, kjm-git-ms, kjm-ip-intel-ms, kjm-logs-ms, kjm-main-site, kjm-model-warmup, kjm-opencode-arsenal, kjm-portal-ms, kjm-repo-mirror, kjm-repo-toolkit, kjm-smses-ms, kjm-storage-ms, kjm-telegram-ms
(all owned by `kingsleyjmtech`)

## Ticket template

**Title:** Enable all kjm-claude-arsenal plugins in every private repo

**Description:**

### Why
The plugins in `kingsleyjmtech/kjm-claude-arsenal` are only available in repos that declare them. Committing a shared `.claude/settings.json` to each private repo makes all of them load automatically in every Claude Code session, including cloud sessions, which start in a fresh container with no user-level settings.

### What to add
Path in each repo: `.claude/settings.json`

```json
{
  "extraKnownMarketplaces": {
    "kjm-claude-arsenal": {
      "source": {
        "source": "github",
        "repo": "kingsleyjmtech/kjm-claude-arsenal"
      }
    }
  },
  "enabledPlugins": {
    "kjm-git-autopilot@kjm-claude-arsenal": true,
    "kjm-laravel@kjm-claude-arsenal": true,
    "kjm-spring@kjm-claude-arsenal": true,
    "kjm-vue@kjm-claude-arsenal": true,
    "kjm-ansible@kjm-claude-arsenal": true,
    "kjm-playwright@kjm-claude-arsenal": true,
    "security-agent@kjm-claude-arsenal": true,
    "kjm-agent-hub@kjm-claude-arsenal": true,
    "kjm-meta@kjm-claude-arsenal": true
  }
}
```

### Rules
- **If the repo has no `.claude/settings.json`:** create it with the JSON above.
- **If the repo already has one:** merge, don't overwrite. Add the `kjm-claude-arsenal` entry to `extraKnownMarketplaces` and the nine entries to `enabledPlugins`. Keep every other existing key and value, such as permissions, hooks and env.
- **If a repo explicitly sets one of these plugins to `false`:** leave it `false` and note it on this ticket.
- **Check the JSON before committing:** it must be valid, for example by running `python3 -m json.tool .claude/settings.json`.
- **Branch and PR:** work on a ticket branch cut from `development`, or from the default branch if the repo has no `development` branch. Open one PR per repo with a Conventional Commit, such as `chore: enable kjm-claude-arsenal plugins`. Never commit directly to `master`, `main`, `staging` or `development`.

### Repos
- [ ] kingsleyjmtech/<repo> (one line per repo from step 1)

### Acceptance criteria
- Every repo in the checklist has a merged PR adding or merging `.claude/settings.json` as above.
- In one repo, a fresh Claude Code cloud session shows the arsenal's agents and skills. This proves the private marketplace can be fetched from a cloud session.
- Any repo where `kjm-git-autopilot` gets in the way of cloud sessions (its Stop hook forces commit and push) is listed on this ticket with that plugin set to `false`.

**Labels:** chore, tooling (only if those labels already exist; do not create labels)
**Priority:** Medium
