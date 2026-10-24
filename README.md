# skills

Agent skills for Claude Code, Codex, Cursor and other agents.

Install one skill:

```sh
npx skills add chrisvasqm/skills --skill jira-cli
```

Or install all of them with `npx skills add chrisvasqm/skills`.

## Skills

- [jira-cli](skills/jira-cli/SKILL.md): use the [`jira`](https://github.com/chrisvasqm/jira-cli) CLI to work with Jira Cloud tickets, comments, boards and sprints.

## Adding a skill

Each skill is one folder, `skills/<name>/SKILL.md`, and must stand alone. Add it to the list above in the same PR.
