<!-- Copyright The Linux Foundation and each contributor to LFX. -->
<!-- SPDX-License-Identifier: MIT -->

# Why figures differ — the same question, two tools, two numbers

Two LFX tools asked what sounds like the same question routinely return
two different numbers, and both are right. This reference is the catalogue
of the mechanisms behind that, so that a difference is explained in the
reader's words instead of averaged, hidden, or "fixed" by picking the
larger one. No parameters here (the guidance owns them: *SM* =
`read_lfx_standard_metrics_guidance`, *SL* = `read_lfx_semantic_layer_guidance`)
and no figures: a difference is described by its mechanism and its rough
size, never measured into this file.

## How to reconcile

1. **Name the two populations** in words: what each tool counted, over
   which scope, in which window, in which vocabulary. Read them from the
   `applied` block, the scope line, or the record fields — never from the
   request you think you sent.
2. **Walk the catalogue below** for the mechanism that separates them.
   Most differences are one mechanism; a large one is usually scope.
3. **Choose the reading the question wants** and say why. The governed
   reading wins for a headline; the other is reported as a second framing
   or dropped.
4. **If no mechanism explains it**, it is a discovery failure (a wrong
   literal, a wrong slug, a shell account) and the answer is not ready.
   Never present the two side by side as "sources disagree".
5. **Other dashboards and published pages are not a reconciliation
   surface.** They differ by repository registration, member cleaning and
   curated lists; say what the figure covers and stop (*SL* "Scope").

## Memberships and organisations

**Status-based vs date-based membership count.** Today's reading counts
memberships whose status is active; a reading on any other date, and a
series, counts terms that cover that date. The two readings of the same
day differ where statuses lag term dates. A deck uses one kind per
section and says "as of <date>, date-based" when it is not today.
*SM* "Reading results", "Inventory" (memberships).

**Memberships (pairs) vs member organisations.** The family counts
project-account pairs: a company on three projects counts three times.
"How many members" in the everyday sense is distinct organisations, a
reading no governed family gives today
`[not yet in production: SM-3 member_organizations]` — report memberships,
say the grain, say the organisation count is not available as a governed
figure; never pull the rows and count them. *SM* "Inventory"
(memberships).

**Warehouse family vs membership records.** `search_members` shows the
CRM's live membership records for one company (status, tier, project, key
contacts, in the record vocabulary — its own project slugs); the family
counts the warehouse's active pairs. They agree when the warehouse has
loaded the CRM and the company is spelled the same in both; they differ by
load lag, by a record the CRM holds in a non-active status, and by slug
vocabulary (the record's slug for a project is not always the warehouse
slug). The family gives the figure, the record view gives the story of
one company. Never count records into a figure; never quote a record's
status as the warehouse's.

**Account alone vs company including subsidiaries.** The default reading
of a named company is that legal account only. "IBM including Red Hat" is
a different scope, and it is a choice the answer names in words. A
company that is itself a subsidiary vanishes as its own row under the
parent grain. The two readings differ by everything the subsidiaries
hold. *SM* "The switches, row by row", "Organizations: account and
parent_org".

**Account column vs parent column.** Every organisation breakdown carries
both the account and its parent; a row like "Red Hat LLC — parent IBM"
is one account, not two. Ranking by account and ranking by parent are two
different tables, taken from two calls, never by hand-summing the account
rows into parents (a top-N cut hides subsidiaries the sum would miss).
*SM* "Reading results".

**Legal name vs everyday name vs shell account.** The stored organisation
name is the legal name; the everyday name often exists as a stray
same-company account with no memberships and no activity. A stray account
is rejected with candidates when it carries nothing at all, but a shell
that carries a little (a few enrollments, a registration) passes and
returns zero for the family you asked — a confident zero. Resolve the
legal name first, and treat a zero for a company that plainly has data as
a wrong name. *SM* "Resolve names first — ALWAYS", "Organizations".

**CRM vocabulary vs enrichment vocabulary.** Activity data carries the
employer as free text from enrichment ("Red Hat", "Red Hat, Inc.", and
dozens of team and regional variants); membership and account data carry
the CRM legal name. Contributing-organisation counts use the enrichment
vocabulary; organisation breakdowns of contributions use the account
vocabulary. One answer, one vocabulary. *SM* "Reading results",
"Inventory" (contributing_organizations); *SL* "Worked recipes" 5–6.

**List price vs dues billed.** Membership revenue in the family is the
list price of active memberships; dues actually billed are a finance
figure the tools do not hold. Say "list-price value"; never divide it by
the count. *SM* "Reading results".

**New memberships vs new organisations vs churn vs lost.** New business is
first-per-project (a second project counts again, a returning account
counts again). "New to the LF" is a different reading, and it has two
routes today, only one of them honest. The semantic layer carries an
organisation-grain firstness dimension (the membership rows whose install
date is the account's first LF membership ever); filtering the new
memberships metric on it gives first-ever membership *rows*, so a same-day
pair of installs counts twice — report it as ad hoc, say it counts
first-ever memberships rather than organisations, and never head the
column "new organisations". The other flag with "first" in its name is the
CRM's New Business opportunity type: it re-flags a returning account and
is not firstness at all. The distinct-organisation figure is a governed
family `[not yet in production: SM-3 new_member_organizations — until
then: the ad hoc first-ever-membership reading with its caveat]`. Churned
memberships are pairs that ended; a company that dropped one project and
kept another churned but is not lost
`[not yet in production: SM-3 lost_member_organizations]`. The churn date
is the day after the term ends, so a year-end churn lands in the next
year. *SM* "Inventory" (new_members, membership_churn); *SL* "Value
discovery" (read the dimension's own description before filtering on it).

**Billing country vs conformed country.** The raw billing country is free
text; the conformed country entity normalises it and files what it cannot
resolve under NULL. A country breakdown read raw has more rows and
different totals per country than the conformed one; the LF region
grouping is provisional. *SM* "Inventory" (memberships, contributors);
*SL* "Value discovery".

## Projects and scope

**Foundation slug vs the foundation's own bucket.** A foundation's slug on
the plain project column matches only its catch-all bucket; the foundation
dimension matches the foundation and its projects. An order of magnitude
apart on activity, with no error. *SL* "Scope"; *SM* "Projects and
subprojects".

**Whole tree vs one level vs one hop.** The standard metrics walk a
project's tree and a company's subsidiaries to any depth; the semantic
layer's project dimensions reach a foundation completely but a node below
it only one level down, and its account roll-up reaches one hop. A
subtree or company figure read ad hoc is smaller than the governed one by
the deeper levels. *SL* "Scope" (REACH).

**Spine subtree vs segment bucket.** On activity data, one dimension walks
the project spine (every node under a project), another holds a project's
own bucket, a third groups by segment. Same project name, three
populations. Sum metrics need the spine filter or they inflate. *SL*
"Scope".

**The umbrella foundation vs LF-wide.** The umbrella's own slug is one
bucket of hosted projects; LF-wide is no project filter at all. Several
times apart. *SL* "Scope".

**Consortium vs its fund project.** A consortium's memberships can sit on
a sibling `-fund` project; each slug alone is a partial reading and the
combined figure is the consortium. Today the combined reading is two
family calls or one ad hoc query on the consortium dimension, labelled ad
hoc `[not yet in production: SM-3 consortium switch]`. *SM* "Projects and
subprojects".

**Twin slugs.** Some project families exist under two slugs; a low total
is a reason to group by slug before concluding. *SL* "Scope".

**Attachment level.** Memberships, registrations and sponsorships attach
at foundation level; a leaf project's own reading is legitimately
near-empty. Enrollments and maintainers attach below the foundation too.
*SL* "Scope"; *SM* "Projects and subprojects".

## People and activity

**Contributors vs participants vs contributions.** People with a code
contribution; people with a code contribution or a collaboration
(issues, comments, reviews); the volume of code activity. Each sits
inside the next. "How many developers took part" is participants;
contributors is the narrower alternative, named as such. Participants
will widen to any activity `[not yet in production: SM-3 participants =
any activity]` and the figure will jump; say which definition ran, from
`applied.definition`. *SM* "Reading results", "Inventory".

**Bots.** Governed contributor and activity figures exclude bots; an ad
hoc or generated-SQL figure includes them unless it says otherwise. *SM*
"Inventory" (contributors, contributions); *SL* "Worked recipes" 1.

**Unattributed and placeholder rows.** Activity with no resolved employer
sits in a NULL account row that often leads a ranking; learners with no
company sit in placeholder accounts. None of them is an organisation;
shares are computed on the attributed base and the unattributed share is
stated once. *SM* "Reading results", "Inventory" (training_enrollments,
certifications).

**Headcount vs volume; distinct counts vs rows.** A breakdown of distinct
people never sums to the folded figure; the folded figure comes from its
own call. Volumes add; people do not. *SM* "The switches, row by row".

**Maintainers: LF projects vs the whole index; roster vs account entity.**
The family counts maintainers of LF projects as of today; an ad hoc count
over the whole index reads higher. A company's maintainers through the
account entity at any depth `[not yet in production: DBT-2 account entity
on maintainers]` — until then the ad hoc reading reaches one hop.
*SM* "Inventory" (maintainers); *SL* "Worked recipes" 11.

**Maintainer contributions: roster as of the build, activity in the
window.** People on today's roster, their contributions over the window;
a person who was a maintainer then but not now is not counted. *SM*
"Inventory" (maintainer_contributions).

## Events and training

**Accepted speakers vs all proposals.** The family counts accepted
speakers, distinct people; an ad hoc count over every proposal status
reads higher. *SM* "Inventory" (speakers); *SL* "Routing".

**Registrations vs registrants vs checked-in.** Registrations are records;
registrants are distinct people by email; checked-in attendance exists
only for some registration sources, so zero attendees can mean no check-in
data. Windows are by event start date in the family and by registration
date if read ad hoc without choosing. *SM* "Inventory"
(event_registrations); *SL* "Routing".

**Sponsorship assets vs sponsoring companies.** The family counts
sponsorship assets and their price, all tiers, for events starting in the
window; one event can carry several assets for one company, and a
company's sponsorship sits on the account that bought it (a subsidiary's
row is separate from the parent's). *SM* "Inventory" (event_sponsorships).

**Platform training vs the published trained figure.** The training and
certification families cover the platform's own history and one branch
carries no account; lifetime headlines are published figures, cited as
such. By-account readings ad hoc keep zero rows the family omits. *SM*
"Inventory" (training_enrollments, certifications); *SL* "Routing".

## Health and value

**Health v2 vs the older text.** `applied.definition` says which health
average a call read; where a guidance sentence and the applied block
disagree, the applied block ran. Health and software value are daily
snapshots: the family pins one; an unfiltered ad hoc aggregate counts
each project once per day. Software value is each project's own latest
row, not one day. *SM* "Inventory" (project_health, software_value).

**LF-hosted vs the index population.** Health by population separates
LF-hosted projects from the wider index; a headline is LF-hosted unless
it says otherwise. *SM* "Inventory" (project_health).

## Meetings and rosters

**Attendances vs attendees vs invitees vs occurrences.** The interim
meeting recipe counts records (one invitee at one occurrence);
"attendees" as people is a distinct count on the same data; invitees are
a larger population than those who attended; the number of meetings is a
count of distinct occurrences, which the recipe does not expose — it is a
SQL-assistant reading over the same attendance data, as is the sum of
scheduled duration (stored per occurrence; summed over distinct
occurrences, never over attendance rows). Meeting-type buckets include a
literal "None" and a blank, which are two rows. Worded "attendances",
labelled interim; occurrences and hours labelled generated SQL
`[not yet in production: TOOLS-2 org meeting KPIs]`. *SL* "Worked
recipes" 12.

**Visible to you vs the warehouse.** Meeting and committee tools return
what the caller's identity may see; the warehouse holds what was loaded.
A count from the service tools is never an LF total. See
[service-tools.md](service-tools.md).

**Roster vs inference.** A board seat comes from the committee tools and
nowhere else; a company's seats are the roster filtered by organisation,
paginated to the end `[not yet in production: TOOLS-1
get_org_committee_seats]`. *SL* "Routing".

## Time

**Trailing twelve months vs calendar.** The default window is the prior
365 complete days; a calendar year is a choice. `applied.defaulted` says
when the dates were chosen for you; a deck states them as chosen. *SM*
"Defaults and the applied block".

**UTC days vs session-clock days.** Standard-metric dates are UTC
calendar days; ad hoc time filters cut at the session's day boundary, so
two readings of "last month" differ by a few hours of activity. State the
window; never claim an exact day across lanes. *SM* "Reading results";
*SL* "Windows".

**All time vs the sum of windows.** A window drops rows with no usable
timestamp, so an all-time figure can exceed its windows added up. *SM*
"Reading results".

**Partial periods and future-dated installs.** The last row of a to-date
series is partial and says so; memberships can be installed with a future
date, and an unbounded current-year count includes them. *SM* "Reading
results"; *SL* "Windows".

**Run date, not refresh date.** No lane reports when its tables were last
loaded; two runs a day apart can move. The run date stands for freshness
and a figure is re-run rather than reconciled against an earlier draft.
