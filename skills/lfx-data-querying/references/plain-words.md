<!-- Copyright The Linux Foundation and each contributor to LFX. -->
<!-- SPDX-License-Identifier: MIT -->

# Plain words with two readings — what the families count, and the alternative to offer

An executive asks in everyday words: "organisations", "members",
"developers", "projects", "revenue", "attendees", "last year". On the
standard metrics most of those words have a default family whose
`applied.definition` sentence says exactly what was counted, and one or
more other readings — another family, a switch or grouping on the same
family, or a semantic-layer metric — that a reader may have meant. The
discipline: **answer with the default family, repeat its definition in
the reader's words, and offer the alternative in one sentence that says
what the difference is.** Never the reading with the bigger number by
preference; never two readings as a contradiction; never a figure whose
population the reader has to guess. Each entry below was checked against
the family's own definition sentence on the production tools on the day
this file was written; the sentence in the applied block is the one to
repeat, not this file's paraphrase, when they differ. Mechanisms:
[why-figures-differ.md](why-figures-differ.md); scopes:
[axes.md](axes.md).

## Organisations, companies

- **Default family reading:** legal organisations — CRM accounts. Every
  family's organisation grouping and organisation scope work on these,
  activity families included, and each row carries the account and its
  parent. "Top contributing companies" is contributions by organisation.
- **Other readings:** the contributing-organisations family counts *the
  employer the contribution data names* — the enrichment vocabulary,
  more granular, small employers and name variants included — and gives
  a count only, never the names; the same vocabulary drives the
  employer-region grouping. Meeting and participant records carry a
  free-text organisation; committee seats carry the roster's field.
- **Offer it as:** "Counted as legal organisations known to the CRM, N
  contributed code. A broader reading — the employer the contribution
  data names for each contributor, which includes small employers and
  name variants — gives a larger count; say if you want that view."
  Never the two counts as one figure; never the enrichment count as
  "companies".

## Members, membership

- **Default family reading:** memberships — "distinct project-account
  pairs with an active term, status-based" as of today. "How many members
  does CNCF have" is memberships in CNCF's programme, grain named.
- **Other readings:** distinct member organisations (a company on three
  programmes counts once) — the member-organisations family, and its
  paying-only sibling; a past-date or
  series reading is date-based, not status-based, and says "as of
  <date>" (read on today's date it runs above today's own figure: free
  memberships with an open-ended end date whose status has lapsed); the CRM's membership *records* for one company
  (`search_members`, "visible to you"); committee *members* (people);
  mailing-list *members* (subscribers); and in the activity data a
  "member" is a person's contributor identity.
- **Offer it as:** "N distinct member organisations" when the question is
  how many members; "N memberships, counting each organisation once per
  programme it belongs to" when it is memberships — and the other reading
  offered beside it.

## Developers, contributors, participants, people active

- **Default family reading:** "developers who took part" is the
  participants family — "distinct non-bot people with any activity in the
  window: code, issues, reviews, comments, stars, forks, meeting
  invitations and attendance, training and exams, Hacker News; the
  broadest people count". "Contributors" is the contributors family —
  distinct code contributors, bots excluded.
- **Other readings:** the layer's code-or-collaboration count (issues,
  comments and reviews beside code; no stars, forks or meetings), a
  middle figure between contributors and participants, said so; the
  maintainer roster; the metric whose name says "first-time contributors"
  on the layer, which counts any activity type and is not a subset of
  contributors.
- **Offer it as:** "N people took part, counting code and collaboration;
  M of them contributed code. Say if you want code contributors only, the
  maintainer roster, or everyone with any activity at all."

## Projects

- **Default family reading:** a slug resolved from the project records;
  on the activity families it covers "<slug> and every project under it
  on the project spine, folded"; on memberships it is that programme
  plus what the spine maps under it (next to nothing for the umbrella).
- **"How many projects does X have":** no family answers it; the
  semantic layer's `pcc_project_count` does — the project directory, the
  catalogue people mean by "projects". A foundation's tree is the
  foundation dimension; direct children are a grouping by the parent
  project slug; the project depth and path dimensions give level and
  path. The layer's other count, `project_count`, counts
  community-analytics segments — a different population, for questions
  explicitly about tracked segments, and a different number for the same
  X is population, not error. The project search tool and any count built
  on it cover only the projects onboarded into LFX v2 and visible to the
  caller — they can be lower, so a service-tool project count is never
  "all projects of X" and is never reconciled against the directory; the
  tools resolve names and slugs, the layer gives the number.
- **Other readings:** the project records' own tree (parents and
  children as the project service stores them — hosted foundations are
  the umbrella's children there but their own roots on the spine);
  "project communities" in the annual reports (published, definition has
  changed); health-scored projects (LF-hosted vs the wider index);
  repositories.
- **Offer it as:** "N projects in the directory under CNCF" / "CNCF and
  every project under it on the project spine" / "the umbrella's own
  programme" / "the annual report's count, cited".

## New members

- **Default family reading:** new memberships — "memberships from a New
  Business opportunity, by install date", one per project, organisation
  and install day (a second programme counts again; a returning account
  counts again); as a series, the current year is partial and flagged,
  and the years add up to the span.
- **Other readings:** organisations new to the LF — the
  new-member-organisations family counts arrivals (no membership anywhere
  in the LF the day before; a lapsed account that rejoins counts again),
  at the LF, the foundation or the project as the applied block says;
  first-ever memberships, the layer's first-membership dimension on the
  membership rows (ad hoc; a same-day pair of installs counts twice, so
  never headed "organisations"); churned memberships (ended with no subsequent membership, non-zero
  revenue, by the day after the term ended); lost organisations, paid
  departures judged on the day. `[not yet in production: DBT-2c on the standard-metric families — until then: the new-organisations family's definition sentence still says first membership while its rows count arrivals, and the lost-organisations family still excludes organisations that have since returned; the layer's metrics carry the new meanings, so say which path ran]`
- **Offer it as:** "N new project memberships from M organisations
  arriving at the LF, returners included; of those, roughly K were here
  for the first time ever — an ad hoc reading that counts first
  memberships, not organisations."

## Revenue, dues, value

- **Default family reading:** the memberships family's value — "revenue
  is list price, not dues billed"; never divided by the count.
- **Other readings:** invoice and discount amounts on memberships exist
  as semantic-layer metrics (ad hoc); sponsorship revenue is "the asset
  price in USD" on the sponsorships family; software value is "COCOMO
  software value summed over each LF-hosted project's own latest snapshot
  row", additive across projects, never across days.
- **Offer it as:** "worth N at list price; billed dues are a separate
  reading; sponsorship and training revenue are separate figures."

## Attendees, registrations, reach

- **Default family reading:** for events, the registrations family —
  "accepted registrations of events starting in the window; registrants
  and attendees are distinct people by email, Bevy speaker rows
  excluded": three columns, registrations (records), unique registrants
  (people), checked-in attendees (people, only where the source carries
  check-in, so zero can mean no data). For meetings, attendees are the
  layer's distinct-people metric and attendances its records (one
  person at one occurrence).
- **Other readings:** distinct people across meetings; invitees; "reach"
  in the annual reports (published); social reach ("author follower
  counts over the mentions: the sum is a potential-reach proxy", not
  additive across projects). Three "attend" readings exist on the layer:
  meeting attendances (records), meeting attendees (people) and event
  attendees (people) — name which.
- **Offer it as:** "N registrations from M people; check-in exists only
  for some sources, so attendance is a floor" / "N attendances, not N
  people".

## Events, meetings

- **Default family reading:** events are conferences and similar with
  registrations, sponsorships and speakers — the event families, windowed
  by event start date. Meetings are the LF platform's occurrences: the
  layer's meeting metrics for how many, how many scheduled minutes and
  who came over a period, the meeting tools for lists (if explore does not offer them, the SQL assistant over the attendance data gives occurrences and scheduled minutes, the attendance recipe attendances).
- **Other readings:** an "event" that is really a meeting or a webinar;
  sponsorship "events" (the same events from the sponsorship side; one
  event can carry several sponsorship assets).
- **Offer it as:** name which — "LF events with registrations" or
  "meetings run through the LF platform".

## Speakers

- **Default family reading:** "accepted speakers of events starting in
  the window: distinct people whose speaker status is Accepted"; by
  organisation is the speaker's account as resolved from the proposal,
  with a large unresolved row.
- **Other readings:** every proposal status (a semantic-layer or
  generated-SQL reading; about three times larger).
- **Offer it as:** "N accepted speakers; proposals in review or rejected
  are not counted."

## Maintainers

- **Default family reading:** "today's roster: active maintainers (no end
  date) on LF projects", distinct people.
- **Other readings:** the whole maintainers index (includes non-LF
  projects; higher); maintainers as of a past period (the family's period
  reading); maintainers by company including subsidiaries at any depth —
  the family's subsidiaries switch, or ad hoc through the layer's
  top-parent dimension on maintainers (two roots can share a name, so the
  identifier is the exact key); maintainer contributions — "code
  contributions by people on today's maintainer roster of the segment",
  with a distinct contributing-maintainers count beside the volume (the
  roster as of the last activities build; the maintainers family's period
  reading uses today's roster and differs by a few people).
- **Offer it as:** "N maintainers on LF projects as of today."

## Health, healthy projects

- **Default family reading:** "projects with a v2 health score on the
  latest daily snapshot on or before end_date, and their mean health
  score; LF-hosted projects; the average … normalized to a hundred-point
  scale"; bands are the stored names (Excellent, Healthy, Fair,
  Concerning, Critical), and the applied coverage says how many LF-hosted
  projects carry a score that day.
- **Other readings:** the wider index population (by population); any
  home-made threshold on the raw score over every project in the index —
  an order of magnitude away from the family's Healthy band; an average
  across days (a snapshot error). An ad hoc reading on the daily health
  fact is bounded to the rows carrying a v2 score — the layer exposes
  that population as a dimension on the daily health metrics — because
  the unscored rows are a population of their own, roughly as large, and
  carry no score; the current-state metrics are already anchored on it
  and read each project's own latest day over the whole index unless
  filtered to LF-hosted projects — a different population from the pinned
  day, never "LF project health" without the filter; the family points
  there for "current" and has no unpinned reading of its own. An unscored
  project is reported as unscored with the coverage the result gives,
  never with a reason of your own.
- **Offer it as:** "N LF-hosted projects scored, M in the Healthy band as
  the score defines it; the wider index is a separate population."

## Country, region

- **Default family reading:** for memberships, the member account's
  billing country, conformed, with an unresolved row ("accounts with no
  billing country or a spelling the lens does not resolve"); for
  contributors and contributions, the person's own country, known for a
  minority; for organisation region, the employer's headquarters. The LF
  region grouping is provisional.
- **Other readings:** the raw billing field (more rows, unconformed);
  where the work happens; for contributors, the employer-headquarters
  lens (organisation region), which can invert the ranking the person
  lens gives and covers a different share of the work — offer it beside;
  "APAC" in the everyday sense, which is several stored rows.
- **Offer it as:** "countries of the billing address, N resolved plus an
  unresolved group" / "the person's own country where known".

## Last twelve months, this year, last year

- **Default family reading:** window families read the trailing twelve
  months to today as UTC dates on the activity, event, training and
  social families, and all history on the membership movement families
  (new, churned); state families read "as of today", status-based.
- **Other readings:** a calendar year (dates); year-to-date bounded at
  today; "same point last year"; a past-date membership reading
  (date-based, says so); "since tracking began" is the first month with
  data, read at month grain — a year bucket is not a start date.
- **Offer it as:** "the twelve months to <date>; say if you want calendar
  <year> or year-to-date."

## The Linux Foundation

- **Default family reading:** LF-wide — no project set, every programme
  and project.
- **Other readings:** the umbrella's own slug — its own membership
  programme and its own activity bucket, not the LF as a whole; the LF as
  a legal entity.
- **Offer it as:** "across the LF as a whole" / "the Linux Foundation's own
  membership programme only".

## Top contributors

- **Default family reading:** contributions by contributor — people
  ranked by volume by identity (handle; two identities can share a
  display name), shown only where naming individuals suits the audience;
  otherwise contributions by organisation.
- **Other readings:** organisations by headcount (contributors by
  organisation), which ranks differently from volume.
- **Offer it as:** "ranked by volume of code contributions; by number of
  people the order differs."

## Training, learners, certified

- **Default family reading:** enrollments — "distinct enrollments (TI +
  edX platform data) by enrollment time; the edX branch carries no
  account" — with enrolled users (people) beside them; certifications —
  "enrollments that resulted in a completed certification, by enrollment
  time". Placeholder accounts for unaffiliated learners are unattributed.
- **Other readings:** the official lifetime "trained" headline
  (published); a product-type filter on the layer (a nearby but different
  population).
- **Offer it as:** "N enrollments from M people on the platform; the
  lifetime figure is the published one, cited."

## Sponsors

- **Default family reading:** "sponsorship assets of events starting in
  the window, all tier types; revenue is the asset price in USD", by
  organisation (one event can carry several assets for one company; a
  subsidiary's row is separate).
- **Other readings:** distinct sponsoring organisations (count the rows'
  organisations, say so); a tier name (stored per event).
- **Offer it as:** "N sponsorships worth X, from M organisations."

## Social mentions, reach

- **Default family reading:** mentions — "social listening mentions by
  mention time; one mention is one source id" — with distinct authors and
  positive/negative counts beside them (neutral is in neither); reach —
  the sum and average of author followers over the mentions.
- **Other readings:** a portfolio total across projects (not additive: a
  prolific author counts once per mention, and a project can sit inside
  another's mention set); a de-duplicated follower total (each author's
  followers counted once), far smaller, which no family or layer metric
  holds today.
- **Offer it as:** "N mentions from M authors; reach is potential
  impressions, follower counts summed per mention, not added across
  projects." Never "audience" or "people reached": follower counts exist
  for one network only, and every post by a high-follower account adds
  that account's followers again.

## Committees, boards

- **Default reading (record tools):** the roster of the named committee
  (board category for governing boards), active seats, with voting
  status; "visible to you".
- **Other readings:** every committee of a project including election
  committees ("Other"); technical bodies; a ranking of organisations by
  seats across all projects, which is a generated-SQL reading over the
  committee data (the why-figures-differ "Roster vs inference" entry),
  not a roster walk.
- **Offer it as:** "the governing board's roster as visible to you, N
  active seats".

## Subsidiaries, "the company"

- **Default family reading:** the named legal account alone (the
  organisation switch defaults to excluded).
- **Other readings:** the company including subsidiaries at any depth
  (combined), or broken down (separate).
- **Offer it as:** "the IBM account alone; including Red Hat and the
  other subsidiaries the figure is Y — say which view you want on every
  slide."

## The sentence pattern

"<figure>, counting <the family's definition in plain words>. <One
sentence: the alternative reading, what it counts instead, and whether it
is governed, ad hoc, or not yet available.>" Once per figure; the
provenance block carries the tool's words.

## The SQL assistant as the fallback lane

The generated-SQL lane covers the shapes and domains the families and
the layer do not, and it interprets everyday words on its own. Observed
on the production tools on the day this file was written: asked for a *count* of organisations it
took the inferred-employer vocabulary and dropped the unaffiliated group,
asked for a *ranking* it took CRM accounts; "developers who took part"
became everyone with any activity row; "countries" the raw billing field;
"speakers" every proposal status; "healthy projects" a home-made
threshold over the whole index; "contributors" it refused and routed to
the governed lane; "members", "new members", "membership revenue" and
"maintainers" matched the families. So it is never the first lane for an
everyday word; where it is the lane that covers the shape (meeting
occurrences and hours, cross-domain joins, a hierarchy walk no family
expresses), its population line and its SQL are read before the figure
is repeated, and the provenance says "no governed reading for this shape
today".
