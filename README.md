<!-- Copyright The Linux Foundation and each contributor to LFX. -->
<!-- SPDX-License-Identifier: MIT -->

# lfx-mcp-playbooks

Playbooks for agents that answer questions through the **LFX MCP server**:
which tool answers which kind of question, in what order, with what
discipline, and how the resulting figure is stated and sourced.

A playbook is not a manual for a tool. Each LFX MCP query lane ships its own
guidance document, read through a tool call
(`read_lfx_standard_metrics_guidance`, `read_lfx_semantic_layer_guidance`),
and those documents own the parameters, the groupings, the switches, the
defaults, the stored literals and the worked calls. The playbooks here sit
one level up: they say which lane to take for which job, what to resolve
before querying, what an answer must state, and how a deck's figures stay
consistent with one another — and they point to the guidance for everything
else. When a playbook and a guidance document disagree, the guidance is
current and the playbook is behind.

## Who this is for

An agent session (Claude Code, Cowork, or any MCP client) connected to the
LFX MCP server, working for people whose figures end up in board decks,
member communications and public claims. The bar is reproducibility: a
figure is quoted with the lane, scope, window and population that produced
it, so the same question re-run gives the same answer.

## The skills

| Skill | What it is for |
|---|---|
| [`lfx-data-querying`](skills/lfx-data-querying/SKILL.md) | Answering one quantitative question: the four lanes, the routing decision, name and value discovery, the reader's-words answer with its provenance block, and the traps that return a plausible wrong number instead of an error. |
| [`lfx-deck-building`](skills/lfx-deck-building/SKILL.md) | Producing a deck's worth of figures: the conventions fixed before the first query, cross-framing checks, the data-notes appendix, the final consistency pass, and what LFX cannot reproduce and how to cite it instead. |

Each skill is a `SKILL.md` entry point plus a `references/` file loaded on
demand.

## Evidence

The traps and the disciplines here come from a triage of wrong answers
against expert reference figures, and from verification against the live
tools; nothing is folklore. The data is fluid, so the playbooks carry no
figures of their own — every number in a deliverable comes from a fresh
call.

## Installing

The repository is a Claude Code plugin and its own single-plugin
marketplace. From Claude Code:

```
/plugin marketplace add /path/to/lfx-mcp-playbooks
/plugin install lfx-mcp-playbooks@lfx-mcp-playbooks
```

The skills then load as `/lfx-mcp-playbooks:lfx-data-querying` and
`/lfx-mcp-playbooks:lfx-deck-building`. Alternatively, copy or symlink the
skill directories into the agent's skill path (for Claude Code:
`.claude/skills/` in the project, or `~/.claude/skills/` for the user).

## A note to readers

The playbooks are written to a few standing rules, and a reader should hold
them to those rules:

- **No figures.** A playbook never carries a count, a revenue, or a
  measured ratio. Where an order of magnitude helps ("several times",
  "an order of magnitude"), it is qualitative; anything measured carries
  the date it was measured and an instruction to re-run.
- **Only deployed tools.** Every tool named exists on the deployed LFX MCP
  server. Nothing is described as coming.
- **Parameters live in the guidance.** A playbook names a lane and a job;
  the guidance document names the parameter.
- **Answers in the reader's words.** Prose for the person who asked; field
  names, keys and tool names in the provenance block, not the sentence.
- **Regions are provisional.** The LF region grouping is pending
  stakeholder sign-off; every recommendation of a region grouping says so.
