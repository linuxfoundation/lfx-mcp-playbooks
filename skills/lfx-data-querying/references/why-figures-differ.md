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
day differ where statuses lag term dates — mostly free memberships with
an open-ended placeholder end date whose status has lapsed, so the
date-based reading of today runs above today's own figure. A deck uses
one kind per section and says "as of <date>, date-based" when it is not
today.
*SM* "Reading results", "Inventory" (memberships).

**Memberships (pairs) vs member organisations.** The family counts
project-account pairs: a company on three projects counts three times.
"How many members" in the everyday sense is distinct organisations, the
member-organisations family (paying-only: its paying sibling), a
different figure from memberships; report the one the question means,
say the grain, and never pull membership rows and count them. *SM*
"Inventory" (memberships, member_organizations).

**Tier rows vs the total.** A pair holding two active terms in two tiers
sits in both tier rows and once in the total, so tier rows sum at or
above the total while the list-price value sums exactly. It is a second
term, not a label defect: say "pairs holding two tiers", and let the CRM
owner judge whether a same-day pair of identical products is one. *SM*
"Inventory" (memberships).

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

**New memberships vs new organisations vs churn vs lost.** New
memberships are New Business installs at the install grain (a project,
an organisation, a day): a second project counts again, a returning
account counts again, and the yearly rows add up to the span. "New to
the LF" is the new-member-organisations family, which counts arrivals:
a term starting while the organisation held no membership anywhere in
the LF the day before, so an organisation that lapsed and came back
counts as new again, the way the CRM re-flags New Business; the level of
arrival follows the project switch (the LF with no project, the
foundation for a root, the project with excluded) and is named in the
applied block. First-ever is a separate reading, the layer's
first-membership dimension on the membership rows, reported as ad hoc and
as memberships, never headed "new organisations". Churned memberships
are pairs that ended; a company that dropped one project and kept
another churned but is not lost — lost organisations are departures: a
paid term that ended with no other term of the organisation covering the
next day, judged on that day, so a later return does not undo it, and a
free term's lapse is not a departure. The churn date is the day after
the term ends, so a year-end churn lands in the next year. As series,
new memberships, arrivals, churned memberships and departures each add
up across years. `[not yet in production: DBT-2c on the standard-metric families — until then: the new-organisations family's definition sentence still says first membership while its rows count arrivals, and the lost-organisations family still excludes organisations that have since returned; the layer's metrics carry the new meanings, so say which path ran]` *SM* "Inventory" (new_members,
membership_churn, lost_member_organizations); *SL* "Value discovery"
(read the dimension's own description before filtering on it).

**Roll-forward residues.** Start plus new minus churned never equals the
end count, because the four are four populations. Memberships: the start
snapshot is 31 December of the prior year — a term ending that day is
inside the start count and churns on 1 January, and a 1 January install
is inside a 1 January start count and new, so a 1 January start counts
both twice; churn is priced, the headcount is not, so a free or
quasi-associate lapse leaves the count without churning; a lapse with a
later return is never churn at all (churn requires no later membership,
which is why past years shrink between builds); new is new business only,
so a re-activation sold as a renewal enters the end count without being
new, while a second new-business sale to an already active pair is new
without adding a member; and a pair that drops one product while keeping
another churns and stays. Organisations: start plus arrivals minus
departures reaches the end up to the free-term residual — a lapse with
no price is not a departure, so an organisation whose only term at year
end was free leaves the headcount without being lost, and one holding a
free term while its paid one ended is lost while the headcount keeps
it. Name the mechanism and the side it falls on; a gap no mechanism
covers is a scope or date error. `[not yet in production: DBT-2c on the standard-metric families — until then: the new-organisations family's definition sentence still says first membership while its rows count arrivals, and the lost-organisations family still excludes organisations that have since returned; the layer's metrics carry the new meanings, so say which path ran]` *SM* "Inventory" (memberships,
new_members, membership_churn, member_organizations,
new_member_organizations, lost_member_organizations).

**Billing country vs conformed country.** The raw billing country is free
text; the conformed country entity normalises it and files what it cannot
resolve under NULL. A country breakdown read raw has more rows — one per
spelling, so a raw count of countries is always higher, never lower — and
different totals per country than the conformed one; the blank row is
accounts with no billing country, and the conformation drops nothing.
Say "countries" only of the conformed reading. The LF region grouping is
provisional. *SM* "Inventory" (memberships, contributors);
*SL* "Value discovery".

## Projects and scope

**Foundation slug vs the foundation's own bucket.** A foundation's slug on
the plain project column matches only its catch-all bucket; the foundation
dimension matches the foundation and its projects. An order of magnitude
apart on activity, with no error. *SL* "Scope"; *SM* "Projects and
subprojects".

**Whole tree vs one level vs one hop.** The standard metrics walk a
project's tree and a company's subsidiaries to any depth. The semantic
layer offers both reaches side by side, and the dimension chosen decides
the figure: on the account entity the roll-up name folds one hop (the
direct parent) while the top-parent name and the account path fold the
whole group; on projects the foundation dimension reaches a foundation
completely, the plain slug one node, the project path the subtree. A
company figure read on the one-hop roll-up is smaller than the same
figure on the top parent by every deeper subsidiary, and a top-parent
figure matches the family's "including subsidiaries" reading only when
the same root was resolved (two roots can share a display name; the
identifier is the exact key). *SL* "Scope" (REACH).

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
combined figure is the consortium: on the membership and organisation
families the default combined reading is the whole consortium in one
call, its members listed in the applied block; excluded is the named
project alone; other families never merge one. *SM* "Projects and
subprojects" (Consortia).

**Twin slugs.** Some project families exist under two slugs; a low total
is a reason to group by slug before concluding. *SL* "Scope".

**Attachment level.** Memberships, registrations and sponsorships attach
at foundation level; a leaf project's own reading is legitimately
near-empty. Enrollments and maintainers attach below the foundation too.
And on memberships a foundation's slug is one programme, not a subtree:
a hosted foundation's memberships sit on its own slug, so a reading on
the umbrella's slug neither includes nor "excludes" them — they were
never in scope. *SL* "Scope"; *SM* "Projects and subprojects".

## People and activity

**Contributors vs participants vs contributions.** People with a code
contribution; people with a code contribution or a collaboration
(issues, comments, reviews); the volume of code activity. Each sits
inside the next. "How many developers took part" is participants — any
non-bot activity, stars, forks, meetings and training included — and
contributors is the narrower alternative, named as such; say which
definition ran, from the definition sentence the result carries. *SM*
"Reading results", "Inventory".

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

**Maintainers: LF projects vs the whole index; account alone vs group.**
The family counts maintainers of LF projects as of today; an ad hoc count
over the whole index reads higher. A company's maintainers including
subsidiaries at any depth: the family's subsidiaries switch, or ad hoc
through the layer's top-parent dimension on maintainers (two roots can
share a name; the identifier is the exact key). Affiliation is carried
per person, so the by-organisation rows partition the total exactly,
the unresolved-employer row usually the largest single row; the
by-project rows sum above it, a person maintaining several projects; a
maintainer figure that equals the sum of the project rows is seats, not
people.
*SM* "Inventory" (maintainers); *SL* "Worked recipes" 11.

**Maintainer contributions: roster as of the build, activity in the
window.** People on the roster, their contributions over the window; a
person who was a maintainer then but not now is not counted. Two
readings of "maintainers active in the window" exist and differ by a few
people either way: the maintainer-contributions family reads a flag
stamped on each activity when the activities data was last built, so its
roster is as of that build; the maintainers family with a period joins
today's roster live. Quote the maintainer-contributions reading, say it
reflects the roster as of the last activities build, and treat the other
as the cross-check: the difference is roster changes since that build,
not an error. *SM* "Inventory" (maintainer_contributions, maintainers).

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

**Scored vs unscored rows.** The daily health fact holds rows with a v2
score and rows without one, in comparable numbers; the family reads the
scored ones. An ad hoc count over the fact without bounding to the
scored population reads far higher, and an ad hoc average over it is
defined only on the scored rows. The layer exposes the scored population
as a dimension on the daily health metrics; the current-state metrics
carry no such switch because they are already anchored on a score — and
they read each project's own latest day over the whole index unless
filtered to LF-hosted projects, a different population from the family's
pinned day, never "LF project health" without the filter; the family
itself has no unpinned reading and says so. A project without a score is
reported as unscored, with the coverage sentence the result carries; the
answer never supplies a reason the data does not carry. *SL* "Worked
recipes" 8.

## Meetings and rosters

**Attendances vs attendees vs invitees vs occurrences.** The layer
holds four meeting readings on two models. Occurrences count distinct
meetings held, with or without attendance as a dimension; scheduled
minutes sum the stored duration once per occurrence, never per
attendance row, and are scheduled, not time spent; attendees count
distinct people (an LF user, e-mail as the fallback, never invitee ids);
attendances count records, one person at one occurrence, and are the
reading that carries the organisation, the committee and the meeting
type. Invitees are a larger population than those who attended, and the
attendance rate is attendances over invitations on the same slice —
walk-ins can push it above one. An occurrence shared by several projects
is attributed to one of them. The layer has no per-caller visibility;
the meeting tools have — cite which. The attendance data is the census; the attended-meeting rows of the activity
data are the subset that reached the contributor platform, keyed on
meeting series and person, so their "meetings" are series-person pairs
and their people are resolved contributor identities — right for a
contributor-style question, never for meetings held. The attendance data
carries the invitee's CRM account only; the enriched employer field
exists on the activity rows, so an attributable share reads lower on the
attendance data than on the activity data. Meeting-type buckets include a
literal "None" and a blank, which are two rows. Records worded
"attendances"; the named metrics labelled ad hoc (if explore does not offer them, the SQL assistant over the attendance data gives occurrences and scheduled minutes, the attendance recipe attendances). *SL* "Worked
recipes" 12.

**Potential impressions vs potential audience.** The reach family sums
author follower counts over the mentions, so an account that posts many
times counts its followers each time, and a handful of prolific
high-follower accounts make up most of the total; follower counts exist
for one network only, and the others add nothing. A de-duplicated reading
(each author's followers once) is an order of magnitude smaller and is
not on the layer. A reach figure labelled "authors de-duplicated" that
sits near the family's figure was the per-mention sum under the wrong
label. *SM* "Inventory" (social_reach).

**Indexed in LFX v2 vs the warehouse.** The record tools and the count
tool read the LFX v2 index: records of projects onboarded into LFX v2,
filtered to what the caller's identity may see, with no project status
on committees or meetings. The warehouse reads every project it was
loaded with, at a project status and a date. So the same population —
boards across the LF, their seats, a foundation's projects, meetings in
a window — comes out different from each side, by onboarding,
visibility, status and timing, and neither figure is an error. An
LF-wide figure is the warehouse reading, said as such; the index count
is "in LFX v2 today, visible to you", and is what LFX v2 applications
show their users. Quote one, and name the other only as a cross-check.
See [service-tools.md](service-tools.md).

**Roster vs inference.** A board seat comes from the committee tools and
nowhere else; a company's seats are the roster filtered by organisation,
paginated to the end. A ranking of organisations by seats across every
project is a different job: walking every roster through the tools is a
hundred calls, so it is a generated-SQL reading over the committee data,
labelled as such, with LF staff seats and unaffiliated individuals set
aside and said, technical steering committees kept out of "boards", and
spelling variants of one company noted rather than merged by hand. One
company's seats are the organisation seats tool, "visible to you", under
the organisation gate. *SL* "Routing".

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
