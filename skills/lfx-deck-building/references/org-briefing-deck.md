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

- **Legal name first.** `search_b2b_orgs` gives the stored legal name and
  identifier; the everyday name is often a stray account with nothing on
  it or a shell with a little (a few enrollments) that returns a confident
  zero for everything else. A zero for a company that plainly has data is
  a wrong name. The record vocabulary of the membership records
  (`search_members`) confirms the same identifier.
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
  column applies); meeting and participant records carry free-text
  organisation names (D15: aliases unmerged) and say so.
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
contributors (code) and participants (code or collaboration) for the
company, distinct people, never summed across projects; per project as a
breakdown. Participants widen to any activity later
`[not yet in production: SM-3 participants = any activity — until then:
code or collaboration, said so]`. Label: governed.

**Top contributors from the company.** Contributions by contributor for
the company: a people ranking by identity, presented only where naming
individuals is appropriate for the audience, otherwise as a count. Label:
governed.

**Maintainers from the company, by project.** Standard metrics,
maintainers by project with the company as the organisation; LF projects
only, as of today, roster-based. The group view (subsidiaries at any
depth) is the family's subsidiaries switch, or ad hoc through the layer's
top-parent dimension on maintainers, said so. Label: governed / ad hoc.

**Share of a project's work.** Volume over the org-attributed base of the
same metric, scope and window; the unattributed share stated once on the
data-notes slide. Label: governed.

## Section 3 — Events, sponsorship, training

**Event registrations and attendance by the company's people.** Standard
metrics, registrations by organisation for the company (the registrant's
account): registrations, distinct people, checked-in where the source
carries it. Corporate e-mail domain matching is not a route the tools
offer and a figure built that way is not reproducible. Label: governed.

**Speakers from the company.** The speakers family carries no
organisation scope today; a company reading is the SQL assistant over
accepted speakers by account name, labelled generated SQL, cross-framed
against the family's total for the same events `[not yet in production:
SM-3 speakers by organisation — until then: the SQL assistant reading]`.
Label: generated SQL.

**Sponsorships: which events, which tier, how much.** Standard metrics,
sponsorships by organisation for the company and by event; one event can
carry several assets; tier names as stored per event. The subsidiary's
sponsorships are separate rows under the parent. Label: governed.

**Training and certification by the company's people.** Standard metrics,
enrollments and certifications by organisation for the company;
placeholder accounts for unaffiliated learners are unattributed rows,
never companies; platform data only. Label: governed.

## Section 4 — Governance

**Seats the company holds, across which boards, with what vote.** The
committee tools: for each foundation in the company's footprint, the
board-category committees, each roster paginated to the end, filtered on
the company's organisation identifier, client-side; voting status and
role from the seat record. "Visible to you"; a company's seats can split
across spellings (D15). `[not yet in production: TOOLS-1
get_org_committee_seats — until then: paginate each board and filter]`.
Label: visible to you.

**Key contacts.** The membership records' key contacts — people, shown
only where naming individuals is appropriate for the audience. Label:
visible to you.

## Section 5 — In the room (meetings)

**Meetings the company's people attended; attendances by month; hours.**
Two readings, both floors bounded by platform onboarding and both on the
attendance data's organisation field (loosely resolved, no subsidiary
roll-up: the company's spellings are listed and said). Attendances by
period for the company: the interim semantic-layer recipe, labelled
interim, worded "attendances". Distinct meetings the company's people
attended and the hours those meetings ran: the SQL assistant over the
same attendance data (occurrence key and scheduled duration are stored
per occurrence; hours summed over distinct occurrences, never over
attendance rows), labelled generated SQL. The meeting tools list one
project's or one meeting's records without an organisation filter, so
they give the story of one meeting, not the company figure
`[not yet in production: TOOLS-1 participant filters and
count_lfx_resources; TOOLS-2 org meeting KPIs — until then: the interim
recipe for attendances, the SQL assistant for occurrences and hours, the
vocabulary note on both]`. Label: interim / generated SQL.

## Section 6 — Peers and comparisons

- Every peer is resolved to its legal name and read at the same grain and
  window as the company; a peer table mixes no grains.
- "Same point last year" uses the same day-of-year on both windows.
- Rank movements are read from two complete rankings, not from a
  remembered earlier deck.

## Section 7 — What the briefing cannot say from LFX today

Listed on the data-notes slide, not silently dropped: meeting attendance
by company as a governed figure (today interim and generated SQL, floors);
speakers by company as a governed figure;
maintainers of subsidiaries at depth; distinct organisation counts for
"members of N foundations" at organisation grain
`[not yet in production: SM-3 member_organizations]`; anything matched by
corporate e-mail domain; any figure from a previous deck that is not
re-run.

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
- **Every "visible to you" and "interim" figure is a floor** and says so.
- **Every figure was re-run for this deck**, and the applied block's
  definition sentence is the population on the slide.
