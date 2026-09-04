---
name: lfx-data-querying
description: Answers a quantitative question about Linux Foundation projects, members, contributors, events, training, maintainers, health or social listening through the LFX MCP tools — lane choice, name and value discovery, and an answer with its provenance. Use whenever a question asks for a count, a share, a ranking or a series from LFX data.
---
<!-- Copyright The Linux Foundation and each contributor to LFX. -->
<!-- SPDX-License-Identifier: MIT -->

# Querying LFX data

Read the guidance once per session before the first call:
`read_lfx_standard_metrics_guidance` for the standard metrics,
`read_lfx_semantic_layer_guidance` for the semantic layer and the SQL
assistant. They own every parameter, grouping, switch, default, literal and
worked call. This playbook says which lane, in which order, for which job,
with what discipline and provenance. Answer from fresh calls only.

## 1. The lanes

**Standard metrics** — `query_lfx_standard_metrics`. Governed recipes with
a fixed definition; the caller chooses only grouping, scope and dates, so a
re-run gives the same figure. First choice for any count, revenue, share or
series in a family the guidance lists: memberships and their movements,
contributors and contributions, maintainers, health and software value,
events, training, social listening. The only lane that reaches a project's
whole tree and a company's subsidiaries at any depth. Every answer carries
an `applied` block saying what ran, and a `truncated` flag. Guidance:
"Inventory", "The contract".

**Semantic layer** — `explore_lfx_semantic_layer`, then
`query_lfx_semantic_layer`. Named metrics and dimensions over the same
warehouse, for a grouping, filter or slice the families do not offer.
Explore discovers names and stored values; query runs them. Reaches one hop
on organisations and one level below a foundation on projects; a whole tree
is a standard-metrics question. Answers are labelled ad hoc. Guidance:
"Protocol", "Scope".

**SQL assistant** — `query_lfx_lens`. Generated SQL over the warehouse, for
cross-domain joins and hierarchy shapes no standard metric expresses.
Answers are labelled as generated SQL. Every answer opens with a **scope**
line (LF-wide when no project scope was set) and, when SQL ran, closes with
a **snapshot** block: tables read, refresh times, pipeline run. Never for
social listening or people rankings — those are standard metrics. Guidance:
"Routing".

**Service tools** — names, records, governance, meetings. `search_projects`
resolves project slugs, `search_b2b_orgs` organisation legal names.
Governance rosters: `search_committees`, `search_committee_members`,
`get_committee`, `get_committee_member`. Meetings: `search_meetings`,
`search_past_meetings`, `search_past_meeting_participants`,
`search_meeting_registrants`, `search_past_meeting_summaries`,
`get_meeting`, `get_past_meeting`, `get_past_meeting_participant`.
Membership records: `search_members`, `get_member_membership`. Figures
counted from these are "what is visible to you": say so.

## 2. Routing

Decide in this order, and stop at the first lane that fits:

1. **Read the guidance** for the lane, once per session.
2. **Governance or meetings?** Rosters, seats, chairs, voting status:
   committee tools. Meeting lists, one meeting's details, participants:
   meeting tools. Neither goes to the layer or the assistant. One interim
   exception: aggregate meeting *metrics* (attendances over a period, by
   company or committee) are for now a semantic-layer recipe ("Worked
   recipes" in the semantic-layer guidance), labelled interim ad hoc.
3. **Does a family match?** Read "Inventory" in the standard-metrics
   guidance and match by what the family answers. Past-date and year-end
   membership counts, series by period, "top contributors", "top
   maintainers", org and project breakdowns all have one. Use it; never
   rebuild it ad hoc to sort, filter or scope.
4. **No family fits?** Explore the semantic layer for the metric and
   dimension the question needs, then query. If a family covers the same
   ground at a coarser grain, run it too and reconcile.
5. **The layer cannot express it?** The SQL assistant: concrete dates
   written into the question, the project scope list set explicitly (or
   deliberately omitted for LF-wide, and said so), the answer labelled as
   generated SQL. Zero rows or an unknown name from the layer is a
   discovery failure, not a reason to switch lanes.

## 3. Discovery

- **Resolve names first.** Project slugs from `search_projects`;
  organisation legal names from `search_b2b_orgs`. Stored spellings are not
  everyday ones. A name either tool returned this session may be reused; a
  name that has not come back from them is never passed.
- **Zero rows means a wrong literal until proven otherwise.** The semantic
  layer returns zero rows, not an error, for a real dimension with a
  nonexistent value. Check spelling and scope before reporting absence —
  "Value discovery" in the semantic-layer guidance.
- **Copy dimension names from explore output.** Qualified names carry an
  entity prefix that differs per metric. Never assemble one; never reuse
  one remembered from another session.
- **Look up a literal you have not seen** before filtering on it. Tier
  names differ per foundation; country and region spellings are the stored
  form.

## 4. Answering

### 4.1 The reader's words

The prose is for the person who asked: no field names, dimension keys,
metric names, SQL, tool or parameter names unless they ask how a figure was
made. "People with a code contribution to CNCF and its projects in the last
twelve months, bots excluded" — not a column, not a filter. Provenance goes
in the block below.

### 4.2 Scope, window, population — in prose

Every figure states, in the reader's words, the three things that define
it: **scope** ("CNCF and its subprojects", "IBM as one company including
subsidiaries", "LF-wide"), **window** ("the last twelve months to
yesterday", "as of the end of last year"), **population** ("people with a
code contribution, bots excluded"; "accepted registrations"; "list-price
membership value, not dues billed"). A default that was applied is stated
as if chosen. Where a region grouping is used, say the LF region grouping
is provisional pending stakeholder sign-off.

### 4.3 The provenance block

After the answer, one block per figure: **lane** and family or metric;
**scope** as applied (the name, and whether it covered the tree or the
subsidiaries); **window** as concrete dates or an as-of date;
**population** (the definition sentence the tool returned); **defaults and
coverage** (what the tool chose for you; unattributed rows, distinct counts,
partial last period, future-dated end); **snapshot** when the lane provides
one (the SQL assistant's block; the semantic layer's compiled SQL on request
only); **label** — governed, ad hoc, generated SQL, visible to you, or
interim.

### 4.4 When the tool pushes back

- **`truncated` is true**: the answer is "the top N", never "all". Say so
  or re-run with a larger row cap.
- **An unknown slug is rejected** (with candidates): pick one or go back to
  `search_projects`. Never present a candidate as the asker's choice; never
  retry the everyday name.
- **An organisation is rejected** (no data-bearing account matches): pick
  the parent legal name among the candidates or go back to
  `search_b2b_orgs`. Never sum stray same-company accounts into a parent.
- **An empty result**: say what it means — a wrong literal, an attachment
  level (memberships attach at foundation level, so a leaf project's own
  are legitimately empty), or genuine absence — and which you verified.
  Never fill in.

## 5. The gotchas that survive

One line each; symptom, cause, check and the guidance section in
[references/gotchas.md](references/gotchas.md).

1. Unresolved names return zero rows or a rejection; resolve first.
2. Qualified dimension names are entity-prefixed per metric; copy, never
   assemble.
3. Two organisation vocabularies (CRM legal name; enrichment spelling)
   never mix in one answer.
4. Bots are excluded by default in contributor and activity figures (the
   LFX Insights convention); say so once.
5. Organisation shares are computed on the org-attributed base; the
   unattributed share is stated once, separately.
6. Headcount for "how many people", volume for "share of work"; distinct
   counts never sum across rows.
7. Health and software value are daily snapshots; the family pins the
   latest, an unfiltered aggregate does not.
8. A foundation's slug on the plain project column matches only its
   catch-all bucket; scope a foundation with the foundation dimension.
9. The unattributed row is never an organisation, never folded into a
   parent; a descending sort puts it first — re-sort before a top-N.
10. Memberships of a JDF series sit on its `-fund` sibling slug; ask for
    both.
11. Governance rosters come from the committee tools, never inferred.
12. Meeting figures come from the meeting tools and are "visible to you";
    aggregate meeting metrics are an interim layer recipe, labelled.
13. Membership count and revenue are different grains: side by side, never
    a ratio.
14. Year-to-date counts bound at today; installs can be future-dated.

## 6. Before reporting any number

- Every literal came from this session's output.
- Zero rows: spelling and scope checked before "none".
- Magnitude cross-framed against a second reading (one scope level up, a
  related figure it must sit inside).
- The unattributed row is not an organisation.
- Lane, scope, window, population in the reader's words; provenance block
  present; `truncated`, defaults and coverage read from the `applied`
  block, not from the request you think you sent.
- Re-run rather than remember.
