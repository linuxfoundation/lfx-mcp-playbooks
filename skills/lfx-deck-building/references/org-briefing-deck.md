<!-- Copyright The Linux Foundation and each contributor to LFX. -->
<!-- SPDX-License-Identifier: MIT -->

# The company briefing deck — a workload pattern

The other recurring executive deck: one company across the whole Linux
Foundation, for a meeting with that company's leadership. Memberships and
what they cost, where the company's engineers work and how they rank,
who sits on which board, what the company sponsored and attended, how much
of the coordination it showed up for. Org-sided, cross-foundation, exact
to the digit, and checked line by line by the people it is about. This
reference is the pattern: what each section asks, which tool and reading
answers it, the trap registered against that reading (D1–D20 data defects,
M1–M16 access problems, and the reconciliation habits from the briefing
that started this work), the check, and the label. No figures, no
parameters. Lines that need something not deployed carry
`[not yet in production: <bundle> — until then: <fallback>]`.

## Section 0 — Resolve the company, choose the scope

- **Legal name first for CRM figures.** When visible, `search_b2b_orgs`
  gives the stored legal name and identifier; the everyday name is often a stray account with nothing on
  it or a shell with a little (a few enrollments) that returns a confident
  zero for everything else. A zero for a company that plainly has data is
  a wrong name. The record vocabulary of the membership records
  (`search_members`) confirms the same identifier. When organisation
  discovery is gated, use the querying skill's readable-record discovery
  routes. Roster and participant searches take their own stored spellings,
  never a CRM name substituted for one.
- **The scope choice is the first slide's decision.** The default reading
  of a named company is the account alone. "The company including its
  subsidiaries" is the combined reading, walked to any depth by the
  standard metrics; the breakdown by subsidiary is the separate reading.
  A company whose largest subsidiary is bigger than itself (the flagship
  case) needs both readings on every slide that compares it with peers,
  because the peers' figures are read at the same grain. A company that
  is itself a subsidiary has no combined reading of its own and its parent
  is named on the conventions slide.
- **One vocabulary per slide.** Membership, dues, sponsorship, training and
  registration slides are on the CRM account (legal name, parent alongside).
  Activity slides read by organisation are on the account too (the row's
  account is resolved to the parent for that project before the parent
  column applies); the meeting tools' participant records carry the
  organisation name as stored, while the layer's attendance metrics carry
  the CRM account and its parents.
- **Window.** The trailing twelve months to the run date, as concrete
  dates, on every activity slide; the deck that started this work used a
  month-anchored thirteen-month window while saying "last twelve months"
  — the fix is the dates on the slide. "Same point last year" is the same
  day-of-year, both windows stated.

## Section 1 — Membership footprint

**Memberships held, by project and foundation, with tier.** The figure:
standard metrics, memberships by project for the company (alone, then
combined), as of today, project-account pairs. The story: `search_members`
for the company's records — tier, dates, status, project as the record
names it — "visible to you", never counted into the figure. Tier literals
differ per foundation. Trap D10: three membership grains exist; the slide
says "memberships" and, where it says "member of N foundations",
foundation-level attachment is the reason a leaf project shows none.
Label: governed (figure), visible to you (records).

**What the memberships are worth.** The same call's list-price value,
beside the count, never divided; dues billed are a finance figure the
tools do not hold. Label: governed.

**Rank among members.** Two rankings, said which: memberships by
organisation ordered by list-price value at account grain (the company's
own account against other accounts), and the same at parent grain
(combined reading, every parent resolved to the top of its chain). The
company's position is read off the rows, and the rank is "among accounts
holding at least one active membership". Never hand-sum accounts into a
parent for a rank. Label: governed.

**Since when; first membership ever.** The account's first LF membership
date is an ad hoc dimension on the semantic layer today; the membership
records give each term's dates. A "member since" claim quotes the
earliest install date and says which. Label: ad hoc / visible to you.

**Growth of the company's memberships over the years.** Memberships as an
at-date series by year for the company (date-based readings on past
dates, said so). Label: governed.

## Section 2 — Engineers and code

**Contributions by project over twelve months.** Standard metrics,
contributions for the company by project (alone; combined for the group
view), bots excluded, the window as dates. The project rows are the
company's footprint; the folded figure is the headline. Trap M13 / D1:
organisation attribution is a floor (the employer is resolved for a
minority of people), so every company figure is "at least". Label:
governed.

**Rank among companies, per project and LF-wide.** Contributions by
organisation for the project (and with no project for LF-wide), parent or
account grain held to the company's own grain; the unattributed row is not
an organisation and is dropped before the position is read; the rank is
"among organisations with a resolved employer". Label: governed.

**Contributors and participants from the company.** Standard metrics,
contributors (code) and participants (any non-bot activity, meetings and
training included) for the company, distinct people, never summed across
projects; per project as a breakdown; the two populations are named on
the slide. Label: governed.

**Top contributors from the company.** Contributions by contributor for
the company: a people ranking by identity, presented only where naming
individuals is appropriate for the audience, otherwise as a count. Label:
governed.

**Maintainers from the company, by project.** Standard metrics,
maintainers by project with the company as the organisation; LF projects
only, as of today, roster-based. The group view (subsidiaries at any
depth) is the family's subsidiaries switch, or ad hoc through the layer's
top-parent dimension on maintainers, said so. Per-project maintainer
counts include people the roster inherits from vendored Linux kernel
trees on kernel-fork projects, and MAINTAINERS-file reviewers count as
maintainers; a person maintaining two projects counts once in each. The
family names the split — by role (maintainer, reviewer) and by source
(the project's own repository, an inherited kernel tree, a seeded
roster) — and the total, organisation and project readings carry the
split columns beside the total: a slide that uses a split names it and
pairs it with the total it was cut from, since a split alone reads as
a total (on the layer a filtered split omits the groups with nothing
in them); a kernel-fork row keeps the inherited-tree caveat and, from
the excluding-inherited column beside that row's total, says how much
of the row came only with an inherited kernel tree or another seeded
roster. Label: governed / ad hoc.

**Share of a project's work.** Volume over the org-attributed base of the
same metric, scope and window; the unattributed share stated once on the
data-notes slide. Label: governed.

## Section 3 — Events, sponsorship, training

**Event registrations and attendance by the company's people.** Standard
metrics, registrations by organisation for the company (the registrant's
account): registrations, distinct people, checked-in where the source
carries it. Corporate e-mail domain matching is not a route the tools
offer and a figure built that way is not reproducible. Label: governed.

**Speakers from the company.** Standard metrics, speakers by organisation
for the company: accepted speakers whose proposal resolved to the
account, with the unresolved share stated once, since a large share of
speakers resolves to no account. Label: governed.

**Sponsorships: which events, which tier, how much.** Standard metrics,
sponsorships by organisation for the company and by event; one event can
carry several assets; tier names as stored per event. The subsidiary's
sponsorships are separate rows under the parent. Label: governed.

**Training and certification by the company's people.** Standard metrics,
enrollments and certifications by organisation for the company;
placeholder accounts for unaffiliated learners are unattributed rows,
never companies; platform data only. Label: governed.

## Section 4 — Governance

**Who represents the company at a foundation.** Two readings, never one
for the other, never merged into one name. The *contact of record* is
the membership's key contact: the person the membership record names
for a role, with the role and the status as the record stores them and
the date the record was last updated, where one is returned; a contact
record's board-member flag is the membership's own claim, not a seat.
A contact flagged active is not proof the term is active, so the slide
says "contact of record on the <status> term", the term's status from
the membership records (the `lfx-data-querying` skill's service-tools
reference, Organisations).
The *seat holder* is the person on a seat that represents the company
— the seats the `lfx-data-querying` skill's service-tools reference
defines (Which seats represent the company) — with the voting status
as the roster stores it, and its term date only where the roster records
one, never the record stamp, which dates the LFX v2 record. Empty placeholder
terms are not dates; say "no term date recorded" when absent. The organisation
seats tool's rows carry no date. The
read is the organisation seats tool's one call under the organisation
gate: the contacts of record beside the seats, each with its date as
recorded, the voting-status split, and a per-project pairing of the
voting contacts with the seats that represent the company. Under an
identity without the grant the two reads remain the way — the
key-contact tools for the contacts, the roster search for the seats —
and the notes say which ran. A company can have a voting contact who
holds no seat, and a seat holder who is not the membership's contact:
the slide shows both side by side, each labelled as what it is and
cited as recorded on its side, never as "current". Contacts and seats
are people: shown only where naming individuals is appropriate for the
audience. A refusal is the gate, never "no seats"; each fallback reading
is "visible to you", and an empty side is a visibility limit, not an
absence. Never infer the missing contact from a seat, or a seat from a
contact; never call a record stamp "member since". Label: visible to you.

**Seats the company holds, across which boards, with what vote.** Every
seat the company holds in each foundation of its footprint, on every
committee category, with voting status and role from the seat record;
which of them represent the company is the item above. The read is the
organisation seats tool: every seat with the board split, the
voting-status split and a per-project summary in one call, under the
organisation gate. For a seat count without the grant, use the count
tool for the organisation and read its complete flag, "visible to you".
To read the seats, the fallback is the committee tools: each roster read
through the roster search
filtered on the company's stored organisation name, one read per
spelling the company appears under (D15). When a roster comes back
empty, the coverage audit over its foundation is read before the empty
result is interpreted: it says per project which committees are
indexed and which have no visible member, a zero being an access
effect or a roster not yet onboarded (the `lfx-figure-checking` skill's
governance-rosters entry), and the slide's lead line names which case
the audit found, never "no seats" over a caveat (the
`lfx-data-querying` skill's section 5, item 11). Every roster in this
section is read from the committee tools; a figure read from the
warehouse side is the SQL assistant's warehouse copy of the v1 committee
records, only for an open LF-wide ranking as the staff last resort,
active seats only. The layer has no committee metric. This is a different
source: say which was read, never combine or reconcile them (the
`lfx-figure-checking` skill's "Rosters: LFX v2 vs the v1 warehouse copy"
entry). Label: visible to you for these company seat readings.

**Key contacts.** The membership records' key contacts, the
contact-of-record reading above: role and status as stored, the updated
date where one is returned — people, shown only where naming
individuals is appropriate for the audience. Label: visible to you.

## Section 5 — In the room (meetings)

**Meetings the company's people attended; attendances by month; hours.**
Attendances and people who attended, for the company: the layer's
attendances and unique-attendees metrics by the account entity — the whole
company by its top parent, subsidiaries folded in — worded "attendances"
and "people", with the unattributed share (no account, an account that
does not resolve, or a placeholder account) stated once; label ad hoc,
a floor bounded by platform onboarding. Distinct meetings the company's
people attended, and the scheduled minutes those meetings ran: the SQL
assistant over the attendance data, summed over distinct occurrences,
because no named metric counts occurrences by company; label generated SQL,
also a platform floor. The meeting tools filter participants by the exact
stored organisation name (case-sensitive, one spelling a call, no subsidiary
roll-up, a wrong spelling returns zero, not an error). With a project or
committee and a date range they give the company's people at that body's
past meetings, "visible to you"; count-only gives index records — not people
and not attendances. Distinct occurrences on all raw attended rows give
meetings attended, distinct occurrence-and-person pairs give attendances;
the listing's meeting count is meetings expanded, not meetings attended.
These are the readings for a caller without staff tools, one project or
committee at a time, never an LF-wide or company-wide period total, and
never reconciled with the layer's. State that the wider total is unavailable.

## Section 6 — Peers and comparisons

- Every peer is resolved to its legal name and read at the same grain and
  window as the company; a peer table mixes no grains.
- "Same point last year" uses the same day-of-year on both windows.
- Rank movements are read from two complete rankings, not from a
  remembered earlier deck.

## Section 7 — What the briefing cannot say from LFX today

Listed on the data-notes slide, not silently dropped: meeting attendance
by company as a governed family figure (attendances and people are ad hoc
on the layer; distinct meetings by company is generated SQL, all floors);
anything matched by corporate e-mail domain; any figure from a previous
deck that is not re-run.

## The checks a company briefing runs

- **Alone ≤ combined** on every figure that has both readings; the
  breakdown by subsidiary reconciles to the combined figure for additive
  metrics and is reported as a breakdown for distinct counts.
- **The company's project figure ≤ the project's total** for the same
  metric and window (one scope level up).
- **Contributors ≤ participants ≤ contributions** for the company.
- **One vocabulary per slide**, and the grain (account or parent) on every
  slide that names the company.
- **Every rank says among whom**, at which grain, on which date or window.
- **Every caller-visible figure and every layer meeting figure is a floor**
  for the wider population and says what bounds it; layer meeting figures
  say ad hoc, company-meeting figures from the SQL assistant say generated
  SQL, and figures derived from scoped participant records say visible to you.
- **Every figure was re-run for this deck**, and the applied block's
  definition sentence is the population on the slide.
