---
name: lfx-data-querying
description: Answers a question about Linux Foundation projects, members, contributors, events, training, maintainers, health, social listening, governance rosters, meetings or mailing lists through the LFX MCP tools — which tool for which kind of question, name and value discovery, why two tools give two figures, and an answer with its provenance. Use whenever a question asks for a count, a share, a ranking, a series, a roster or a record from LFX data.
---
<!-- Copyright The Linux Foundation and each contributor to LFX. -->
<!-- SPDX-License-Identifier: MIT -->

# Querying LFX data

Read the guidance once per session before the first call:
`read_lfx_standard_metrics_guidance` for the standard metrics,
`read_lfx_semantic_layer_guidance` for the semantic layer and the SQL
assistant. They and the tool descriptions own the mechanics of a call:
every parameter, grouping, switch, default, literal, error and worked
call. This playbook owns the work: which tool answers which kind of
question, in what order, how the same figure differs across tools and why,
and how an answer is worded and sourced. It never restates a parameter.
Answer from fresh calls only.

## 1. The tools, by the job they do

**Standard metrics** — `query_lfx_standard_metrics`. Governed recipes with
a fixed definition; the caller chooses only grouping, scope and dates, so a
re-run gives the same figure. First choice for any count, revenue, share or
series in a family the guidance lists: memberships and their movements,
contributors and contributions, maintainers, health and software value,
events, training, social listening. The governed lane that reaches a
project's whole tree and a company's subsidiaries at any depth. Every answer
carries an `applied` block saying what ran, with a `truncated` flag, and the
compiled SQL for anyone who asks how a figure was made. Guidance:
"Inventory", "The contract".

**Semantic layer** — `explore_lfx_semantic_layer`, then
`query_lfx_semantic_layer`. Named metrics and dimensions over the same
warehouse, for a grouping, filter or slice the families do not offer (a
consortium, a meeting type, a direct-children list, a dimension a family
has no switch for). Explore discovers names and stored values; query runs
them. Reaches one hop on organisations and one level below a foundation on
projects; a whole tree is a standard-metrics question. Answers are labelled
ad hoc. Guidance: "Protocol", "Scope".

**SQL assistant** — `query_lfx_lens`. Generated SQL over the warehouse, for
cross-domain joins and hierarchy shapes no standard metric expresses.
Answers are labelled as generated SQL. Every answer opens with a **scope**
line (LF-wide when no project scope was set) and carries the SQL it ran.
Unknown slugs are rejected before any query runs. Never for social
listening, people rankings or membership counts on any date — those are
standard metrics. This is the fallback lane, for the shapes and domains
the families and the layer do not cover yet: it interprets everyday
words on its own (see the plain-words reference), so it is the last lane
tried, and an answer that needed it says so in its provenance ("no
governed reading for this shape today"). Guidance: "Routing".

**Service tools** — records and actions, never figures. Names:
`search_projects`, `get_project`, `search_b2b_orgs`. Membership records:
`search_members`, `get_member_membership`, the key-contact tools. Rosters:
`search_committees`, `search_committee_members`, `get_committee`,
`get_committee_member`. Meetings: `search_meetings`, `search_past_meetings`,
`search_past_meeting_participants`, `search_meeting_registrants`,
`search_past_meeting_summaries`, `get_meeting`, `get_past_meeting`,
`get_past_meeting_participant`, `get_past_meeting_summary`. Lists:
`search_mailing_lists`, `search_mailing_list_members`, `get_mailing_list`.
Discord and email tools: actions on an explicit ask only. Anything counted
from these is "what is visible to you": say so. The craft for each group:
[references/service-tools.md](references/service-tools.md).

## 2. Which tool for which question

| The question asks for | Tool | Why this one | Label |
|---|---|---|---|
| A count, value, share, ranking or series in a family the inventory lists (members, dues, new and churned memberships, contributors, contributions, participants, maintainers, health, software value, registrations, sponsorships, speakers, training, certifications, social mentions and reach) | standard metrics | fixed definition, whole tree and all subsidiaries, `applied` block, repeatable | governed |
| A company's figure "including subsidiaries", or a foundation's "and its projects" | standard metrics | the only lane that walks either hierarchy to any depth | governed |
| A slice the families have no switch for (consortium, meeting type, direct children, a dimension seen in explore) | semantic layer | named metric and dimension, stored values discoverable | ad hoc |
| A cross-domain join or a hierarchy shape no metric expresses | SQL assistant | generated SQL, with its scope line and SQL returned | generated SQL |
| A project's slug, record, parent, legal entity | `search_projects`, `get_project` | the record is the truth about what a slug is | — |
| A company's legal name and identifier | `search_b2b_orgs` | the stored name every organisation-scoped call takes | — |
| What one company holds: memberships, tiers, dates, contacts | `search_members`, `get_member_membership` | the record view of the CRM, the story behind the figure | visible to you |
| Who sits on a board or committee, with what vote | committee tools | rosters live nowhere else | visible to you |
| Which meetings a project or committee held, who was invited, who attended, what was discussed | meeting tools | occurrence records with participants and summaries | visible to you |
| Attendances over a period, by company or committee | semantic layer, interim recipe | the meeting tools list, they do not aggregate | interim |
| How many meetings, and how many hours they ran | SQL assistant | distinct occurrences and stored scheduled duration live on the attendance data, which the recipe does not expose | generated SQL |
| A mailing list and its subscriber count | mailing-list tools | list-service records | visible to you |
| A role check or assignment, an email | Discord and email tools | actions, on an explicit ask, confirmed first | — |

Decide in this order; stop at the first row that fits:

1. **Read the guidance** for the lane, once per session.
2. **A record or a roster?** Names, membership records, seats, meetings,
   lists: the service tools. Neither the layer nor the assistant holds a
   roster or a meeting.
3. **Does a family match?** Read "Inventory" in the standard-metrics
   guidance and match by what the family answers. Past-date and year-end
   membership counts, series by period, "top contributors", "top
   maintainers", org and project breakdowns all have one. Use it; never
   rebuild it ad hoc to sort, filter or scope. "Top contributors" is a
   people ranking the family gives by identity: run it and present it
   where naming individuals is appropriate.
4. **No family fits?** Explore the semantic layer for the metric and
   dimension the question needs, then query. If a family covers the same
   ground at a coarser grain, run it too and reconcile
   ([references/why-figures-differ.md](references/why-figures-differ.md)).
5. **The layer cannot express it?** The SQL assistant: concrete dates
   written into the question, the project scope list set explicitly (or
   deliberately omitted for LF-wide, and said so), the answer labelled as
   generated SQL. A question with no period is asked as all time, never
   with a window of your own; the answer opens with the scope line the tool
   returned. Zero rows or an unknown name from the layer is a discovery
   failure, not a reason to switch lanes.

## 3. Discovery

- **Resolve names first.** Project slugs from `search_projects`,
  organisation legal names from `search_b2b_orgs`; stored spellings are
  not everyday ones. A name either tool returned this session may be
  reused; one that has not come back from them is never passed. A
  foundation is found by its short name or slug, not its long legal name;
  the record confirms which it is.
- **The Linux Foundation as a whole is no project at all.** `search_projects`
  returns a slug for the foundation's own name, and that slug is one bucket
  of hosted projects, never the umbrella; an LF-wide question leaves the
  project unset on every lane. Passing the bucket understates LF-wide
  figures several times over with no error — "The contract" in the
  standard-metrics guidance, "Scope" in the semantic-layer guidance.
- **Two axes, and they differ: the project tree and the membership
  programme.** On the tree, the umbrella foundation is the root: the major
  foundations (CNCF, PyTorch Foundation, OpenSSF, LF Networking, LF AI &
  Data, LF Decentralized Trust, LF Edge, LF Energy, CDF, OpenInfra, Open
  Mainframe, ASWF, FINOS, GraphQL Foundation and their peers) are its
  children, and product projects (Kubernetes, Envoy, Prometheus,
  Hyperledger Fabric, Besu, ONAP, EdgeX, Zowe and the rest) sit under their
  foundation — confirmed with `search_projects` and `get_project`, never
  from memory. On memberships, a foundation's slug is that foundation's
  own membership programme, one slug: a child foundation's memberships
  carry the child's slug and are neither included in nor "excluded" from
  the parent's reading; there is no subtree scope on memberships, and
  LF-wide is no project filter. So the prose never says "CNCF is not part
  of the LF" (wrong on the tree) and never says "memberships in projects
  under the LF" or attaches a child-project count to a membership figure
  (wrong on the membership axis). Which axis a figure sits on is said in
  the reader's words. Every scope axis — project, switches, organisation,
  time, population, geography, ranking, the assistant's scope line — has a
  row in [references/axes.md](references/axes.md): what it selects, what
  it does not, and the sentence never to write.
- **Zero for a company that plainly has data is a wrong name.** An
  everyday name can match a shell account that carries almost nothing and
  passes the guard; the family then returns zero without complaint. Back
  to the legal name.
- **Zero rows means a wrong literal until proven otherwise.** The layer
  returns zero rows, not an error, for a real dimension with a nonexistent
  value. Check spelling and scope before reporting absence — "Value
  discovery" in the semantic-layer guidance.
- **Copy dimension names from explore output.** Qualified names carry an
  entity prefix that differs per metric; never assemble one, never reuse
  one remembered from another session.
- **Look up a literal you have not seen** before filtering on it; tier
  names differ per foundation, country and region spellings are the stored
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
subsidiaries", "LF-wide"), **window** ("the twelve months to today", "as
of the end of last year"), **population** ("people with a
code contribution, bots excluded"; "accepted registrations"; "list-price
membership value, not dues billed"). A default that was applied is stated
as if chosen. A region grouping is said to be provisional pending
stakeholder sign-off.

Three habits the reader never sees but the figure depends on:

- **A relative window is the family's default or a bare period series**,
  never a start date computed by hand. "The last five years" is a series
  by year; the table quotes each year from its own row, marks the current
  year as to-date, and says which years it shows.
- **A parent total comes from the combined reading**, never from adding
  account rows: a ranking's cut hides the subsidiaries a hand-sum would
  miss, and distinct counts do not add at all.
- **"How many developers took part" is participants** (code or
  collaboration); contributors (code only) is the narrower alternative,
  named as such, never the silent default.

### 4.3 The provenance block

After the answer, one block per figure: **lane** and family or metric;
**scope** as applied (the name, and whether it covered the tree or the
subsidiaries); **window** as concrete dates or an as-of date;
**population** (the definition sentence the tool returned); **defaults and
coverage** (what the tool chose for you; unattributed rows, distinct counts,
partial last period, future-dated end); **SQL** produced on request only
(every query lane returns it) — say it was kept only if you kept it;
**label** —
governed, ad hoc, generated SQL, visible to you, or interim. No lane stamps
a data refresh time today: the run date stands for freshness.

### 4.4 When the tool pushes back

- **`truncated` is true**: the answer is "the top N", never "all". Say so
  or re-run for the full set.
- **An unknown slug is rejected** (with candidates — "Errors" in the
  standard-metrics guidance): pick one or go back to `search_projects`.
  Never present a candidate as the asker's choice; never retry the everyday
  name.
- **An organisation is rejected** (no data-bearing account matches): pick
  the parent legal name among the candidates or go back to
  `search_b2b_orgs`. A candidate that itself carries nothing is not a
  choice. Never sum stray same-company accounts into a parent.
- **An empty result**: say what it means — a wrong literal, an attachment
  level (memberships attach at foundation level, so a leaf project's own
  are legitimately empty), or genuine absence — and which you verified.
  Never fill in.

### 4.5 Two readings, one answer

When two tools give two figures for what sounds like one question, both
are usually right about different populations. Name the two populations,
find the mechanism in
[references/why-figures-differ.md](references/why-figures-differ.md),
choose the reading the question wants, and say why in a sentence. The
governed reading wins for a headline. A difference no mechanism explains
is a discovery failure, not a disagreement between sources; "sources
differ" never goes in an answer. Where the applied block and a guidance
sentence disagree on a definition, the applied block ran.

### 4.6 The everyday word and its default reading

"Organisations", "members", "developers", "projects", "revenue",
"attendees", "last year" each have two or more readings on these tools.
Answer with the default reading, name it in a clause, and offer the
alternative in one sentence that says what the difference is — never the
larger number by preference, never two readings as a contradiction.
Organisations are legal organisations known to the CRM unless the reader
asks for the broader inferred-employer view; members are memberships
unless the reader asks for distinct organisations; developers who "took
part" are participants, contributors the narrower reading. The family's
`applied.definition` sentence is the default reading in the tool's words;
repeat its meaning, never a paraphrase that widens it. The list, with the
family's definition and the offer sentence for each word:
[references/plain-words.md](references/plain-words.md).

## 5. The gotchas that survive

Symptom, cause, check and guidance section for each:
[references/gotchas.md](references/gotchas.md).

1. Unresolved names return zero rows or a rejection; resolve first.
2. Qualified dimension names are entity-prefixed per metric; copy, never
   assemble.
3. Two organisation vocabularies (CRM legal name; enrichment spelling)
   never mix in one answer.
4. Bots are excluded by convention in contributor and activity figures;
   say so once.
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
10. Memberships of a JDF series sit on its `-fund` parent slug; ask for
    both.
11. Governance rosters come from the committee tools, never inferred.
12. Meeting figures come from the meeting tools and are "visible to you";
    aggregate meeting metrics are an interim layer recipe, labelled.
13. Membership count and revenue are different grains: side by side, never
    a ratio; and a membership count is not an organisation count — a reading
    the family says it does not give is reported as unavailable, never
    derived by pulling and counting rows.
14. Year-to-date counts bound at today; installs can be future-dated.

## 6. Before reporting any number

- Every literal came from this session's output; zero rows had spelling
  and scope checked before "none".
- Magnitude cross-framed against a second reading (one scope level up, a
  related figure it must sit inside); the unattributed row is not an
  organisation.
- Lane, scope, window, population in the reader's words; provenance block
  present; `truncated`, defaults and coverage read from the `applied`
  block, not from the request you think you sent.
- A second figure for the same question was reconciled by mechanism, not
  averaged.
- Every comparative aside ("would rank just behind", "the next two would
  be") was checked against the rows it describes, or left out.
- A dimension chosen because its name matched the question had its own
  description read first, and the answer says what it counts (rows, or
  people, or organisations).
- Every count from records is "visible to you" and was paginated to the
  end.
- Re-run rather than remember.
