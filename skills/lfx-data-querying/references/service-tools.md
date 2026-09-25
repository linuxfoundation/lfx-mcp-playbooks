<!-- Copyright The Linux Foundation and each contributor to LFX. -->
<!-- SPDX-License-Identifier: MIT -->

# The service tools — records, rosters, meetings, lists, actions

The service tools are not a data lane. They return **records** the
caller's identity may see (a project, a membership, a committee seat, a
meeting and who was in it, a mailing list) and they perform **actions**
(send an email, assign a Discord role, edit a committee). Their tool
descriptions own the parameters and filters. This reference is the craft:
what each tool is for in real work, how a record differs from a figure,
and the discipline that keeps a count of records honest.

## The rules that hold for every service tool

- **A record view is not a figure.** Records tell the story of one
  company, one committee, one meeting. A number counted from records is
  "what is visible to you" and is labelled so; it is never an LF total
  and never substitutes for a family or metric that holds the figure.
- **Count with the count tool; page only to read.** Count records with
  the count tool and read its complete flag. Page a search to the end
  when its rows are the answer; a page token means more rows, and an
  empty page can still carry one. A partial count is a lower bound.
  Meeting and participant records are large: ask for modest pages (a few
  dozen) and follow the token, rather than one page of a hundred that
  overflows the result and has to be read back from a file.
- **Identifiers come from this session.** A project, committee, meeting
  or organisation identifier is copied from a search result this session,
  never remembered from another; an appropriate readable membership or
  roster record can also supply an organisation identifier. Names used
  as filters come from that tool's own records, never a different vocabulary.
- **Vocabularies do not cross.** Record slugs, record organisation
  names, and free-text organisation fields on participants are their
  own vocabularies; they are not the warehouse's slugs or the CRM legal
  names, and they are not mixed into a figure read elsewhere (the
  `lfx-figure-checking` skill's why-figures-differ reference).
- **Actions are not data and are never implied.** Sending an email,
  assigning a role, creating or editing a committee or seat happen only on
  an explicit ask, confirmed, with the exact recipients or target read
  back; a data question never triggers one.
- **Read tools only, in a data workflow.** Create, update and delete tools
  exist beside the search tools; in querying and deck work they are not
  called.

## Projects — resolve, then navigate

- **Resolve a slug before any data call.** The typeahead search works
  well on product and project names ("Kubernetes", "PyTorch") and on the
  short foundation names and slugs ("cncf", "tlf"); a foundation's long
  legal name ranks poorly, so search by the short name or the slug and
  confirm the record; the search also takes an exact slug or an exact
  stored name, which returns the one record and no candidates.
- **Read the record, not just the slug.** A project record says whether
  it is a foundation, its legal entity type, its parent and its legal
  parent. A foundation record with a legal parent above it is a hosted
  foundation, not the umbrella. A project whose legal entity is a fund
  (the `-fund` sibling) holds the consortium's memberships.
- **The umbrella is not a scope.** The Linux Foundation's own record is
  one bucket; LF-wide work leaves the project unset everywhere.
- **The search is not a census.** Project records exist only for
  projects onboarded into LFX v2; the authoritative project directory is
  the semantic layer's, and it can hold more projects for a foundation or
  parent than the search returns. "How many projects does X have" is the
  layer's project-directory count; the search resolves names and slugs, and a
  count made from it says "projects indexed in LFX v2 and visible to your
  identity", is a lower bound when the tool says the count stopped early,
  and is never reconciled against the directory. The record tools stay
  exact for meetings, participants, committees and members, which are
  native to LFX v2: the count tool counts records of one kind in one
  call and says whether the count is complete; a count that is not
  complete is a lower bound and is said to be one; the project search's
  own total carries the same flag. Every count is "records indexed in
  LFX v2 and visible to you". Its filters are the fields the record
  carries: a member record knows its committee's category and its
  project, so seats across every board is one call. Committee members
  are scoped to a project by their project tag, never by a project
  parent, which they do not carry and which counts zero. A committee record
  knows its project but not the project's status, so an active-only
  figure is the count combined with the layer's project directory, and a
  filter on a field the record lacks comes back as zero, which is not an
  answer — never walk the index to get round it. A long window with no
  scope can time out: scope by project or committee and use month windows,
  check each record count is complete, and add only non-overlapping counts,
  never distinct people. What the tools count is what LFX Self Serve
  shows; the warehouse total over a period is the layer's.
- **Children of a foundation** come from the search's parent filter, and
  the entities under a legal parent from its legal-parent filter, each
  with the total and its flag. The legal-parent children of a foundation
  record are its legal entities; the projects of a JDF-type foundation
  hang off that entity, one hop lower, so resolve the entity record
  first and filter on it. The layer's foundation dimension is the
  population reading, not this index.

## Organisations — resolve, then read the membership records

- **The CRM legal name comes from `search_b2b_orgs`** when visible: use it
  for CRM-account readings, not as a replacement for the organisation
  spelling on a roster or participant record. Those searches use their own
  stored names. If organisation discovery is gated, readable membership or
  roster records can supply identifiers; say which source named them and
  which scope remains inaccessible.
- **`search_members` is the record view of a company's memberships**:
  every membership record for an organisation (by its identifier) or for
  a project, with status, tier, dates, the company name as the CRM spells
  it and the record's project slug. It answers "what does this company
  hold, on which projects, in which tiers, since when" — the story behind
  the figure. The figure itself (how many active memberships, their
  list-price value) is the memberships family, and the two are compared
  in words, never counted against each other.
- **`get_member_membership` and the key-contact tools** hold one
  membership's detail and its named contacts. The key-contact tools
  answer "who is the contact of record for this membership": the role,
  whether the contact is active, and the date the contact record was
  last updated, where one is returned; a contact record's board-member
  flag is the membership's own claim, not a seat. A contact flagged
  active is not proof the term is active: the flag is the contact
  record's, the term's status is the membership records'. A voting
  contact can sit on an earlier term of the same company, so the
  contact is reported as "contact of record on the <status> term" with
  its updated date, the seat with its recorded term date, if any, and
  neither as "current" nor
  "currently" (the plain-words reference, "Current, currently"). "Who
  holds the seat" is the committee roster (next section); the two are
  different people often enough that neither stands in for the other.
  The organisation seats tool returns the same contacts beside the
  seats, in one call under the organisation gate, paired per project
  with the seats that represent the company (next section); when no key
  contact is indexed for the company in scope its note says so, and the
  per-membership key-contact tool is the fallback. Contacts are people:
  presented only where naming individuals is appropriate, never as a
  list to be exported.

## Committees — rosters, seats, voting status

- **Find the committee by project and name.** A search scoped to a
  project with the committee's name ("Governing Board", "Technical
  Oversight Committee", "End User") returns the committee record with
  its category (Board, technical, other). An unfiltered search across a
  project returns every committee, election committees included, and
  runs to many pages.
- **The roster is `search_committee_members`, paginated to the end.**
  Each seat carries the person, their organisation as the roster stores it
  (name and identifier), the role, the voting status and how the seat
  was appointed, each as stored (the answer keeps the record's own
  wording), and its status. Only active seats are seats. A company's
  seats on one committee come from the roster search filtered on the
  organisation's stored name, the spelling copied from a roster record;
  a company's seats can split across spellings of its name, so it is
  one read per spelling the company appears under, and the full roster
  paginated and filtered on the identifier client-side is the
  cross-check. The filtered read is the primary because the search's
  roster-coverage note speaks to it (on an empty result it says whether
  nothing matched the filters) and because one filtered call is what a
  reader can re-run; the whole roster paginated and filtered client-side
  is the check, never the primary, and the committee and organisation
  filters together narrow ("Two filters narrow", below). A row is
  reported as stored, never dropped or re-attributed on an inference
  about the person (an e-mail domain, a personal address, a title); an
  odd row is shown with its oddity said, because the roster is the
  record and the reader's judgement belongs to the reader.
- **A company's seats across the LF** come from the organisation seats
  tool: every seat the company holds, split by committee category with a
  summary by category, by project, by role and by voting status, in one
  call. Asked for, the membership contacts of record come beside the
  seats — role and status as stored, the updated date where one is
  returned — with a per-project representation pairing the voting
  contacts with the seats that represent the company (next bullet).
  It sits behind the organisation gate: a refusal is the gate, never
  "no seats", and returns no contacts either. Fall back to the membership
  search and key-contact tools for contacts, and the roster search or
  count tool for seats, each "visible to you"; an empty side is a
  visibility limit, not an absence. Never infer one side from the other.
  A ranking of companies by seats is not this tool's job (the querying
  playbook's routing table).
- **Which seats represent the company.** A seat represents the company
  when its committee is of board category or its voting status is
  Voting Rep or Alternate Voting Rep on any committee — TOC/TSC seats
  and the member-class rosters filed under category Other included —
  never board seats alone, because a company whose vote sits on a
  technical or member-class committee is represented there, and a
  board-only cut drops it. Observer, Emeritus and None seats are seats,
  reported from the rows, not representation. The organisation seats
  tool's representation pairing applies this rule; a roster read by
  hand applies the same one.
- **Roster facts come from the committee tools, never from inference.** A board seat is never
  inferred from tier, sponsorship or activity. A roster answers "who
  holds the seat"; when the question is "who represents the company",
  the answer gives both records, each labelled: the seat holder, and
  the membership's contact of record (the key-contact tools, or the
  organisation seats tool's contacts beside the seats). When they name
  different people, both are shown side by side, never merged into one
  name. Dates as recorded: a contact carries its updated date; a roster
  row carries a role or voting term date only where recorded (an empty
  placeholder is no date). The organisation seats tool's rows carry none.
  A roster row's created and updated stamps date the LFX v2 record —
  mostly its onboarding — never the seat. Cite "term recorded as
  <start>–<end>" or "no term date recorded", never "current", "currently"
  or "member since". Say "listed as active on the roster at this read";
  a past recorded end beside an active status is reported as that oddity,
  not silently corrected. A contact flagged active is not proof the term
  is active (the organisations section above). Country is not
  a roster field; "from N countries" about a committee is not
  reproducible.
- **Coverage audit.** The coverage audit tool (`audit_committee_coverage`)
  takes a foundation (its root project) and covers it and its direct
  child projects, over the
  records visible to the caller: per project, the active memberships,
  the committees with their category and visible member count, the
  committees with no visible member, whether a board committee exists,
  and a gap, set only for projects with active memberships — no
  committee indexed, no board-category committee, or a board committee
  with no visible member. Its complete flag says when a count stopped
  early. When a roster comes back empty, the audit over its foundation
  is read before the empty result is interpreted, because it turns an
  empty read into a named case for the whole foundation in one call; it
  never turns one into "no seats": its own note says a
  zero can be an access effect or a roster not yet onboarded and never
  to report a project as having no seats from this result alone, and a
  program view over a foundation needs an identity with project-level
  audit rights. The answer's first sentence names the case the audit
  found, never "no seats" over a caveat (the querying playbook's
  section 5, item 11). For a person's or a company's seats the roster
  tools remain the read.
- **Two filters narrow.** Where a search takes two scoping filters
  (each tool's description says which), giving both returns the records
  that match both; a second filter never widens a result, so a count
  that grows when a filter is added was read from the wrong tool.

## Meetings — what happened, who was there

- **Past meetings by project and date range** (`search_past_meetings`)
  return each occurrence with its duration, sessions, visibility (public
  or restricted) and, when it belongs to a committee, the committee
  identifier. The list is what the caller may see: restricted meetings of
  committees the caller is not on do not appear, so a count of meetings or
  a sum of hours is "visible to you".
- **Meetings in a month from the meetings search** (`search_meetings`)
  are series and upcoming meetings listed by the series' start date, so
  "meetings in <month>" read from it is the series starting in the
  month, not the occurrences in it, and a weekly series that started
  earlier is absent: say so. "Scheduled this month" needs each series'
  own occurrences in the month, cancellations dropped, from the meeting
  records; "held this month" is the past-meetings search or the count
  tool over past meetings. The answer says which grain it counted,
  series or occurrences.
- **Participants of one occurrence** (`search_past_meeting_participants`)
  say who was invited and who attended, with a free-text organisation
  name and two flags saying whether that organisation is a member of the
  LF and of the project. The organisation name is typed by the organiser
  or the participant, not resolved to a CRM account: group by it only
  with that said.
- **Registrants of an upcoming meeting** (`search_meeting_registrants`)
  carry the organisation name and whether they were invited through a
  committee or directly.
- **Summaries** (`search_past_meeting_summaries`, `get_past_meeting_summary`)
  are generated text about one occurrence, useful for "what was
  discussed"; they are not attendance data.
- **People at a project's or a committee's past meetings over a period**
  come from the attended participants listing, which de-duplicates people
  by identity. Its record count and its count-only mode do not — they
  count index records, and more than one record can exist for one person
  at one occurrence, so a record count is neither attendances nor people.
  On the layer, attendances count one person at one occurrence and unique
  attendees count people. Without the layer, read all raw attended rows:
  distinct occurrence-and-person pairs give attendances; distinct
  occurrences give meetings attended. The listing's meeting count is the
  meetings expanded, not the meetings anyone attended. For a company,
  copy its exact stored organisation spelling from a participant record:
  case-sensitive, one spelling a call, no subsidiary roll-up, a miss is a
  silent zero. A date range needs a project or committee. Two populations hide in the committee filter: with a date range
  it resolves the committee's past meetings and returns everyone at
  them; without one it returns the participant records that carry the
  committee — say which ran. A project's or a committee's own meeting
  count over a period is the count tool, "visible to you"; the
  total over the warehouse is the layer's. They are two readings, never
  adjusted toward each other; the gap is explained by the
  `lfx-figure-checking` skill's index-versus-warehouse entry.
- **Aggregate meeting metrics** are the layer's named metrics, labelled
  ad hoc, with no per-caller visibility, and reach only callers with staff
  tools: occurrences and scheduled minutes by foundation, project or
  committee; attendances and people also by company through the account
  entity. Distinct meetings a company's people attended and those meetings'
  scheduled minutes have no named metric: the SQL assistant, generated SQL.
  A caller without the staff tools gets counts visible to them — the count
  tool over past meetings, the participants listing for people — one
  project or committee at a time. An LF-wide or company-wide total over a
  period is not available to them, and the answer says so. Never reconcile
  these caller-visible readings with warehouse totals.

## Mailing lists and Discord — communities as records

- **Mailing lists** (`search_mailing_lists` by name or project, then the
  members tool) return each list with its subscriber count as the list
  service reports it. A subscriber count is a list-service figure, quoted
  as such, not a warehouse metric; a company's subscribers are members of
  the list whose email domain or organisation field matches, paginated.
- **Discord** tools find users and roles and check or assign a role. They
  answer "does this person hold this role" and perform the assignment on
  an explicit ask; they are not a source of community size.

## Email — an action, never a lookup

- **Templates** list what can be sent; **`send_email`** sends. In a data
  or deck workflow neither is called. When a human asks for a send, the
  template, the recipients and the merge fields are read back and
  confirmed before the call, and the result reported as sent or failed.

## Saying it in the answer

- "Visible to you" on every count made from records, once per figure.
- The record vocabulary named when it differs from the warehouse ("the
  membership record lists the project under its own slug").
- A person named only where naming individuals is appropriate.
- Pagination stated only when it changes the reading ("all pages read";
  "first page only, so a lower bound").
