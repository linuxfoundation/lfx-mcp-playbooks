<!-- Copyright The Linux Foundation and each contributor to LFX. -->
<!-- SPDX-License-Identifier: MIT -->

# The membership-value deck — a workload pattern

The recurring executive deck that argues the value of Linux Foundation
membership: growth, the coordination the LF hosts, the developer community,
project health, reach through events and training, governance, dues, and
the stories that carry the argument. This reference is the pattern, not a
slide list: each section names the questions it asks, the tool and the
reading that answers each, the trap the assessment registers found in that
section (code and mechanism, from the data-defect register D1–D20 and the
access register M1–M16), the check, and the label. No figures, no
parameters: the guidance owns the calls, the querying playbook owns the
routing, and this file owns what a value deck needs from them.

Lines that need something not deployed carry
`[not yet in production: <bundle> — until then: <fallback>]`. The fallback
is what the deck does today.

## Before the first section

- Conventions first (querying playbook §1 of the deck playbook): one
  window, one organisation grain, one denominator policy, the scope of
  each section written down. A value deck mixes LF-wide sections with
  foundation sections; the section heading carries the scope.
- **The whole LF is no project.** Every LF-wide figure leaves the project
  unset; the umbrella's own slug is a bucket (M1: the generated-SQL lane
  once injected that slug silently and the headline shrank several times
  over). Check: the scope line or the applied block says LF-wide.
- **Resolve every foundation and company name first**, and know which
  projects are a consortium (M8, D11: a series' memberships sit on the
  fund, and a headline once read on the series slug alone undercounted
  several times); the membership and organisation families read the whole
  consortium in one call by default and list its members, and the appendix
  row names them.
- **Run date stands for freshness** (M16: no lane stamps a refresh time).
  Every figure carries the run date in the appendix.

## Section 1 — Growth and momentum

**Communities hosted over the years.** A published series: the annual
reports' own figure per year, cited as such and never rebuilt from the
project index (D19: report definitions changed between years; only a run
of years with one definition is chartable). Label: published.

**New memberships per year.** Standard metrics, the new-memberships family
as a bare series by year, LF-wide; each year quoted from its own row, the
current year marked to-date, and the table saying which years it shows.
Trap D10 / M13: this is account-project grain — a company joining a second
project counts again — and the deck once read it as "new members" at
organisation grain and had to be relabelled. Say "new project
memberships". Check: the slide caption names the grain; the yearly rows
add up to the family read as one figure over the same span (one row per
project, organisation and install day), and the to-date row matches a
second reading bounded at today. Label: governed.

**New member organisations.** Standard metrics, the
new-member-organisations family LF-wide: organisations arriving in the
year — no membership anywhere in the LF the day before, so a lapsed
account that rejoins counts as new again, as the CRM counts New
Business; the level of arrival named as the applied block gives it. A
"first time ever" slide is the layer's first-membership dimension, ad
hoc, and says it counts memberships. Check: arrivals sit below the year's
new memberships (an organisation joining two programmes is one here, two
there), the current year bounded at today (M12: future-dated installs
inflate an unbounded current year). Label: governed `[not yet in production: DBT-2c on the standard-metric families — until then: the new-organisations family's definition sentence still says first membership while its rows count arrivals, and the lost-organisations family still excludes organisations that have since returned; the layer's metrics carry the new meanings, so say which path ran]`.

**Growth as a roll-forward.** Members at the start of the year, joins,
departures, members at the end: the at-date family on 31 December of
the prior year and of the year, the new-memberships and churn families
over the year — the same at organisation grain with the new- and
lost-organisation families. The four never balance exactly; the notes
name the residue by mechanism (the querying playbook's "Roll-forward
residues"), and the caption says gross joins, never new-minus-churned as
the growth. Label: governed.

**Same point last year.** The comparison a growth slide wants ("more than
at this point in the previous year") is two windows with the same
start-of-year and the same day-of-year end, both stated as dates; never a
trailing window against a calendar one. Label: governed.

**Membership today versus a decade ago, five-year scoreboards.** Published
figures (annual reports, prior decks); cited, "carried, not regenerated"
where the graphic is reused. Label: published or carried.

## Section 2 — The coordination engine (meetings)

**Meetings hosted, hours of meetings.** The layer's occurrences metric
and its scheduled-minutes metric, LF-wide with no project set, by
foundation or by period, cross-framed against the attendance count for
the same window; minutes are scheduled, never time spent, and are
converted to hours on the slide with that said. Every meeting figure is
a floor: only meetings run through the LF's meeting platform exist here
(D9). Trap D8: an hours figure built from attendances times a sampled
average is an estimate and says so, and is the worse route. Label: ad
hoc, floor (if explore does not offer them, the SQL assistant over the attendance data gives occurrences and scheduled minutes, the attendance recipe attendances).

**People who attended, attendances.** The layer's attendees metric
counts people (an LF user, e-mail as the fallback), never invitee ids,
and sits far below the attendance recipe's records (one person at one
occurrence); the meeting tools list what the caller's identity may see.
Trap M3: no metric family covers meetings, so the names come from
explore. Label: ad hoc for people, interim for attendances, each
worded as such.

**Organisations that show up most; breadth and intensity.** Attendances
grouped by the organisation the meeting record carries, on the interim
recipe — the invitee's account as the source spelled it, free text with
no rollup and no subsidiaries (D15: aliases unmerged, so one company
splits across spellings) — distinct people for breadth, attendances per
person for intensity; the slide says which vocabulary the grouping used
and carries the alias note; two buckets are not companies and are stated
once as unattributed; LF-hosted entities (the LF's own staff, a
foundation's own secretariat) top an attendance ranking and are set aside
from the member ranking, said on the slide. Label: interim
`[not yet in production: TOOLS-2 — until then: the interim recipe with the
vocabulary note]`.

**Projects and working groups that met.** A distinct count of projects on
the same data, floor by onboarding. Label: interim. (A foundation's
project *population* is the layer's project metrics over the
authoritative project directory, never a count of the projects indexed in
LFX v2.)

## Section 3 — The developer community

**People active across LF projects; growth year over year.** Standard
metrics: participants (any non-bot activity) for "took part",
contributors for "wrote code"; both LF-wide, both distinct people, each
window stated as dates; year-over-year is two complete windows. Trap D5:
three contributor counts exist for the same question (definition,
population, bots) — the deck names which and holds it; participants is
any non-bot activity, stars, forks, meetings and training included, so
the "took part" figure runs well above "wrote code" and the slide says
why. Label: governed.

**What developers do in a year: commits, pull requests, reviews, issues,
by platform.** Semantic layer, activity counts by type and by platform,
LF-wide, one window; each type is its own row and types are never summed
into a "total" unless the metric is the total (D7: activity identifiers
repeat across rows, so the obvious query over-counts; the governed
distinct metric is the check). "Per day" figures are the window total
divided by its days, said so. Label: ad hoc.

**Contributors by project or foundation.** Standard metrics, contributors
by project, or one call per foundation; a foundation row includes its
hosted projects (scope statement on the slide). Distinct counts do not sum
across rows. Label: governed.

**Top organisations by contributors and by volume.** Standard metrics,
contributors and contributions by organisation, parent grain chosen and
said; the unattributed row is not an organisation and is dropped from the
ranking (re-sort before the top-N); the unattributed share is stated once
(D1: the employer is resolved for a minority of people, so every
organisation headcount is a floor and shares are on the attributed base).
Volume is the honest way to express share of work; headcount says how
many people. Label: governed.

**Contribution and membership by region and country.** Standard metrics
by country and region: contributions and contributors follow the person
(known for a minority, D4), memberships follow the account's billing
country (near-complete coverage). The LF region grouping is provisional
pending sign-off and the slide says so; "APAC" in the everyday sense is
several stored rows together. Label: governed, region provisional.

## Section 4 — Maintainers and stewardship

**Maintainers, active maintainers.** Standard metrics, maintainers family:
LF projects only, as of today, roster-based. An ad hoc count over the
whole index reads higher. By company: the family by organisation
(subsidiaries folded with the switch), or ad hoc by the layer's
top-parent dimension. Label: governed.

## Section 5 — Project health and software value

**Projects scored, health bands, at-risk count, average by foundation.**
Standard metrics, project-health family: the latest snapshot, v2 bands by
their stored names, LF-hosted unless the population grouping is asked
for. Trap D12 / M11: the health data blends LF-hosted projects with a wider
index, and an unfiltered aggregate over daily snapshots counts each
project once per day — the family pins both. History is short (D13): no
trend and no tenure claim. Label: governed; a value-weighted or
count-weighted reading is an ad hoc composition on the same snapshot,
labelled ad hoc.

**Software value tracked.** Standard metrics, software-value family:
each project's own latest row, USD, additive across projects and never
across days; the applied coverage says how many projects carry a value.
Label: governed.

## Section 6 — Reach: events, training, certification

**Events, registrations, speakers.** Standard metrics: registrations
(accepted, by event start date, distinct people separate from records,
check-in only where the source carries it), speakers (accepted only,
distinct people; by organisation is the speaker's account as resolved
from the proposal, with a large unresolved row stated once),
sponsorships (assets and their price, all tiers). Label: governed.

**Course enrollments and certifications.** Standard metrics, training and
certification families: platform data only, so the lifetime headline is a
published figure (D17: two enrollment figures exist on different tables;
publish the definition of the one used); placeholder accounts for
unaffiliated learners are named as unattributed, never as organisations.
Label: governed; lifetime claim: published.

**Reach headline (attendees, learners, certified).** The annual reports'
"by the numbers", cited per year, never reconciled against the platform
figures on the same slide. Label: published.

## Section 7 — Mentorship, crowdfunding, social listening

**Mentorship and crowdfunding.** Out of scope of the tools (D20); published
figures, cited with document and year. Label: published.

**Mentions, reach, authors, platforms; brand portfolio reach.** Standard
metrics, social-mentions and social-reach families by project; reach is
potential impressions, the sum of author followers per mention (a
prolific author counts once per mention; follower counts exist for one
network only), never an audience, and portfolio reach is not additive
across projects (D18: the feed begins recently, so no long trend;
project sets are curated). Label: governed.

## Section 8 — Consortia and joint development

**Organisations that have signed, consortia launched and active, active
memberships across consortia, the largest consortia.** Memberships by
project on the consortium's slug: the default combined reading is the
whole consortium in one call, its members listed in the applied block
(M8: a series slug alone once undercounted); distinct signatory
organisations is the member-organisations family on the same scope (D11,
M2: an ad hoc grouped distinct count was once capped and the headline had
to be stated as a floor — the family gives the figure).
Consortia counts come from the project records (active stage, legal
entity type), "visible to you". Label: governed / ad hoc / visible to you,
per line.

## Section 9 — Governance

**Top organisations by board seats; foundations spanned; total seats;
voting split; unaffiliated seats; cross-industry holders.** Rosters live in
the committee tools and nowhere else; one organisation's seats are the
organisation seats tool (board split, per-project summary, under the
organisation gate); a ranking of organisations by seats across all
projects is the generated-SQL reading over the committee data with staff
and unaffiliated seats set aside; totals of committees and of seats on
them are the count tool, one kind a call, "visible to you", with the
complete flag read, and across all onboarded projects regardless of
status unless combined with the layer's directory. Traps D14 and D15:
roster records carry no "community-elected" attribute, so unaffiliated
seats are a proxy and say so; organisation aliases are unmerged, so a
company's seats can split across spellings. Committee members' countries
are not a roster field (deck playbook §5). Label: visible to you.

## Section 10 — Dues and funding

**Total current membership dues; dues by tier, by foundation, by region;
top sponsors.** Standard metrics, memberships family (list-price value of
active memberships, dues only, never divided by the count), by tier or by
foundation or by region; sponsorships by organisation for the events
side. Trap D16: non-dues revenue (events, training) is not in the
memberships family, so a "largest funder" share is dues-only and the
slide says so. Label: governed.

**Top members by list-price value; concentration.** Memberships by
organisation ordered by value, parent grain chosen and said (combined
reading for parents, never a hand-sum of account rows). Label: governed.

## Section 11 — Stories and case studies

Project case studies, survey results, third-party figures: cited to the
publishing organisation, document and date; confidence is the source's.
Carried graphics marked "carried, not regenerated". Label: published or
carried. Nothing in this section is LFX data.

## The section-level checks a value deck runs

- **Every LF-wide figure sits above its foundation figure**, and every
  foundation figure above its largest project's. A jump of several times
  is a scope error, not growth.
- **Contributors ≤ participants ≤ activities**, in every section that
  shows two of them.
- **One vocabulary per slide** (CRM legal names on membership and dues
  slides; enrichment or free-text names on activity and meeting slides,
  said so).
- **Every "visible to you" and every "interim" figure is a floor**, and
  the slide says floor.
- **Every published figure is cited and not reconciled** against a
  warehouse figure on the same slide.
