<!-- Copyright The Linux Foundation and each contributor to LFX. -->
<!-- SPDX-License-Identifier: MIT -->

# The row recipes — one entry per measure

This is the substance of the packet: for every measure the packet carries,
which lane, which family or metric, which scope, which window, what counts
as one, how the rest of the LF is read, which label and which footnote.
The same entry runs for every applicant in every foundation, so two
packets can be laid side by side. No entry carries a figure, and no entry
spells a parameter, a switch value or a dimension name: the tool guidance
owns those, and the agent reads them there in the session (the "Boundary"
section at the end says where).

The measures are described by what they count, not by any template's row
number or header wording. Templates differ by foundation; the agent maps a
template row to the entry that counts the same thing, and where a template
has a measure no entry covers, it says so and leaves the cell as the
template has it.

## Common to every entry

**Circle 1, the foundation**, on the standard metrics: the foundation's
slug as the project scope, read as its whole tree at any depth for a total
(the plain reading of a project name; "The contract" and "The switches, row
by row" in the standard-metrics guidance), and as the per-project breakdown
— the separate reading with the project grouping — where an entry needs
rows. On the semantic layer: the whole subtree on the conformed project
entity, as the semantic-layer guidance's "Scope" section spells it in its
Reach paragraph.

**The applicant**, on the standard metrics: the stored legal name as the
organisation scope, read as one group with subsidiaries folded at any depth
(the combined reading) on every call. On the semantic layer: the account
entity's exact-identity reading from the Reach paragraph, selecting the
subtree under each stored account the `applied` block's scope sentence
named on the first call (the identifier comes from `search_b2b_orgs`). That
reading, not the top-parent one, because an applicant that is itself a
subsidiary must be read as its own account and everything under it, never
as its parent's whole group, and because a name that resolved to several
stored accounts puts all of them in scope.

**Circle 2, the rest of the LF.** For an additive measure: the LF-wide
figure (no project scope at all; "The contract") minus the circle-1 figure,
and the packet says it was computed that way (footnote *Rest of the LF,
additive measures*). For a distinct-people measure: a direct read on the
semantic layer with the **exclusion**: rows whose conformed project path is
not under the foundation's subtree, rows with no project attribution
included. On the activity model the exclusion read also keeps to the
activity's own row, so the fan-out along the project ancestry does not
repeat it; both names are in explore's dimension descriptions on the
contributors metric (the flag's description says it marks the activity's
own row; the path's description says it selects a subtree). Distinct
counts never subtract: a person active in both circles would vanish from
the rest. Accepted speakers is the one exception, subtracted as a labelled
floor because no direct read exists (its entry says why).

**Names live.** Wherever a rest-of-LF people figure is read on the layer
**and a governed family covers the same measure** (contributors,
maintainers, participants, registrants), the circle-1 figure is read on
the layer too and compared with the governed circle-1 figure from the
family: equal, or apart by no more than the day cut explains, means the
dimension names and the scope are right; apart by several times means a
wrong literal or a wrong scope dimension, and nothing is filled until it
is found. A wrong literal on the layer returns zero rows, not an error, so
this check is what the layer figures rest on. Meetings have no governed
family: their check is the additive one on attendances (the meetings
entry).

**The window.** The dates the first windowed call returned in the `applied`
block's start and end (the tool's default, never computed by hand), reused
verbatim as the start and end dates of every later **windowed**
standard-metric call and as the day bounds of every layer time filter.
Roster reads (maintainers, seats) carry no window and take no dates.
Standard-metric days are UTC; layer day bounds follow the session clock
(semantic-layer guidance, "Windows"), so every windowed layer figure
carries the footnote *Day cut*.

**Labels.** Governed for a standard-metric figure (unsaid: it is the
default); *ad hoc* for a layer figure; *visible to you* for a service-tool
figure; *floor* where the entry says so. The label is written in the cell's
label column and repeated in the appendix row (the `lfx-deck-building`
skill's data-notes format).

**Reading the tables.** Each entry has one table with the two circles as
columns and, where the measure has a third circle, a line for it. *Route*
says whether circle 2 is read directly or by subtraction. *Footnotes*
names entries of `references/packet-notes.md`.

## Part B — the measures

### Distinct code contributors

| | Circle 1 — the foundation | Circle 2 — the rest of the LF |
|---|---|---|
| Lane | standard metric `contributors`, one figure | semantic layer: the contributors metric (recipe 4: code only, bots excluded) |
| Scope | the foundation tree; the applicant group | the exclusion on the activity's own row; the applicant group through the account entity |
| Window | the packet window; this is the first windowed call, made with no start date, and the dates it applied become the window | the same dates as day bounds on the activity's time axis |
| One is | a distinct person with a code contribution, bots excluded | the same |
| Route | direct | direct, with the exclusion |
| Label | governed | ad hoc |
| Footnotes | — | *Day cut*; the *Names live* comparison against circle 1 |

### Code contribution activities

| | Circle 1 — the foundation | Circle 2 — the rest of the LF |
|---|---|---|
| Lane | standard metric `contributions`, one figure | standard metric `contributions`, one figure, LF-wide, minus circle 1 |
| Scope | the foundation tree; the applicant group | LF-wide; the applicant group |
| Window | the packet window | the packet window |
| One is | one code contribution activity, bots excluded | the same |
| Route | direct | subtraction, said |
| Label | governed | governed, computed |
| Footnotes | — | *Rest of the LF, additive measures* |

An optional check: the same exclusion read as the contributors entry, on
the code-activity metric (recipes 2 and 10 name it; not the any-activity
metric of recipe 4, a wider population), agrees with the subtracted
figure within the day cut. It is a check, never the figure.

### Active maintainers

| | Circle 1 — the foundation | Circle 2 — the rest of the LF |
|---|---|---|
| Lane | standard metric `maintainers`, one figure | semantic layer: the active-maintainers metric with the LF-project flag true (recipe 11) |
| Scope | the foundation tree; the applicant group | the exclusion on the conformed project path; the applicant group through the account entity (recipe 11 names the employer dimensions) |
| Window | none: today's roster, no dates passed | none: active means no end date (recipe 11) |
| One is | a distinct person on the roster of an LF project | the same; a person on two projects counts once |
| Route | direct | direct, with the exclusion |
| Label | governed | ad hoc |
| Footnotes | *Maintainers* | *Maintainers*; the *Names live* comparison against circle 1 |

The per-project caveat (people inherited from vendored kernel trees,
MAINTAINERS-file reviewers) is the family's and belongs to the per-project
rows of Part C, not to this total; the total is distinct people. Roster,
not activity: a maintainer with no contribution in the window still counts.
The circle-3 floor (maintainers of projects outside the LF) is its own
entry below.

### Code contributions by maintainers

Only when the template asks for it.

| | Circle 1 — the foundation | Circle 2 — the rest of the LF |
|---|---|---|
| Lane | standard metric `maintainer_contributions`, one figure: the contributions column (additive) and the contributing-maintainers column (distinct) | contributions: LF-wide `maintainer_contributions`, one figure, minus circle 1. Contributing maintainers: no route for the rest, see below |
| Scope | the foundation tree; the applicant group | LF-wide; the applicant group |
| Window | the packet window | the packet window |
| One is | a code contribution by a person on the maintainer roster of the activity's project; a distinct contributing maintainer | the same |
| Route | direct | contributions by subtraction, said; the distinct part is read LF-wide and labelled **LF-wide**, never "rest" |
| Label | governed | governed, computed (contributions); governed, LF-wide (people) |
| Footnotes | *Maintainers* (the roster the figure read) | *Rest of the LF, additive measures*; *Maintainers* |

Recipe 11 says maintainer-by-contribution figures are not in the layer,
so the distinct part has no exclusion read. Maintainership is as of the
build; the `applied` block's definition sentence says which roster this
call read and is quoted in the appendix row.

### Projects contributed to (count)

| | Circle 1 — the foundation | Circle 2 — the rest of the LF |
|---|---|---|
| Lane | standard metric `contributions`, the per-project breakdown (separate reading), every row, an order asked for | standard metric `contributions`, the per-project breakdown LF-wide, every row, an order asked for |
| Scope | the foundation tree, one row per project; the applicant group | LF-wide, one row per project; the applicant group |
| Window | the packet window | the packet window |
| One is | one project row returned, the `applied` block's truncated flag false | one LF-wide project row whose slug is not among the circle-1 rows |
| Route | direct | the LF-wide rows minus the circle's rows, matched by slug |
| Label | governed | governed, computed |
| Footnotes | — | *Rest of the LF, additive measures* |

A foundation's own bucket is a row like any other; a leaf project is one
row. The count is a row count, so the truncated flag must be false on both
reads; a cut list is a floor and says so. The same two reads feed Part C's
project table, so they are made once.

### Working group and committee seats (count and groups)

| | Circle 1 — the foundation | Circle 2 — the rest of the LF |
|---|---|---|
| Lane | `get_org_committee_seats` scoped to the foundation, the seat rows asked for | `get_org_committee_seats` with no foundation (all projects), the seat rows asked for, minus circle 1 |
| Scope | the applicant's record (or the group's records: "Seats and subsidiaries" below); the foundation as the tool scopes it — its root project plus its direct child projects | the applicant's record (or the group's); every project |
| Window | none: the roster at this read | none |
| One is | a seat: one seat row; a group: a distinct committee among the seat rows, told apart by project and committee | a seat row of the all-projects read not in the circle-1 read; a distinct committee likewise |
| Route | direct | subtraction, said |
| Label | visible to you | visible to you, computed |
| Footnotes | *Seats* | *Seats*; *Rest of the LF, additive measures* |

Seats are additive; people are not. The tool reports people (distinct
e-mails) for each read it makes, so a people figure exists for circle 1
and for the whole LF, and none for the rest: a people cell for the rest
stays empty with a dash and the footnote says why. The tool's foundation
scope is the root project plus its direct children (its description says
so), while the standard metrics read the whole tree; the footnote says it.
Under the organisation grant the result is complete for the scope; a
refusal is the gate, never "no seats" (the `lfx-data-querying` skill's
service-tools reference, Governance rosters; its section 5, item 11).

### Technical Steering Committee seats

| | Circle 1 — the foundation | Circle 2 — the rest of the LF |
|---|---|---|
| Lane | the circle-1 seats read: its summary by committee category, the technical steering category exactly as the tool spells it | the all-projects seats read, the same category, minus circle 1 |
| Scope | as the seats entry | as the seats entry |
| Window | none | none |
| One is | a seat filed under that category | the same |
| Route | direct | subtraction, said |
| Label | visible to you | visible to you, computed |
| Footnotes | *Seats* | *Seats* |

Oversight, advisory and board categories are other categories and are not
folded in; the footnote names the category that was read, spelled as the
tool stores it. No new call: the summary comes with the seats read.

### Meeting attendance (people · attendances)

| | Circle 1 — the foundation | Circle 2 — the rest of the LF |
|---|---|---|
| Lane | semantic layer: the unique-attendees metric and the attendances metric on the attendance model (recipe 12) | the same two metrics with the exclusion |
| Scope | the whole subtree on the conformed project entity; the applicant group through the account entity (recipe 12: organisations on the attendance model) | the exclusion on the conformed project path; the applicant group |
| Window | the packet window as day bounds on the model's time axis, the meeting date | the same |
| One is | people: a distinct identified attendee; attendances: one person at one occurrence | the same |
| Route | direct | direct, with the exclusion, for both; attendances are then checked: circle 1 plus rest equals the same applicant-group reading with no project scope |
| Label | ad hoc, a floor | ad hoc, a floor |
| Footnotes | *Meetings*; *Day cut* | *Meetings*; *Day cut* |

"Attendees" or "people" only for the unique-attendees figure, "attendances"
for the records, never one divided by the other (the `lfx-data-querying`
skill's section 5, item 12). No family covers meetings, so there is no
governed circle-1 figure and the names-live comparison does not apply
here; the check is the additive one on attendances, and people ≤
attendances on each circle.

### Distinct people with any activity

| | Circle 1 — the foundation | Circle 2 — the rest of the LF |
|---|---|---|
| Lane | standard metric `participants`, one figure | semantic layer: the metric that carries the participants family's population (see below) |
| Scope | the foundation tree; the applicant group | the exclusion on the activity's own row; the applicant group through the account entity |
| Window | the packet window | the same dates as day bounds |
| One is | a distinct non-bot person with any activity in the window | the same |
| Route | direct | direct, with the exclusion |
| Label | governed | ad hoc |
| Footnotes | *Participants* | *Participants*; *Day cut*; the *Names live* comparison against circle 1 |

Governed and kept, because a family serves it; the risk is misreading, so
the population is written beside the figure in the family's own words —
code, issues, reviews, comments, stars, forks, meeting invitations and
attendance, training and exams, Hacker News — and the cell is never
captioned "contributors". Contributors ≤ participants in each circle is a
check.

The semantic-layer guidance does not list a participants metric by name
today; recipe 4 names the contributor populations. The agent finds the
metric with explore's metric search on the family's own definition words,
reads its description, and proves it with the names-live comparison: a
circle-1 reading that agrees with the governed figure within the day cut
is the family's population; one that does not is a different population,
and the rest-of-LF cell then carries no figure and says so.

### Event attendees (registered · checked in)

| | Circle 1 — the foundation | Circle 2 — the rest of the LF |
|---|---|---|
| Lane | standard metric `event_registrations`, one figure: the distinct-registrants column and the checked-in column | semantic layer: the distinct-registrants and checked-in metrics with the exclusion (see below) |
| Scope | the foundation tree; the applicant group | the exclusion on the conformed project path (registrations carry the conformed project entity, recipe 14); the applicant group through the account entity (recipe 14: the account lens) |
| Window | the packet window, on the event's start date (the family's definition) | the same dates on the event-start time axis, not the sign-up date (recipe 14: the two time axes) |
| One is | a distinct person by e-mail with an accepted registration; a distinct person with check-in data | the same |
| Route | direct | direct, with the exclusion |
| Label | governed | ad hoc |
| Footnotes | *Events* | *Events*; *Day cut*; the *Names live* comparison against circle 1 |

Check-in data exists only for some registration sources, so a zero
checked-in is "no check-in data", not low attendance, and
checked-in ≤ registered is a check. Registrations attach at foundation
level, so the subtree reading is in effect the foundation's own rows; the
exclusion keeps every other foundation's rows and the unattributed ones.
The guidance names the accepted-registrations metric on the layer (recipe
14) and not the two people metrics by name: the agent finds them with
explore's metric search on the family's column words and proves them with
the names-live comparison, as for participants.

### Events sponsored (count only)

| | Circle 1 — the foundation | Circle 2 — the rest of the LF |
|---|---|---|
| Lane | standard metric `event_sponsorships`, the per-event breakdown | standard metric `event_sponsorships`, the per-event breakdown LF-wide |
| Scope | the foundation tree; the applicant group | LF-wide; the applicant group |
| Window | the packet window, on the event's start date | the packet window |
| One is | events: one event row; sponsorships: the count column summed over the rows | an LF-wide event row not among the circle-1 rows; its count column likewise |
| Route | direct | the LF-wide rows minus the circle's rows, matched by event |
| Label | governed | governed, computed |
| Footnotes | *Events* | *Events*; *Rest of the LF, additive measures* |

One event can carry several sponsorships, so the two figures differ and
both are counts. **The revenue column the tool returns is never
transcribed**: pricing, dues and revenue are outside the packet's scope
even when a tool returns them. The truncated flag false on both reads.

### Accepted speakers

| | Circle 1 — the foundation | Circle 2 — the rest of the LF |
|---|---|---|
| Lane | standard metric `speakers`, one figure | standard metric `speakers`, one figure, LF-wide, minus circle 1 |
| Scope | the foundation tree; the applicant group | LF-wide; the applicant group |
| Window | the packet window, on the event's start date | the packet window |
| One is | a distinct person with an accepted speaker status | the same |
| Route | direct | subtraction, **labelled a floor** |
| Label | governed | governed, computed, a floor |
| Footnotes | — | *Speakers, rest of the LF* |

This is the one people measure read by subtraction, because the layer
offers no organisation reading at any depth for speakers: speakers carry
no account entity (the Reach paragraph of "Scope"), and the speakers
model's own account-name slice reads one account by its stored name, not
the group, so the applicant group has no direct exclusion read. A person
who spoke in both circles is subtracted away, so the rest is a floor; it
is exact when the circle-1 figure is zero, and the footnote says so.

### Foundation certifications (certifications · enrollments)

A circle-1 measure only.

| | Circle 1 — the foundation |
|---|---|
| Lane | standard metric `certifications`, one figure, the foundation as the project scope; standard metric `training_enrollments`, the per-course breakdown, the foundation as the project scope |
| Scope | the foundation tree; the applicant group |
| Window | the packet window, by enrollment date (both families) |
| One is | a completed certification; an enrollment (the enrollments column summed over the course rows; the enrolled-users column is distinct and is not used) |
| Route | direct |
| Label | governed |
| Footnotes | *Training* |

The course rows name which certification or course each enrollment
belongs to, so the cell can say "enrollments in the foundation's
certifications" with the course names beside it. Enrollments are
additive, so the course rows sum to a one-figure read of the same family;
that is a check, not a second figure.

### Training enrollments · certifications (LF)

A circle-2 measure only.

| | Circle 2 — the rest of the LF |
|---|---|
| Lane | standard metric `training_enrollments`, one figure, LF-wide, minus the foundation's enrollments; standard metric `certifications`, one figure, LF-wide, minus the foundation's certifications |
| Scope | LF-wide; the applicant group |
| Window | the packet window, by enrollment date |
| One is | an enrollment; a completed certification |
| Route | subtraction, said |
| Label | governed, computed, a floor |
| Footnotes | *Training*; *Rest of the LF, additive measures* |

The family's definition says the edX branch carries no account, so an
organisation-scoped read sees the other platform's rows only: a floor, on
both circles, and the footnote says so.

### Maintainers of projects outside the LF (circle 3, a floor)

| | Circle 3 — beyond the LF |
|---|---|
| Lane | semantic layer: the active-maintainers metric with the LF-project flag **false** (recipe 11) |
| Scope | the applicant group through the account entity; no project scope |
| Window | none: active means no end date |
| One is | a distinct person on the roster of a non-LF project the platform tracks |
| Route | direct |
| Label | ad hoc, a floor |
| Footnotes | *Maintainers*; *Beyond the LF* |

The roster covers only the non-LF projects the platform tracks, so the
figure is a floor and never "the applicant's open-source maintainers".
The same read grouped by project and role is Part C's fourth table.

### Everything else beyond the LF

The cell stays as the template has it, and nothing is substituted. The
warehouse the data tools read holds contribution activity for LF-hosted
projects only; the maintainer roster and project health also cover
projects outside the LF, but health carries no organisation and never
becomes an applicant figure. Footnote *Beyond the LF* says so once, and
the reply names the cells that stayed.

## The board view

Every board-view cell is one of the Part B figures above: contributors;
maintainers, with the beyond-LF floor beside it; seats; meeting people;
registered attendees; events sponsored and accepted speakers;
certifications. No new read is made. The same figure appears twice in
the packet, and its appendix row says which Part B measure it is, so a
reader who checks one finds the other.

## Part C — the detail tables

### C1 — top projects by code activity

The three per-project breakdowns already made for circle 1 (the separate
reading) and LF-wide — `contributions`, `contributors`, `maintainers`,
each for the applicant group — joined by project slug. Ordered by code
activities; as many rows per circle as the template has; the "other LF"
rows are the LF-wide rows whose slug is not among the circle's. Each row
carries that project's code contributors, code activities and active
maintainers.

- Distinct counts in these rows are never summed: the circle's total is
  the one-figure read, not the column's sum.
- The per-project maintainer caveat (people inherited from vendored kernel
  trees, MAINTAINERS-file reviewers; a person on two projects counts once
  in each) is the family's note and travels with the table (the
  `lfx-data-querying` skill's section 5, item 16).
- A ranking asks for a few more rows than it shows and asks for its order
  (the `lfx-data-querying` skill's section 4.2); a row count that is a
  figure needs the truncated flag false, so the projects-contributed-to
  read is made with no limit and the table is cut client-side.

### C2 — seats and meeting attendance by group

Two sources side by side, and the caption says so: the LFX v2 committee
service for seats, the warehouse's meeting data for attendance.

- Seats: the circle-1 seat rows grouped by project and committee, with the
  voting statuses as stored.
- Attendance: the attendance model grouped by the project and the
  committee-name slice (recipe 12 names the slices), the applicant group
  through the account entity, the subtree, the window → people ·
  attendances.
- The two sides are matched on **project and committee name together**,
  never on the committee name alone: the same committee name (a technical
  steering committee, a marketing committee) recurs under several projects
  of one foundation, and a name-only match would hang another project's
  attendance on a seat row. The two systems' committee identifiers are
  not assumed to be the same identifier. A row that matches on neither
  side, or on more than one, is shown unmatched with its project and
  committee as stored, never forced into a pair.
- A group with attendance and no seat shows a dash for seats; a seat group
  with no attendance shows zero attendance; rows with no committee name
  are one "no committee" bucket per project.
- Ordered by attendances; as many rows as the template has.

### C3 — meeting attendance by meeting type

The attendance model grouped by the stored meeting-type slice (recipe 12),
circle 1, the applicant group, the window. One row per stored value, the
untyped bucket (recipe 12: a stored "none" literal and a null, both
untyped) named "no type recorded". Ordered by attendances. When there are
more stored values than the template has rows, the top rows stay and the
remainder is one row that names the stored values it folds. The
template's "as recorded in LFX" is honoured: values are copied as stored,
never renamed.

### C4 — maintainer roles on projects outside the LF

The circle-3 read grouped by the roster's project key and the role
(recipe 11 names both), ordered by maintainers, as many rows as the
template has; the project key is shown as stored. A floor, said in the
table's caption.

## Seats and subsidiaries

`get_org_committee_seats` reads one organisation record. The packet's
organisation is the group, so there are two routes, and the *Seats*
footnote says which one ran.

**Group.** Enumerate the subsidiary accounts that can be discovered: the
`contributors` family's by-organisation breakdown with the separate
reading, the applicant as the organisation scope, lists the stored
accounts under the applicant at any depth, each with its direct parent
alongside. (The `maintainers` family's by-organisation rows carry no
parent column, so they are not the discovery read.) `search_b2b_orgs` on
each name confirms the record and its parent, and the chain upward is
walked on those records. An account is in the group when
it sits **under one of the applicant's resolved accounts at any depth**:
its parent is the applicant, or its parent's parent is, and so on up the
chain the records show. Immediate-parent equality is not the test, because
a subsidiary of a subsidiary is in the packet's scope on every other row.
The applicant's own resolved accounts are in the set; accounts are
deduplicated by identifier, not by name. Then read seats per account,
scoped to the foundation for circle 1 and unscoped for the whole LF, and
add the seat counts: a seat is filed under exactly one organisation record,
so seats add. People are not added across accounts. The footnote names how
many accounts were read and that discovery covers the subsidiaries that
carry data or that the search found; an account neither surfaces is
undiscovered, and the footnote says the count is a floor for that reason.

**Parent only.** One read on the applicant's record. The footnote says
seats cover the applicant's own record while the other rows fold in
subsidiaries, so a seat filed under a subsidiary's record is not counted.

## Boundary: what these entries name, and what they do not

The tool guidance owns the mechanics of a call; this reference owns the
work. So the entries name standard-metric **families** and the service
tools, and say each read in the reader's words — one figure, the
per-project breakdown, the separate or combined reading, LF-wide, the
packet window — because the recipe must say which reading each cell takes
for two runs to match. The parameter that carries each reading, its
values and its defaults are in the standard-metrics guidance ("The
contract", "The switches, row by row"), and nothing here restates them.
The `applied` block is read as the querying playbook reads it: the scope
sentence, the definition sentence, the dates and the truncated flag that
ran.

The entries name **no qualified dimension name** of the semantic layer.
Each ad hoc read is described by what it is, and the guidance section
that spells the name is:

- the company at any depth through the account entity, and the whole
  subtree on the conformed project entity: "Scope", the Reach paragraph;
- the LF-project flag, the employer dimensions, the project key and the
  role on the maintainers model: recipe 11;
- the committee-name and meeting-type slices, the organisation reading
  and the time axis on the attendance model: recipe 12;
- the event-start time axis and the account lens on registrations:
  recipe 14;
- the own-row flag and the project path on the activity model: explore's
  dimension descriptions on the contributors metric.

The agent discovers each name on the live layer, copies it from explore
output for the metric it is used with, and the names-live check catches a
wrong one. Remembered names are the commonest wrong-answer source, and a
name pinned here would drift from the layer without anyone noticing.
