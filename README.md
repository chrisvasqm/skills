# skills

Agent skills for Claude Code, Codex, Cursor and other agents.

Install one skill:

```sh
npx skills add chrisvasqm/skills --skill cleanup
npx skills add chrisvasqm/skills --skill jira-cli
npx skills add chrisvasqm/skills --skill test-cli
```

Or install all of them with `npx skills add chrisvasqm/skills`.

## Skills

- [cleanup](skills/cleanup/SKILL.md): review the changed code for reuse, simplification, efficiency and altitude issues, then fix them without changing behavior.
- [jira-cli](skills/jira-cli/SKILL.md): use the [`jira`](https://github.com/chrisvasqm/jira-cli) CLI to work with Jira Cloud tickets, comments, boards and sprints.
- [test-cli](skills/test-cli/SKILL.md): use the [`test-cli`](https://github.com/chrisvasqm/test-cli) CLI to work with TestRail cases, runs, tests and results, and link them to Jira tickets.

## Adding a skill

Each skill is one folder, `skills/<name>/SKILL.md`, and must stand alone. Add it to the list above in the same PR.
