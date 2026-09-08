<!-- Copyright The Linux Foundation and each contributor to LFX. -->
<!-- SPDX-License-Identifier: MIT -->

# Plain words with two readings — the default, and the alternative to offer

An executive asks in everyday words: "organisations", "members",
"developers", "projects", "revenue", "attendees", "last year". On the LFX
tools most of those words have two or more readings, each a real figure
from a real tool. The discipline: **answer with the default reading, name
it in one clause, and offer the alternative in one sentence that says what
the difference is.** Never pick the reading that gives the bigger number,
never present two readings as a contradiction, never make the reader
guess which one they got. This file is the list: for each word, the
default reading and its tool, what else the word means and where, and
how the offer is phrased. Mechanisms behind each difference:
[why-figures-differ.md](why-figures-differ.md); scopes:
[axes.md](axes.md).

## Organisations, companies

- **Default:** legal organisations — CRM accounts as the standard metrics
  return them on every family (the account and its parent alongside), and
  as the membership records and `search_b2b_orgs` name them. "Top
  contributing companies" is contributions by organisation on these.
- **Also means:** the *enrichment* vocabulary — the employer the
  contribution data names for each contributor, inferred from public
  signals, far more granular, with variants and small employers the CRM
  never consolidated. It appears in exactly two places: the
  contributing-organisations count (a count only; the names are not
  listed; the organisation scope on that family is still by CRM account)
  and the employer-region grouping. On meeting and
  participant records the organisation is free text typed by people; on
  committee seats it is the roster's own field.
- **Offer it as:** "Counted as legal organisations known to the CRM,
  N contributed code. A broader reading — the employer the contribution
  data names for each contributor, which includes small employers and
  name variants — gives a larger count; say if you want that view." Never
  the two counts as one figure, never the enrichment count as
  "companies".

## Members, membership

- **Default:** memberships — project-account pairs with an active term,
  as of today, from the memberships family; "how many members does CNCF
  have" is answered as memberships in CNCF's programme, with the grain
  named.
- **Also means:** distinct member organisations (a company on three
  programmes counts once) — an organisation-grain reading no governed
  family gives today `[not yet in production: SM-3 member_organizations]`;
  the CRM's membership *records* for one company (`search_members`,
  "visible to you"); committee *members* (people on a roster); mailing-list
  *members* (subscribers); and in the warehouse's activity data a "member"
  is a person's contributor identity, not an organisation at all.
- **Offer it as:** "N memberships, counting each organisation once per
  programme it belongs to; the number of distinct organisations is a
  different reading and is not available as a governed figure today."

## Developers, contributors, participants, people active

- **Default:** "developers who took part" is participants — distinct
  people with a code contribution or a collaboration activity (issues,
  comments, reviews), bots excluded. "Contributors" is the narrower
  reading — distinct people with a code contribution.
- **Also means:** any activity at all `[not yet in production: SM-3
  participants = any activity; the figure jumps]`; maintainers (today's
  roster of LF projects); in the SQL assistant's data, "member_id" is a
  person.
- **Offer it as:** "N people took part, counting code and collaboration;
  M of them contributed code. Say if you want code contributors only, or
  the maintainer roster."

## Projects

- **Default:** the LF's project records, resolved by slug; on the activity
  families a slug covers the project and every project under it on the
  spine; on memberships a slug is that programme.
- **Also means:** the project records' own tree (parents and children as
  the project service stores them), which is not the warehouse spine
  (hosted foundations are their own spine roots); "project communities"
  in the annual reports (a published definition that has changed over the
  years); health-scored projects (LF-hosted vs the wider index);
  repositories.
- **Offer it as:** "CNCF and every project under it on the project spine"
  / "the umbrella's own programme" / "the annual report's count, cited".

## New members

- **Default:** new memberships — memberships sold as new business by
  install date, first-per-project (an organisation joining a second
  programme counts again; a returning account counts again).
- **Also means:** organisations new to the LF altogether — today an ad hoc
  reading on the organisation-grain first-membership dimension, counting
  first-ever membership rows (a same-day pair counts twice)
  `[not yet in production: SM-3 new_member_organizations]`; not the CRM's
  New Business flag.
- **Offer it as:** "N new project memberships; of those, roughly M were an
  organisation's first LF membership ever — an ad hoc reading that counts
  first memberships, not organisations."

## Revenue, dues, value

- **Default:** list-price value of active memberships (the memberships
  family), "list price, not dues billed", never divided by the count.
- **Also means:** dues actually billed (a finance figure the tools do not
  hold); sponsorship revenue (asset price, events family); software value
  (a cost-model estimate per project, software-value family).
- **Offer it as:** "worth N at list price; billed dues are a finance
  figure outside these tools; sponsorship and training revenue are
  separate figures."

## Attendees, registrations, reach

- **Default:** for events, accepted registrations (records), with distinct
  registrants (people by e-mail) and checked-in attendees (only where the
  source carries check-in) as the two other columns of the same family.
  For meetings, attendances (one invitee at one occurrence) from the
  interim recipe.
- **Also means:** distinct people across meetings; invitees; "reach" in
  the annual reports (published) and social reach (author followers per
  mention, not additive across projects).
- **Offer it as:** "N registrations from M people; check-in data exists
  only for some sources, so attendance is a floor" / "N attendances, not N
  people".

## Events, meetings

- **Default:** events are conferences and similar with registrations,
  sponsorships and speakers (the event families, by event start date);
  meetings are the LF's meeting platform's occurrences (meeting tools and
  the interim recipe; occurrences and hours from the SQL assistant).
- **Also means:** the everyday "event" that is really a meeting or a
  webinar; sponsorship "events" (the same events, from the sponsorship
  side).
- **Offer it as:** name which — "LF events with registrations" or
  "meetings run through the LF platform".

## Speakers

- **Default:** accepted speakers, distinct people, no organisation scope
  today `[not yet in production: SM-3 speakers by organisation]`.
- **Also means:** every proposal status, read ad hoc (larger).
- **Offer it as:** "N accepted speakers; proposals in review or rejected
  are not counted."

## Maintainers

- **Default:** today's roster of maintainers of LF projects, distinct
  people.
- **Also means:** the whole maintainers index (higher, includes non-LF
  projects); maintainers as of a past period (the family's period
  reading); maintainer *contributions* (their activity in a window).
- **Offer it as:** "N maintainers on LF projects as of today."

## Health, healthy projects

- **Default:** LF-hosted projects with a v2 health score on the latest
  snapshot, in the stored bands.
- **Also means:** the wider index population; an average across days (a
  snapshot error, not a reading).
- **Offer it as:** "N LF-hosted projects scored; the wider index is a
  separate population."

## Country, region

- **Default:** for memberships, the member account's billing country,
  conformed, with an unresolved group; for contributors and contributions,
  the person's own country, known for a minority; for organisation
  region, the employer's headquarters. The LF region grouping is
  provisional.
- **Also means:** where the work happens; where a subsidiary sits; "APAC"
  in the everyday sense, which is several stored rows.
- **Offer it as:** "countries of the billing address, N resolved plus an
  unresolved group" / "the person's own country where known".

## Last twelve months, this year, last year

- **Default:** the trailing twelve months to today, as dates, on activity,
  event, training and social families; all history on membership movement
  families; "as of today" on state families.
- **Also means:** a calendar year; year-to-date bounded at today; "same
  point last year"; a past-date membership reading (date-based).
- **Offer it as:** "the twelve months to <date>; say if you want calendar
  <year> or year-to-date."

## The Linux Foundation

- **Default:** LF-wide — no project filter, every programme and project.
- **Also means:** the umbrella's own slug — one membership programme and
  one activity bucket, not the LF as a whole; the LF as a legal entity.
- **Offer it as:** "across the LF as a whole" / "the Linux Foundation's own
  membership programme only".

## Top contributors

- **Default:** people, ranked by contribution volume by identity, shown
  only where naming individuals suits the audience; otherwise
  organisations by volume.
- **Also means:** organisations by headcount (how many people), which
  ranks differently from volume (how much work).
- **Offer it as:** "ranked by volume of code contributions; by number of
  people the order differs."

## Training, learners, certified

- **Default:** platform enrollments (records) and enrolled users (people)
  by enrollment date; certifications completed; placeholder accounts for
  unaffiliated learners reported as unattributed.
- **Also means:** the official lifetime "trained" headline (published).
- **Offer it as:** "N enrollments from M people on the platform; the
  lifetime figure is the published one, cited."

## Sponsors

- **Default:** sponsorship assets and their price, all tiers, for events
  starting in the window, by organisation (one event can carry several
  assets for one company; a subsidiary's row is separate).
- **Also means:** distinct sponsoring organisations (count the rows'
  organisations, say so); a tier name (stored per event).
- **Offer it as:** "N sponsorships worth X, from M organisations."

## Committees, boards

- **Default:** the roster of the named committee (board category for
  governing boards), active seats, with voting status; "visible to you".
- **Also means:** every committee of a project including election
  committees ("Other" category); technical bodies.
- **Offer it as:** "the governing board's roster as visible to you, N
  active seats".

## Subsidiaries, "the company"

- **Default:** the named legal account alone.
- **Also means:** the company including subsidiaries at any depth
  (combined), or broken down (separate).
- **Offer it as:** "the IBM account alone; including Red Hat and the
  other subsidiaries the figure is Y — say which view you want on every
  slide."

## The sentence pattern

"<figure>, counting <default reading in plain words>. <One sentence:
the alternative reading, what it counts instead, and that it is
available on request or not yet.>" Once per figure, never a lecture; the
provenance block carries the tool words.
