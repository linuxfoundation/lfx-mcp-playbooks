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
- **Paginate to the end before counting anything.** A page token means
  more; an empty page can still carry a token; stop only when no token
  comes back. A count made from the first page is a guess.
  Meeting and participant records are large: ask for modest pages (a few
  dozen) and follow the token, rather than one page of a hundred that
  overflows the result and has to be read back from a file.
- **Identifiers come from this session.** A project, committee, meeting
  or organisation identifier is copied from a search result this session,
  never remembered from another. A name resolves to an identifier before
  it goes into any other call.
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
  project, so seats across every board is one call; a committee record
  knows its project but not the project's status, so an active-only
  figure is the count combined with the layer's project directory, and a
  filter on a field the record lacks comes back as zero, which is not an
  answer — never walk the index to get round it. A long window with no
  scope times out today: split it into a few sub-ranges, check each is
  complete, and add them. What the tools count is what LFX Self Serve
  shows; the warehouse total over a period is the layer's.
- **Children of a foundation** come from the search's parent filter, and
  the entities under a legal parent from its legal-parent filter, each
  with the total and its flag. The legal-parent children of a foundation
  record are its legal entities; the projects of a JDF-type foundation
  hang off that entity, one hop lower, so resolve the entity record
  first and filter on it. The layer's foundation dimension is the
  population reading, not this index.

## Organisations — resolve, then read the membership records

- **The legal name comes from `search_b2b_orgs`**: it returns the CRM
  account's legal name and identifier, which every organisation-scoped
  data call takes. The everyday name is not passed on.
- **`search_members` is the record view of a company's memberships**:
  every membership record for an organisation (by its identifier) or for
  a project, with status, tier, dates, the company name as the CRM spells
  it and the record's project slug. It answers "what does this company
  hold, on which projects, in which tiers, since when" — the story behind
  the figure. The figure itself (how many active memberships, their
  list-price value) is the memberships family, and the two are compared
  in words, never counted against each other.
- **`get_member_membership` and the key-contact tools** hold one
  membership's detail and its named contacts. Contacts are people:
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
  (name and identifier), the role, the voting status (voting, alternate,
  none), how the seat was appointed, and its status. Only active seats are
  seats.
- **A company's seats across the LF** come from the organisation seats
  tool: every seat the company holds, split by committee category with a
  summary by category and by project, in one call. It sits behind the
  organisation gate: a refusal under an identity without that company's
  read grant is the gate speaking, not an empty roster, and the answer
  says so. A ranking of companies by seats is not this tool's job (the
  querying playbook's routing table).
- **Roster facts come from here and nowhere else.** A board seat is never
  inferred from tier, sponsorship or activity. Country is not a roster
  field; "from N countries" about a committee is not reproducible.

## Meetings — what happened, who was there

- **Past meetings by project and date range** (`search_past_meetings`)
  return each occurrence with its duration, sessions, visibility (public
  or restricted) and, when it belongs to a committee, the committee
  identifier. The list is what the caller may see: restricted meetings of
  committees the caller is not on do not appear, so a count of meetings or
  a sum of hours is "visible to you".
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
- **People at a committee's or a meeting's past meetings over a period**
  come from the participants search with its date range, attended-only
  switch, exact organisation name and count-only mode; it de-duplicates
  people by identity. Two populations hide in the committee filter: with
  a date range it resolves the committee's past meetings and returns
  everyone at them; without one it returns the participant records that
  carry the committee — say which ran. A project's or a committee's own
  meeting count over a period is the count tool, "visible to you"; the
  total over the warehouse is the layer's. They are two readings, never
  adjusted toward each other; the gap is explained by the
  `lfx-figure-checking` skill's index-versus-warehouse entry.
- **Aggregate meeting metrics** (meetings held, scheduled minutes,
  people and attendances over a period, LF-wide, by foundation or by
  company) are not a service-tool job: they are the layer's named
  metrics and its attendance records, with no per-caller visibility; the
  meeting tools list (if explore does not offer them, the SQL assistant over the attendance data gives occurrences and scheduled minutes, labelled generated SQL, and the attendance recipe attendances, labelled interim) `[not yet in production: TOOLS-2 org
  meeting KPIs on the service tools — until then: the layer]`.

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
