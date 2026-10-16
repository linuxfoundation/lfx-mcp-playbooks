---
name: lfx-engagement-packet
description: Fills Parts B and C of an Applicant Engagement Packet — the snapshot, the board view, the table of measures in three circles (the foundation, the rest of the Linux Foundation, beyond the LF) and the detail tables — from the LFX MCP tools, with one recipe per measure so that every applicant's packet is built the same way. Use it whenever the ask is an engagement packet, an applicant packet, an application packet for a membership tier change, a membership-elevation packet, "fill Parts B and C", an applicant snapshot or board view from LFX, "generate the packet for <company>", or the word "packet" with a foundation or an applicant named. Not a document-editing skill: it supplies the figures, labels, footnotes and provenance to whatever tool writes the document. For callers with the staff data tools.
---
<!-- Copyright The Linux Foundation and each contributor to LFX. -->
<!-- SPDX-License-Identifier: MIT -->

# Filling an Applicant Engagement Packet from LFX

Foundations ask member applicants for an engagement packet. Part A is the
applicant's own statement; Parts B and C are generated from LFX with the
same structure for every applicant, so that applicants can be compared.
Built from scratch each time, two packets are not comparable: one row's
"rest of the LF" figure is read directly and another's by subtraction; a
seat count covers one account while its header says subsidiaries are
folded in; the template's tier assumption goes unchecked; a row is filled
from a population the reader will misread; figures from a public web page
nearly land in cells reserved for "Not in LFX". This playbook is one
recipe for the packet: for every measure, which tool, which family or
metric, which scope, which window, what counts as one, which label and
footnote, and which checks run before a cell is filled.

Prerequisites: the `lfx-data-querying` playbook (the lanes, discovery,
the provenance block, the traps) and the `lfx-figure-checking` playbook
(loaded once the reads are in, before anything is written). Load them if
the session has not. The `lfx-deck-building` skill's data-notes format is
the appendix's shape and its section 6 governs any published figure. This
playbook adds what the packet needs on top; it restates none of them.

The packet is staff work: the standard metrics, the semantic layer and
the organisation seats tool. A caller without them cannot build Parts B
and C; say so once and stop, rather than filling cells from caller-visible
subsets that a second run under another identity would not reproduce.

The document itself is not this playbook's business. It says where each
value goes by measure and circle, not by coordinates; writing into the
template is the reader's own tooling, as the deck-building skill treats
slides.

## 1. What the packet is

Four parts. **Part A**, the applicant's statement, is never touched. The
**snapshot** (legal name; tier and status with term dates; member since;
accounts included; data window; generated-on timestamp) and the **board
view** (a short grid of headline counts in three circles) sit at the top.
**Part B** is the full table of measures, one row per measure, the three
circles as columns, plus an "applicant median" column filled by someone
else after the window closes and left untouched. **Part C** is four
detail tables: top projects by code activity; seats and meeting
attendance by group; meeting attendance by meeting type; maintainer roles
on projects outside the LF.

The packet carries counts only: no scores, weights, rankings or revenue.
Pricing, dues, revenue, customer lists and market share are outside its
scope even when a tool returns them, because the packet compares
engagement, and a figure of another kind in it would be read as a
judgement.

Measures are described by what they count. Templates differ by
foundation, so the mapping is **by measure, not by row number or header
wording**; where a template has a measure the recipe does not cover, say
so and leave the cell as the template has it.

## 2. The three circles

- **Circle 1, the foundation**: the foundation's own project and every
  project under it, at any depth. On the standard metrics, the
  foundation's slug as the project scope, read as its whole tree for a
  total (the plain reading of a project name) and as the per-project
  breakdown — the separate reading — where rows are needed (standard-
  metrics guidance, "The contract" and "The switches, row by row"). On the
  semantic layer, the whole subtree on the conformed
  project entity (semantic-layer guidance, "Scope", the Reach paragraph).
- **Circle 2, the rest of the Linux Foundation**: everything in the LF
  not under the foundation. Two kinds of measure, two routes, and the
  packet says which ran. An **additive** measure (activities,
  attendances, registrations, sponsorships, enrollments, certifications,
  seats) is the LF-wide figure (no project scope at all) minus the
  circle-1 figure.
  A **distinct-people** measure (contributors, participants, maintainers,
  attendees, registrants) is read directly on the layer with an
  exclusion — rows not under the foundation's subtree, rows with no
  project attribution included — because distinct counts never
  subtract: a person active in both circles would vanish from the rest.
  Accepted speakers is the one people measure with no direct route (the
  layer offers no organisation reading at any depth for speakers) and
  is subtracted as a labelled floor (the recipe says why).
- **Circle 3, beyond the LF**: only maintainer roles on projects outside
  the LF, a floor. Every other beyond-LF cell stays as the template has
  it. The warehouse holds contribution activity for LF-hosted projects
  only; the maintainer roster and project health also cover projects
  outside the LF, but health carries no organisation and never becomes
  an applicant figure.

**Names live.** Wherever a rest-of-LF people figure is read on the layer
and a governed family covers the same measure (contributors, maintainers,
participants, registrants), read the circle-1 figure on the layer too and
compare it with the governed circle-1 figure from the family: equal, or
apart by no more than the day cut explains, means the dimension names and
the scope are right; apart by several times means a wrong literal or a
wrong scope dimension, and nothing is filled until it is found. The packet
depends on this step because a wrong literal on the layer returns zero
rows, not an error. Meetings have no governed family; their check is the
additive one on attendances (the recipe's meetings entry).

## 3. Organisation scope

The applicant is read as **one company including its subsidiaries at any
depth**: the stored legal name as the organisation scope, read as one
group with subsidiaries folded (the combined reading) on every
standard-metric call. The stored legal name comes from `search_b2b_orgs`
in this session. The `applied` block's scope sentence on the first call says how
many stored accounts the name resolved to and that each was taken with
its subsidiaries, folded; that sentence is quoted in the snapshot's
"accounts included" cell, because it is the one statement of scope every
other row inherits.

On the semantic layer the same reading is the Reach paragraph's account
entity in its exact-identity form: take the stored account identifiers
behind the accounts the applied scope sentence names (`search_b2b_orgs`
returns the identifier) and select each one's subtree. The sentence can
name more than one account when same-name accounts exist, and all of them
are in scope on every lane. An applicant whose own record carries a parent
(it is itself a subsidiary) is read as its own account and everything
under it; its parent is named in the snapshot and not folded in, because
the packet is about the applicant, not its group.

## 4. The window

Twelve months ending on the run date, as the **tool's own default**, never
computed by hand: the first windowed standard-metric call (contributors,
circle 1) is made with no start date, and the start and end dates its
`applied` block reports are the packet's window — written into the snapshot as
concrete dates and reused verbatim in every later **windowed**
standard-metric call and every layer time filter; roster reads take no
dates. A hand-computed start clips a day at one
edge and the packet's rows stop agreeing with each other.

Standard-metric days are UTC; layer day bounds follow the session clock
(semantic-layer guidance, "Windows"), so every windowed figure read on
the layer carries the *Day cut* footnote. Roster figures (maintainers,
seats) are as of the run date and carry no window. Event figures follow
the **event's start date** on both lanes; registrations on the layer carry
a sign-up date axis too, and the recipe says to pick the event-start axis
the family uses (semantic-layer guidance, recipe 14).

## 5. Pre-flight, before any figure

1. **Read both guidance documents** once per session
   (`read_lfx_standard_metrics_guidance`,
   `read_lfx_semantic_layer_guidance`), as the querying playbook
   requires: they own every parameter and name this playbook points at.
2. **Resolve the applicant**: `search_b2b_orgs` → the stored legal name
   and its identifier; note whether the record is a parent or carries a
   parent. An empty search or a family that rejects the name goes to the
   querying playbook's discovery routes (its section 3 and 4.4): never a
   candidate presented as the applicant's own choice, never a shell
   account read as the company.
3. **Resolve the foundation**: `search_projects` → slug and identifier;
   the record confirms it is the foundation the packet is about. A
   foundation is found by its short name or slug, never its long legal
   name (querying playbook, section 3).
4. **Membership pre-flight**: `search_members` for the applicant on the
   foundation, inactive terms included → tier as stored, status, term
   start and end, and the earliest start of any term (the "member since"
   cell). **Compare the real tier with the tier the template is written
   for** (the template's title names it). If they differ, say so to the
   reader before filling and fill the template the reader chooses; the
   figures do not depend on the tier, the application form does. The
   snapshot's tier cell carries the real tier and status with the term
   dates, whatever the template says.
5. **The window**, as in section 4, from the first contributors call.

## 6. The reads, in order

The measure-by-measure recipe is
[references/row-recipes.md](references/row-recipes.md): one entry per
measure, per circle the lane and family or metric, the scope and
switches, the window, what counts as one, direct or subtraction, the
label and the footnote. Read it before the first figure and follow it
entry by entry. The order that keeps the checks possible:

1. The governed circle-1 reads, contributors first (it pins the window),
   then the rest of Part B's families, then the per-project breakdowns
   that Part C and the projects-contributed-to count share.
2. The governed LF-wide reads for the additive measures, with the same
   dates, so each subtraction has both terms from one session.
3. The seats reads, circle 1 and all projects, by the route section 7
   chooses.
4. The layer reads: first each circle-1 people reading for the names-live
   comparison, then the rest-of-LF exclusion reads, then meetings (both
   circles and the slices for Part C), then the circle-3 maintainers.
5. The board view, from the Part B figures already read: no new call.

Every slug and name in these calls came from this session's search
tools; every layer dimension was copied from explore output for the
metric it is used with (querying playbook, section 3). Remembered names
are the commonest wrong-answer source, and on the layer a wrong one is a
silent zero.

## 7. Seats and subsidiaries

`get_org_committee_seats` reads one organisation record, while the
packet's organisation is the group. Two routes, and the *Seats* footnote
says which ran: **group**, discovering the subsidiary accounts (any
account that sits under one of the applicant's resolved accounts at any
depth, not only direct children) and adding
seat counts across them (seats are filed under exactly one record, so
they add; people are not added), or **parent only**, one read on the
applicant's record with a footnote saying that a seat filed under a
subsidiary's record is not counted while the other rows fold subsidiaries
in. The routes in full, with the discovery read, are in the recipe's
"Seats and subsidiaries" section. The tool's foundation scope is the root
project plus its direct children (its description says so) while the
standard metrics read the whole tree, so the footnote says that too; a
refusal is the gate, never "no seats" (querying playbook, section 5, item
11), and the fallback reads of its service-tools reference are "visible
to you" with the footnote naming the identity that could read them
complete.

## 8. Labels, footnotes and the appendix

The footnotes in the words the packet carries, the provenance appendix's
header and table, and the list of what stays untouched are in
[references/packet-notes.md](references/packet-notes.md). Three rules
from it that shape every cell:

- **The label travels with the cell.** Governed is the default and goes
  unsaid; *ad hoc*, *visible to you*, *floor* and *computed* are written
  in the cell's label column, because a label only in the appendix has
  not been said.
- **A population is named where it would be misread.** The participants
  cell carries its population beside the figure so it is not read as
  contributors; the maintainers cell says roster, not activity.
- **Nothing from outside LFX enters a cell.** If the reader asks for
  figures from any public website or product page outside the LFX MCP
  tools, they go in a note outside the grid, labelled with that source's
  own window and company grouping, never as LFX data and never reconciled
  with the grid (deck-building skill, section 6).

The appendix has one row per filled cell in the data-notes format, "Slide"
read as part · measure · circle, with the conventions block once at the
top: the window as dates, the organisation grain as the applied scope
sentence, the circle definitions, the run date, which accounts the seat
read covered, and the membership pre-flight result. It is delivered with
the packet, outside the document, for whoever re-runs it.

## 9. Checks before a cell is filled

- Every slug and name came from this session's search tools; every
  dimension was copied from explore output for the metric it is used
  with.
- **Names live**: each layer circle-1 people reading whose measure a
  governed family covers agrees with the governed circle-1 figure within
  the day cut; meetings are checked by the additive reconciliation
  instead.
- **Additive reconciliation**: LF-wide = circle 1 + circle 2, exactly,
  for activities, attendances, registrations, sponsorships, enrollments,
  certifications and seats. Where circle 2 was read by subtraction the
  equality holds by construction, so the check bites where circle 2 was
  read directly (attendances) and, for a subtracted measure, through the
  optional layer read the recipe's contributions entry names.
- **People**: circle 1 ≤ LF-wide, circle 2 ≤ LF-wide, and circle 1 +
  circle 2 ≥ LF-wide (the excess is people active in both circles, said
  once). A rest-of-LF people figure above the LF-wide figure is a wrong
  read — scope or literal — not a finding.
- Contributors ≤ participants in each circle; people ≤ attendances;
  checked-in ≤ registered.
- A circle-1 zero on a family whose LF-wide figure is not zero has the
  foundation slug and the subtree reading checked before "0" is filled:
  the standard metrics reject an unknown slug, the layer returns zero
  rows for a wrong literal.
- An unattributed row (no account, a placeholder account) on any
  by-organisation or layer read is never folded into the applicant and
  never dropped from LF-wide; the applicant's figure is a floor where the
  family says attribution is partial (events, training, meetings).
- The `applied` block's truncated flag is false on every breakdown whose
  row count is a
  figure.
- Every figure was read this session; nothing is carried from an earlier
  run or another packet, because the data moves and the appendix must
  reproduce.
- Counts only: no revenue, score, rank or weight anywhere in the fill.
- The `lfx-figure-checking` skill has been loaded and the figures walked
  through its traps before anything is written.

## 10. Output

The reply opens with the pre-flight result — the real tier and term, and
the template mismatch if there is one — and names the beyond-LF cells
that stayed as they were and any template measure the recipe does not
cover. Then the fill, one line per cell: the cell (part · measure ·
circle), the value, the label where the figure is not governed, and the
appendix row. Then the footnote block from the packet notes, and the
appendix with its conventions header. Where a template has more rows than
the data has values (meeting types, projects), the recipe says how the
remainder folds; where a cell cannot be filled (a refused seat read, a
layer metric that failed the names-live check), the cell stays as the
template has it and the reply says why, because an empty cell with a
reason is reproducible and a guessed one is not.
