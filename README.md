# AI Skills Agent Release

`skills-release-agent` is the Agent-market release package for `skillsaiagent/aiskills`.

It uses the same generated package format as `skills-release`, but its catalog is filtered by live OpenClaw/Hermes Skills Hub hot skill ids. Only ids that already exist in the local AI Skills export catalog are published here.

## Export

From the service submodule:

```bash
cd ../ai-skills-service
npm run skills-release-agent:export
```

The export writes:

- `canonical-skills.json`
- `skills.json`
- `skills.md`
- `skills/<skill-id>/SKILL.md`
- each skill package's generated `references/` and `scripts/`

The command fails if the OpenClaw/Hermes hot source cannot be fetched, if no valid hot ids are parsed, or if none of those ids match the local catalog.

## Search Sync

The shared checker/sync scripts keep their old defaults for `skills-release`. Use explicit arguments for this package:

```bash
node ../scripts/check-skills-release-search.mjs \
  --release-root skills-release-agent \
  --source skillsaiagent/aiskills \
  --expected-count skip

node ../scripts/sync-skills-release-search.mjs \
  --yes \
  --source skillsaiagent/aiskills
```

## Repository

Remote: `git@github.com:skillsaiagent/aiskills.git`

This package is intended to be managed as a separate Git repository/submodule once the remote has an initial commit.
