<!-- Copyright The Linux Foundation and each contributor to LFX. -->
<!-- SPDX-License-Identifier: MIT -->

# Contributing to lfx-mcp-playbooks

This file guides agents and contributors changing **this repo**: editing a
playbook, adding a reference, running the evals, shipping a change. For what
the plugin does and how to install it, see [README.md](README.md).

## What this repo is

Three skills that teach a client agent how to work with the LFX MCP
server: `lfx-data-querying` (which tool answers which kind of question,
discovery, an answer with its provenance), `lfx-figure-checking` (a stated
figure against a fresh read: the mechanisms behind two numbers for one
question, the traps, the verdict and the written check) and
`lfx-deck-building` (a deck's worth of figures that stay consistent with
each other: conventions, cross-framing checks, the data-notes appendix,
what LFX cannot reproduce). The querying and deck skills hand checks to
the checking skill; it takes its fresh reads from the querying skill.
Distributed as a Claude Code plugin and as the
`lfx-mcp` marketplace (`.claude-plugin/`), with `skills/` auto-discovered;
the same directories work as plain Agent Skills in any client that reads
`SKILL.md`. There is no versioning: `main` is the release.

```text
skills/<name>/
├── SKILL.md            # the playbook: frontmatter, license header, body under ~400 lines
├── references/         # loaded on demand; the body says when to read each
└── evals/evals.json    # the test prompts and assertions for the skill-creator loop
```

## The one boundary that matters

**The tool guidance owns the mechanics of a call; a playbook owns the work.**
Each LFX MCP query lane ships its own guidance document, read through a
tool call (`read_lfx_standard_metrics_guidance`,
`read_lfx_semantic_layer_guidance`), and those documents plus the tool
descriptions own every parameter, grouping, switch, default, literal, error
and worked call. The playbooks say which tool for which job, in what order,
how the same figure differs across tools and why, and how an answer is
worded and sourced. Before writing a line, ask which side it belongs on:

- A sentence that names a parameter, a value of a switch, a column, or a
  query shape belongs in the guidance. Route it to the lfx-mcp maintainers
  and write nothing here.
- A sentence about routing, order, discovery, reconciliation, wording or
  provenance belongs here. It may quote the guidance's own words, never
  restate them.

Where a playbook and the guidance disagree, the guidance is current and the
playbook is behind: fix the playbook.

## Standing rules

Every change is held to these; a reviewer checks each one.

1. **No figures.** A playbook never carries a count, a value, a share or a
   measured ratio, not even as an example. Orders of magnitude are
   qualitative ("several times", "an order of magnitude"). The data is
   fluid; every number in a deliverable comes from a fresh call.
2. **Only deployed tools.** Every tool, family, metric and dimension named
   exists on the deployed LFX MCP server today. Nothing is described as
   coming. A line that needs something not yet deployed carries, on one
   line, `[not yet in production: <what> — until then: <fallback>]`, and
   the fallback is what the playbook does today.
3. **Answers in the reader's words.** Prose for the person who asked; tool
   names, field names, keys and SQL stay in the provenance, not the
   sentence. A default that was applied is stated as if chosen.
4. **Mechanisms, not folklore.** A "why figures differ" entry or a gotcha
   says what each tool counted and the mechanism that separates them,
   verified against the live tools. Nothing goes in because it sounds
   plausible.
5. **Regions are provisional.** The LF region grouping is pending
   stakeholder sign-off; anything that recommends a region grouping says
   so.
6. **The deck playbook governs the figures, not the slides.** How a deck
   is written, designed or produced belongs to the reader's own tools.

Scans that must come back empty before a commit (run from the repo root):

```text
grep -rnE '[0-9]{3,}|\$[0-9]|[0-9]+%' skills/ | grep -vE '20[0-9]{2}-[0-9]{2}-[0-9]{2}|<yyyy|<n>|evals\.json|365 complete|"in 2025"'
grep -rn 'not yet in' skills/ | grep -v 'not yet in production'
```

The two exclusions at the end of the first scan are the known benign hits
(a day count that defines a trailing year, and a forbidden-phrase example);
a new hit is a figure until proven otherwise.

## Changing a playbook

1. **Read the live guidance first**, through the tool calls above against
   the deployed server, and read the relevant section of the playbook and
   its references. Most proposed additions turn out to be either already
   in the guidance (then a pointer is enough) or a mechanics line that
   belongs there.
2. **Verify the claim against the live tools** before writing it: the
   `applied` block of a standard-metric result, the compiled SQL, an
   explore call on the semantic layer, a record from a service tool.
   Remembered names and behaviours are frequently wrong.
3. **Put it where it belongs.** A rule the agent needs on every question
   goes in the SKILL.md body, in the section that already covers that
   step; a mechanism goes in the checking skill's
   `references/why-figures-differ.md` or `references/gotchas.md`; an
   everyday word and its default reading in the querying skill's
   `references/plain-words.md`; a deck-section recipe in the deck skill's
   pattern references. A pointer across skills names the skill and the
   entry, never a relative path into another skill's directory. Say a thing once and point to it from elsewhere. Keep the
   SKILL.md body lean: if a paragraph explains a mechanism, it is in the
   wrong file.
4. **Write for a smart reader**: explain why a rule exists rather than
   capitalising it. A rule that is only a MUST gets skipped under pressure;
   a rule with its reason gets applied to the case you did not foresee.
5. **Update the evals.** `evals/evals.json` holds the prompts and the
   assertions; a behaviour worth a rule is worth an assertion, phrased so a
   grader can check it in a transcript. Assertions must survive the
   reader's identity: a step that depends on a tool the tester cannot use
   (organisation search under some accounts) is not assessable and is not
   asserted.
6. **Test through the loop.** The recommended workflow is Anthropic's
   `skill-creator` plugin (`/skill-creator:skill-creator`, official
   marketplace): it runs the eval prompts with and without the change,
   grades them, and shows the outputs side by side. Run the prompts against
   the deployed LFX MCP server, one at a time, as a user would phrase them
   (never "use the skill"), and read the transcripts, not only the final
   answers: which tools ran, in what order, what the `applied` block said,
   whether the wording kept the qualifiers. A pass rate is not the
   deliverable; the tools being right and the figures being right are.
7. **Validate and scan.** `claude plugin validate .` must pass (a warning
   about the missing version is expected), the two scans above must be
   empty, and every markdown file carries the two license comment lines
   directly below the frontmatter, never inside it (CI checks headers on
   every PR).

## Testing against real clients

Claude Code loads the plugin from a local checkout
(`/plugin marketplace add /path/to/checkout`, then
`/plugin install lfx-mcp-playbooks@lfx-mcp`). Claude Desktop (Cowork)
installs from the GitHub marketplace and re-pulls with **Update**, or from
an uploaded zip whose root holds `.claude-plugin/` and `skills/`; it does
not read a local checkout. Whichever client, confirm in the transcript that
the skill actually loaded (a `Skill` step naming
`lfx-mcp-playbooks:<skill>`) before reading the run as evidence.

## Committing and shipping

- Every commit is GPG-signed and signed off: `git commit -S -s`. The DCO
  check enforces the sign-off; the repository expects the signature.
- Subject line: the Jira key first when the work has one
  (`[LFXV2-2891] What changed, in the reader's words`), then a body that
  says what the change makes the agent do differently and what evidence
  it rests on.
- Small, single-purpose commits; a mechanism and the wording that carries
  it travel together.
- Changes reach `main` by pull request; the header check and DCO must be
  green. There are no tags and no version bumps: merging to `main` is the
  release, and clients pick it up with a marketplace update.
