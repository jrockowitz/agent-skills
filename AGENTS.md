# Shared agent skills

This repository supplies skills to the `drupal_playground` checkout and its worktrees.
Each checkout has two links under `.agents/skills/`:

- `_shared` → `~/Sites/agent-skills/custom`: repository-owned skills and their supporting files.
- `_skills.sh` → `~/Sites/agent-skills/.agents/skills`: third-party skills installed from
  `skills-lock.json`. Installed files are ignored by Git.

On a new checkout or after installed third-party skills have been removed, restore them
from `skills-lock.json` by running this command from `~/Sites/agent-skills`. The files are
already present during normal use, so the command does not need to run each session:

```bash
npx --yes skills experimental_install --agent codex --frozen-lockfile
```

`npx --yes` runs the skills CLI without an installation prompt. `experimental_install`
restores the locked skills; `--agent codex` targets Codex; `--frozen-lockfile` keeps the
existing lock file unchanged.

A single link to the repository did not expose the nested `drupalorg-cli` skill in a fresh
Codex session. The cause was not established: depth and the hidden `.agents` directory are
both possible factors. The two links expose both groups at the same visible depth. Codex's
[discovery source](https://github.com/openai/codex/blob/main/codex-rs/ext/skills/src/loader/discovery.rs)
handles scan depth and hidden directories; the [skills guide](https://developers.openai.com/codex/skills)
describes discovery locations and symlinks. Verify discovery in a fresh Codex session after
changing the layout.
