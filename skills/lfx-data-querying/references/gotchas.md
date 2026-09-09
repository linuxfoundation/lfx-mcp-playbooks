<!-- Copyright The Linux Foundation and each contributor to LFX. -->
<!-- SPDX-License-Identifier: MIT -->

# Gotchas — symptom, cause, check, where documented

One entry per line of the playbook's section 5, in the same order. Each
names the symptom you see, the cause, the check that catches it, and the
guidance section that documents the behaviour and its switch. No parameters
here either: the guidance owns them. No figures: a trap's size is said
qualitatively, and anything you measure yourself carries "measured <date>"
and an instruction to re-run.

Guidance readers: `read_lfx_standard_metrics_guidance` (below: *SM*) and
`read_lfx_semantic_layer_guidance` (below: *SL*). Section names are the
headings in those documents. Two companions: a difference between two
tools' figures is explained by mechanism in
[why-figures-differ.md](why-figures-differ.md); the craft of the record
tools is in [service-tools.md](service-tools.md).

## 1. Unresolved names

- **Symptom.** A count of zero, or a plausible small number, for a project
  or company that plainly has data; or a rejection listing candidates.
- **Cause.** Stored slugs and legal names are not the everyday names. The
  semantic layer returns zero rows for a literal that matches nothing; the
  standard metrics reject an unknown slug or a name matching no account
  that carries the family's data, and list candidates instead.
- **Check.** Every slug came from `search_projects` and every organisation
  name from `search_b2b_orgs` in this session. A zero from the layer sends
  you back to discovery, not to "none".
- **Documented.** SM "Resolve names first — ALWAYS", "Organizations:
  account and parent_org", "Errors"; SL "Protocol", "Value discovery".

## 2. Hand-assembled dimension names

- **Symptom.** An error on the dimension name, or a "did you mean" list
  that omits the name you need, or a query that runs against a dimension
  from the wrong entity and returns a different population.
- **Cause.** Qualified dimension names are entity-prefixed and the prefix
  differs per metric; the fuzzy match on an unknown name is not
  authoritative.
- **Check.** Every dimension name in the query was copied from explore
  output for that metric, in this session.
- **Documented.** SL preamble and "Value discovery".

## 3. Two organisation vocabularies

- **Symptom.** A company appears under one spelling in a membership table
  and another in an activity table; one of the two shows nothing.
- **Cause.** CRM account names (legal names) and the enrichment vocabulary
  on activity data are different systems, and they do not line up row for
  row.
- **Check.** One vocabulary per answer. An organisation-attributed activity
  figure and a membership figure are compared only when both were read on
  the account vocabulary.
- **Documented.** SM "Reading results"; SL "Worked recipes" 5 and 6.

## 4. Bots

- **Symptom.** A contribution or contributor figure noticeably higher than
  the same figure from a governed lane.
- **Cause.** Bot exclusion is built into the governed contributor and
  activity metrics; a figure produced outside them may include bots.
- **Check.** The population sentence says "bots excluded" once; a figure
  from the SQL assistant is cross-framed against the governed reading.
- **Documented.** SM "Inventory" (contributors, contributions); SL "Worked
  recipes" 1.

## 5. Organisation shares on the wrong base

- **Symptom.** Shares that sum to well under the whole, or a "largest
  contributor" that is the unattributed bucket.
- **Cause.** A large share of activity has no resolved organisation; a
  share computed over the full pool, or over headcounts, misstates it.
- **Check.** Share of work is volume over the org-attributed base of the
  same metric, scope and window; the unattributed share is stated once,
  separately.
- **Documented.** SL "Worked recipes" 2 and 3; SM "Inventory" (the
  contributions and maintainer-contributions rows).

## 6. Headcount versus volume; distinct counts

- **Symptom.** Per-organisation or per-project rows added up to a "total"
  that exceeds the governed total; a "share" built from people rather than
  work.
- **Cause.** Contributors, participants, registrants, enrolled users and
  contributing organisations are distinct counts — one person in two
  projects is one person, but one row in each. Volumes are additive;
  headcounts are not.
- **Check.** A headline distinct count comes from one call with the whole
  scope folded; the breakdown is a second call, never a sum of the first.
- **Documented.** SM "The switches, row by row", "Reading results",
  "Inventory" (the "never sum rows" caveats).

## 7. Daily snapshots

- **Symptom.** A project count or a software value several times too large.
- **Cause.** Health and software value are one row per project per day;
  aggregating across days counts each project once per day.
- **Check.** Health and value figures come from their families, which pin
  the snapshot; an ad hoc reading filters to one health-bearing date before
  aggregating.
- **Documented.** SM "The two kinds, with examples", "Inventory" (the
  project-health and software-value rows); SL "Worked recipes" 8 and 9.

## 8. Foundation slug on the plain project column

- **Symptom.** A foundation's activity figure an order of magnitude too
  small, with no error.
- **Cause.** The plain project slug of a foundation matches only the
  foundation's own catch-all bucket, not its projects. The standard
  metrics' scope handling is different and documented; this trap is
  specific to ad hoc queries.
- **Check.** A foundation is scoped with the foundation dimension; the
  answer says "and its projects".
- **Documented.** SL "Scope"; SM "Projects and subprojects".

## 9. The unattributed row

- **Symptom.** "The largest contributing organisation is NULL" or a blank
  name at the top of a ranking; a parent total that grew when the
  unattributed row was folded in.
- **Cause.** Rows with no resolved account or employer are unattributed
  work, not an organisation; on the standard metrics they sort last, so a
  top-N holds them only when the list outruns the attributed rows; on an
  ad hoc layer query NULL rows sort first on a descending metric.
  Under a sort on the measure itself the unattributed row can top the
  list on either lane, because it is often the largest row.
- **Check.** The unattributed row is reported as unattributed, dropped from
  every organisation ranking and from every parent fold, and the ranking
  is re-sorted before the top-N is read.
- **Documented.** SM "Reading results"; SL "Query syntax", "Worked
  recipes" 2.

## 10. JDF series memberships

- **Symptom.** A Joint Development Foundation series shows few or no
  memberships under its own slug.
- **Cause.** Memberships attach at foundation level, and a JDF series and
  its `-fund` project are one consortium whose memberships sit on the
  fund, not on the series slug.
- **Check.** On the membership and organisation families the default
  combined reading of either slug is the whole consortium in one call,
  and the applied block lists the members — name them in the answer;
  excluded reads the named project alone; on any other family, and on the
  layer, the series and its `-fund` project are two slugs: ask for both,
  and say they were combined. A JDF-wide organisation count is not one
  call: the membership axis scopes one programme at a time, so list the
  consortia under the JDF legal entity (one hop below the foundation
  record) with the project search's legal-parent filter, then read
  distinct organisations across their slugs in one layer query; the
  per-programme rows do not sum, and the answer says so.
- **Documented.** SM "Resolve names first — ALWAYS" and "Projects and
  subprojects" (Consortia); SM "Inventory" (the
  memberships row: memberships attach at foundation level); the
  `query_lfx_lens` tool description (a JDF series plus its `-fund` parent is
  one call).

## 11. Governance rosters

- **Symptom.** A board or committee membership stated from tier, event or
  activity data.
- **Cause.** Rosters live only in the committee tools; every other source
  is inference.
- **Check.** Any seat, chair or voting status came from
  `search_committee_members`, paginated to the end.
- **Documented.** SL "Routing", "Worked recipes" 12.

## 12. Meetings

- **Symptom.** A meeting count or attendance figure presented as complete,
  or a meeting metric fetched from a lane that does not hold it.
- **Cause.** The meeting tools return the meetings visible to the caller
  and do not aggregate; the layer holds every meeting in the warehouse
  with no per-caller visibility, as four readings that are easy to
  swap: occurrences, scheduled minutes, attendees (people) and
  attendances (records, one person at one occurrence).
- **Check.** Lists and details from the meeting tools, labelled "visible to
  you"; aggregates from the layer's named metrics, discovered with
  explore and copied, never assembled: meetings held are the occurrences
  metric (with or without attendance is a dimension, say which);
  duration is scheduled minutes, never time spent — join and leave times
  are not recorded; people are the attendees metric (an LF user, e-mail
  where the user is unknown), never invitee ids, which read like a people
  count ten times too large; attendances are the attendance recipe's
  records, and the only reading that carries the organisation. People's
  time (attendances times length) is a separate figure from
  meeting-minutes — say which. An occurrence shared by several projects
  is attributed to one of them. A tool figure is cited as "visible to
  you", a layer figure as "all meetings in the warehouse", and neither
  is reconciled against the other. A people figure anywhere near the
  attendance figure is a key error. (if explore does not offer them, the SQL assistant over the attendance data gives occurrences and scheduled minutes, the attendance recipe attendances)
- **Documented.** SL "Routing", "Worked recipes" 12.

## 13. Membership count and revenue

- **Symptom.** "Average dues per member" or a revenue-per-membership ratio.
- **Cause.** The count is distinct project-account pairs with an active
  term; the revenue is the list price of the active membership assets, not
  dues billed. Different grains. And an organisation holding memberships on
  several projects counts once per project, so "how many members" in the
  everyday sense (distinct organisations) is a third reading, the
  member-organisations family (paying-only: its paying sibling) — "how
  many members" is that family, never derived from membership rows.
- **Check.** Presented side by side, never divided; "list-price value"
  said in the population sentence; the organisation reading taken from
  its own family, never obtained by pulling every organisation row and
  counting them — counts come from the one-figure grouping, breakdowns are
  listed with a limit.
- **Documented.** SM "Inventory" (memberships), "Reading results".

## 14. Year-to-date and future-dated installs

- **Symptom.** A current-year new-member count that later goes down.
- **Cause.** Memberships can be installed with a future date; an unbounded
  current-year bucket counts them.
- **Check.** Any current-year or to-date count is bounded at today, and the
  last row of a series is labelled partial when the tool says so.
- **Documented.** SM "Defaults and the applied block", "Reading results";
  SL "Windows".

## Also worth knowing (same discipline, no separate line in the playbook)

- **Tier literals differ per foundation.** Look them up per foundation;
  never reuse. SL "Worked recipes" 7.
- **The umbrella foundation's own slug is not LF-wide.** LF-wide is
  unscoped, and the answer says which population it used. SL "Scope".
- **Memberships attach at foundation level.** A leaf project's own
  memberships are empty by attachment, not by data loss. SM "Projects and
  subprojects"; SL "Scope".
- **Twin slugs exist** for some project families; a low total sends you to
  a breakdown by slug. SL "Scope".
- **Churn dates fall the day after the term ends**, so a year-end churn
  lands in the following year. SM "Inventory" (the membership-churn row).
- **Speakers are accepted speakers only**, distinct people; by
  organisation is the speaker's account as resolved from the proposal,
  with a large unresolved row that is reported as unattributed.
  SM "Inventory" (the speakers row).
- **Training and certification are platform data**: lifetime totals read
  below the official trained figure, and one branch carries no account.
  SM "Inventory" (the training-enrollments and certifications rows).
- **Region groupings**: contributor country and region follow the person
  and are known for a minority of contributors; organisation region follows
  the employer's headquarters. The LF region grouping is provisional
  pending stakeholder sign-off — say so whenever a region grouping appears
  in an answer. SM "Inventory" (contributors, contributions); SL "Worked
  recipes" 13.
- **Day boundaries differ between lanes.** The standard metrics and the
  SQL assistant bound windows on UTC calendar days; the semantic layer's
  day-grain time-dimension filter cuts at midnight US Pacific, so an ad
  hoc window sits a few hours off a UTC one and can lose or gain a day's
  activity at each edge (a date-typed dimension bound stays on the UTC
  day, verified). State the window, never claim an exact calendar day
  across lanes, and never call a small cross-lane difference an error.
  SM "Reading results"; SL "Routing", "Windows".
- **A project the search cannot find is not absent from the data.**
  `search_projects` reads the LFX v2 index, which lags the project
  directory the layer and the standard metrics read, so a real project
  can be missing from the search and still carry data. A standard-metric
  rejection lists candidate slugs from the directory, and the layer's
  project dimension values are the census: take the slug from there, say
  which surface named it, and never report "no such project" on the
  search alone. The reverse holds too: a record in the search is no proof
  the layer has data for it. SM "Errors"; service-tools reference "The
  search is not a census".
- **The explore listing can lag the layer.** The dimensions that explore
  lists for a metric come from a cached view that refreshes on its own
  schedule, so on the day a definition ships a dimension can run at query
  time while explore still omits it (measured 2026-09-08 on the account
  path dimensions of the membership metrics). A rejection at query time
  is authoritative; an omission in explore is not. That is no licence to
  assemble names: copy the qualified name from explore's output for a
  sibling metric on the same entity, run it, and treat the compiled SQL
  as the proof of what was joined. SL "Value discovery".
- **No refresh stamp exists yet.** No lane reports when its tables were
  last loaded; the same window re-run a day apart can move slightly. Record
  the run date with every figure and re-run rather than reconcile.
