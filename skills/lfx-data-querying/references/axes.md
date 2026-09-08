<!-- Copyright The Linux Foundation and each contributor to LFX. -->
<!-- SPDX-License-Identifier: MIT -->

# The axis register — what a scope selects, what it does not, and the sentence never to write

The characteristic failure this register exists for: the tool applies a
scope correctly and the prose narrates it with the wrong idea of what the
scope selected. The scope line was right; the sentence invented a tree, a
roll-up, a population or a window that never ran. One row per axis, in
the reader's words: what the value selects, what a caller tends to think
it selects, the sentence that is therefore forbidden, and how the answer
says it instead. The tool's own words for each row live in the applied
block and the guidance (*SM*, *SL*), and the answer's sentence agrees with
them; it never embellishes them. No parameters here, no counts.

## 1. Project on memberships (and registrations, sponsorships)

- **Selects:** with the default fold, the memberships attached to that
  slug plus whatever the warehouse's project spine places under it — and
  hosted foundations are their own spine roots, so for the umbrella that
  is its own programme and next to nothing else; with the "excluded"
  switch, the programme alone. The applied sentence names which ran.
- **Does not select:** the memberships of the hosted foundations (CNCF,
  PyTorch and the rest carry their own slugs and their own spine roots);
  the children the project records show under the umbrella (that is the
  record tree, not the spine — two different trees). LF-wide is no project
  filter.
- **Forbidden:** "memberships in projects hosted under the LF", "the tlf
  bucket of N projects", "excluding CNCF and PyTorch" (they were never in
  scope), any child-project count glued to a membership figure.
- **Say instead:** "organisations holding a membership in the Linux
  Foundation's own programme, as of today; CNCF and the other hosted
  foundations run their own programmes and are reported separately."
  When the tool carries its own scope sentence, quote it
  `[not yet in production: SM-3 applied.scope — until then: the words above, from the applied block's project and subprojects fields]`:
  the umbrella with the default fold reads "tlf is the umbrella root of
  the project tree and the Linux Foundation's own membership programme,
  not the LF-wide scope; the foundations hosted under the LF are their
  own roots with their own programmes and slugs and are not included";
  excluded reads "the Linux Foundation's own membership programme only;
  hosted foundations carry their own slugs; omit project for LF-wide";
  any other root reads "memberships of the <name> programme, and of the
  programmes the spine places under it".

## 2. Project on the activity families (contributors, contributions, participants, maintainers)

- **Selects:** by default, the slug and every project under it on the
  project spine, folded, at any depth; with "separate", one row per
  project, and distinct counts do not add up across rows; with
  "excluded", the slug's own bucket only, nothing under it.
- **Does not select:** the project's own bucket alone (that is the
  "excluded" reading), nor a subtree read through the plain project column
  (which matches only the node's own bucket on ad hoc queries). Sum
  metrics read ad hoc outside the spine inflate; counts do not. A count
  of projects from the project search tool covers only the projects
  onboarded into LFX v2 and visible to the caller, never the project
  population: "how many projects" is the layer's project metrics over the
  authoritative project directory.
- **Forbidden:** "contributions to CNCF itself, not its projects" for a
  default reading; "CNCF and its projects" for a bucket-only reading; a
  foundation activity figure read on the plain project column presented as
  the foundation's.
- **Say instead:** "CNCF and every project under it on the project spine,
  folded" / "one row per project; distinct counts do not add up across
  rows" / "CNCF's own bucket only, nothing under it" — whichever the
  applied sentence names.

## 3. The subprojects and subsidiaries switches

- **Selects:** *combined* reads the whole tree (or the whole company) and
  folds it into the grouping's rows; *separate* reads the same whole and
  returns one row per subproject or subsidiary; *excluded* reads the named
  node or account alone.
- **Does not select:** *separate* is not "combined plus a breakdown" —
  distinct counts on its rows do not sum to the combined figure;
  *excluded* on a company is the default, so a company figure with no
  switch is the account alone.
- **Forbidden:** "IBM including Red Hat" on a figure read with the default;
  a parent total obtained by adding separate rows; "all of Kubernetes'
  subprojects" on an excluded reading.
- **Say instead:** "the IBM account alone" / "IBM as one company including
  its subsidiaries at any depth" / "broken down by subsidiary; the rows do
  not add up to the company figure because a person counts once".
  The tool's own organisation clause, when it lands
  `[not yet in production: SM-3 applied.scope — until then: the words above, from the applied block's org and subsidiaries fields]`:
  "the account '<name>' alone" / "with its subsidiaries at any depth,
  folded" / "and its subsidiaries at any depth, one row each; rows do not
  add up"; a stored name that resolves to several accounts says so and
  takes each.

## 4. Organisation: name, parent, vocabulary

- **Selects:** the stored legal account name, on every family — the
  organisation scope and the account and parent columns are CRM accounts
  on the activity families too; the parent is the direct parent, except on
  a parent leaderboard (no organisation named, subsidiaries folded or
  separate) where it is the top of the chain. A company's figure is the
  account unless a switch says otherwise.
- **Does not select:** the everyday name (a stray or shell account with
  little or nothing on it); the enrichment vocabulary (the employer the
  contribution data names), which appears in exactly two places — the contributing-organisations count and the
  employer-region grouping; the free-text organisation on meeting and
  participant records; the roster's organisation on committee seats.
- **Forbidden:** "IBM" as a scope when the legal name ran; "Red Hat" (an
  enrichment spelling) and "Red Hat LLC" (an account) as the same row; a
  membership figure and a contributing-organisation figure compared as if
  one vocabulary; a zero for a company that plainly has data presented as
  absence.
- **Say instead:** "the International Business Machines Corporation
  account" / "organisations as the contribution data names them, which is
  a different vocabulary from the membership records".

## 5. Time: windows, as-of dates, periods, days

- **Selects:** window families read a window of UTC calendar days — by
  default the trailing twelve months to today on the activity, event,
  training and social families, and all history on the membership
  movement families (new, churned, lost, new organisations); as-of
  families read the state on the end date (today by default, status-based
  today and date-based on any other day); a period series returns one
  bucket per period for window families and the state at each period end
  for as-of families; the last row of a to-date series is partial and
  flagged.
- **Does not select:** a calendar year unless asked as dates; "this year"
  bounded at today unless the tool bounded it; the semantic layer's
  session-clock day boundary (its day-grain time-dimension filter drops
  the first UTC day, so an ad hoc day window is bounded on the
  UTC-anchored dimension); a window computed by hand.
- **Forbidden:** "in 2025" on a trailing-twelve-months reading; "as of
  today" on a series row; "the last five years" from a self-chosen start
  date; a partial year quoted as a full one.
- **Say instead:** "the twelve months to <date>" / "as of <date>,
  date-based" / "<year> to date, through <date>".

## 6. Population: which people, which projects, which records

- **Selects:** contributors = distinct people with a code contribution,
  bots excluded; participants = distinct people with a code contribution
  or a collaboration activity `[not yet in production: SM-3 participants =
  any activity]`; maintainers = today's roster of LF projects;
  registrations = records, registrants = distinct people by e-mail,
  checked-in only where the source carries it; enrollments = records,
  enrolled users = distinct people; project health and software value =
  LF-hosted projects on the latest snapshot unless the population grouping
  is asked; social reach per project is not additive.
- **Does not select:** "developers" in general, the whole maintainers
  index, all proposal statuses for speakers, people-hours for meetings,
  the index population for health.
- **Forbidden:** "developers who took part" on a contributors reading;
  "attendees" on a registrations reading; "all projects" on an LF-hosted
  health figure; a total of per-project social reach.
- **Say instead:** the population sentence the applied block returned, in
  the reader's words, once per figure.

## 7. Geography: whose country

- **Selects:** contributor and contribution country and region follow the
  person and are known for a minority; organisation region follows the
  employer's headquarters; membership country is the account's billing
  country, conformed, with an unresolved row for accounts whose country is
  unknown or whose stored spelling did not resolve; the LF region grouping
  is provisional.
- **Does not select:** where the work happened; where a subsidiary sits; a
  country for the unresolved row.
- **Forbidden:** "N countries" counting the unresolved row; "developers in
  APAC" without naming the stored rows it was built from; a region claim
  without the provisional note; "the bigger footprint" across members and
  contributors without saying they are two subjects.
- **Say instead:** "countries of the account's billing address, N
  resolved plus an unresolved group" / "the person's own country where
  known, which is a minority of contributors" — and the comparison
  sentence names the two subjects before the numbers: a billing-address
  footprint and a people footprint are two readings, not one bigger and
  one smaller.

## 8. Ranking, limits, identities

- **Selects:** the rows the limit allowed, in the order asked; the
  unattributed row sorts first on a descending ranking today, so it is
  dropped and the list re-sorted before a top-N is read
  `[not yet in production: SM-3 — the unattributed row sorts last on both
  engines, and a top-N never contains it unless the list is longer than
  the attributed rows]`; a people ranking is by identity (handle), and two
  identities can share a display name.
- **Does not select:** "all" when truncated is true; an organisation in the
  unattributed row; one person per display name.
- **Forbidden:** "the top five organisations" with the unattributed row
  among them; "all contributors" on a truncated list; two handles merged
  into one person.
- **Say instead:** "the five largest attributed organisations; N% of the
  volume has no resolved organisation" / "the top N shown; the list was
  cut at N".

## 9. The SQL assistant's scope line

- **Selects:** exactly the slugs listed, or LF-wide when none was listed;
  nothing is injected; an unknown slug is rejected before the query runs.
- **Does not select:** a tree for a foundation slug; a default project
  when none was given.
- **Forbidden:** "LF-wide" on a slug-scoped answer; "CNCF and its
  projects" on a single-slug answer; a project scope the answer's scope
  line does not show.
- **Say instead:** the scope line the tool returned, first, in the
  reader's words.

## How this register is used

Before the population sentence of any figure is written, find the axes
the figure sits on and check the sentence against the forbidden column.
Where the applied block or the scope line names the difference in the
tool's words, the answer repeats that meaning; it never adds a tree, a
roll-up, a population or a window the block does not name.
