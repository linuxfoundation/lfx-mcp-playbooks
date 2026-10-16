<!-- Copyright The Linux Foundation and each contributor to LFX. -->
<!-- SPDX-License-Identifier: MIT -->

# Packet notes — footnotes, the provenance appendix, what stays untouched

The footnotes are written in the words the packet carries, so that every
packet says the same thing under the same measure and a reader comparing
two applicants reads the same qualifiers. Each footnote names the
measures it qualifies; the row recipes (`references/row-recipes.md`) name
the footnotes each cell carries. The agent copies the wording and fills
only the angle-bracket slots from this session's output.

## The footnotes

**Day cut.** Qualifies every windowed figure read on the semantic layer
(rest-of-LF people figures; meeting attendance in both circles).

> Figures marked ad hoc were read over the same dates as the rest of the
> packet, cut at the day boundary of the session clock rather than at
> UTC midnight, so they can differ from the governed figures by a few
> hours of activity at the window's edges.

**Rest of the LF, additive measures.** Qualifies every rest-of-LF cell
computed by subtraction (activities, projects, sponsorships, enrollments,
certifications, maintainer contributions).

> Computed as the LF-wide figure minus the foundation's figure, both
> read for the applicant over the same dates; the two are additive, so
> the difference is exact.

**Maintainers.** Qualifies the maintainers cells in all three circles,
the maintainer-contributions cell and the project rows of Part C.

> Maintainers are a roster read as of <run date>, not an activity count:
> a person is counted while listed on a project's roster with no end
> date, once however many projects they maintain. Within the Linux
> Foundation the count covers LF projects only. Outside it, the figure
> is a floor: the roster covers the non-LF projects the platform tracks.
> Per-project rows include people inherited from vendored Linux kernel
> trees on kernel-fork projects and MAINTAINERS-file reviewers, and a
> person maintaining two projects appears in each. Contributions by
> maintainers use the roster as of the data build.

**Seats.** Qualifies the seat cells, the technical-steering cell and the
seat side of Part C's group table.

> Seats are committee seats visible to the caller in LFX, complete for
> the scope under the caller's organisation grant. The foundation's seats
> are those of its whole project tree, as walked from the project
> records; LFX's own foundation scope for seats, the root project and its
> direct child projects, <agreed with that count | was below it by <n>
> seats on deeper projects>. The people figure for the foundation is the
> tool's figure for its own scope and is <exact | a floor, since deeper
> projects' seats are outside it>. The technical-steering figure is the seats filed under the
> committee category <stored category name>; board, oversight and
> advisory categories are counted in the total and not in it. Seats
> were read for <one account: the applicant's own record | <n> accounts:
> the applicant and the subsidiaries that could be discovered>; <parent
> only: a seat filed under a subsidiary's record is therefore not
> counted, while the other rows fold subsidiaries in | group: seat counts
> are added across the accounts; people are not>. A people figure is
> given only where the tool reported one for that scope.

**Meetings.** Qualifies the meeting-attendance cells and the attendance
side of Part C's tables.

> Meeting figures cover every LFX-registered meeting in the data
> warehouse over the packet's dates. People are distinct identified
> attendees; attendances are one person at one meeting occurrence, so a
> person at ten meetings counts ten. The figures are a floor bounded by
> which communities hold their meetings on the platform, and by the
> share of attendees whose organisation is recorded.

**Events.** Qualifies the event-attendee and events-sponsored cells.

> Registered is distinct people by e-mail with an accepted registration
> to an event that started in the window; checked in is the subset of
> them for whom check-in data exists, which only some registration
> sources record, so a zero means no check-in data rather than low
> attendance. Events sponsored counts events and sponsorships (one event
> can carry several); amounts are outside this packet. Registrations and
> sponsorships attach at foundation level. Figures are a floor where a
> registration carries no organisation.

**Training.** Qualifies the certification and enrollment cells.

> Platform data only, counted by enrollment date. Figures attributed to
> an organisation are a floor: one of the two training platforms records
> no organisation on its enrollments, so its rows cannot be attributed
> to the applicant.

**Speakers, rest of the LF.** Qualifies the rest-of-LF speakers cell.

> Computed as accepted speakers LF-wide minus accepted speakers at the
> foundation's events, both for the applicant over the same dates. A
> person who spoke in both is subtracted away, so this is a floor; it is
> exact when the foundation figure is zero.

**Participants.** Qualifies the "distinct people with any activity"
cells.

> Distinct people from the applicant with any non-bot activity in the
> window: code, issues, reviews, comments, stars, forks, meeting
> invitations and attendance, training and exams, Hacker News. This is a
> broader
> population than code contributors and is not a contributor count.

**Beyond the LF.** Qualifies the maintainers floor in the third circle
and every beyond-LF cell left as the template has it.

> LFX holds contribution activity for LF-hosted projects only.
> Contribution activity outside the Linux Foundation and participation
> in open standards bodies are not in LFX; those cells are left as the
> template has them. The one beyond-LF figure given, maintainers of
> projects outside the LF, is a floor from the maintainer roster the
> platform tracks.

### If the reader asks for the public Insights site's figures

They never go in a cell. The deck-building skill's section 6 governs
published figures: a platform query is never presented as if it
reproduced a published headline, and a published figure is never
reconciled against a warehouse figure. So the site's figures, if the
reader wants them in the packet, go in a note outside the grid, labelled
with the site's own window as the site states it and the site's own
company grouping, never described as LFX MCP data and never reconciled
with the grid. The beyond-LF cells still stay as the template has them:
the site and the packet count different populations under different
groupings, and a figure from either in the other's cell would be read as
the other's.

## The provenance appendix

One row per filled cell, in the `lfx-deck-building` skill's data-notes
format (its `references/data-notes-format.md`), with "Slide" read as the
cell's place in the packet: part, measure and circle, never a coordinate,
because templates differ and the measure is what the next run matches
on. The header block appears once at the top, filled for a packet:

```
Conventions
  Window:          twelve months to <yyyy-mm-dd>, from <yyyy-mm-dd>: the
                   dates the first governed call applied, reused on every
                   lane
  Org grain:       parent company, subsidiaries folded: <the applied scope
                   sentence of the first call, quoted>
  Circles:         1 = <foundation> and every project under it;
                   2 = the rest of the Linux Foundation (additive measures
                   by subtraction, people measures read directly with an
                   exclusion); 3 = beyond the LF, maintainers floor only
  Population:      bots excluded in contributor and activity figures;
                   counts only, no revenue, score, rank or weight
  Source lanes:    standard metrics for every governed cell; the semantic
                   layer, labelled ad hoc, where no family can express the
                   rest-of-LF exclusion or the measure (meetings); the
                   organisation seats tool, visible to you, for seats
  Captions:        the label (ad hoc, visible to you, floor, computed) in
                   the cell's label column, not only here
Run date:          <yyyy-mm-dd>; the run date stands for freshness
Seats read for:    <one account | <n> accounts, named>; foundation scope
                   root plus direct children
Membership:        <tier as stored>, <status>, <term start>–<term end>;
                   template written for <tier>; <match | mismatch, said
                   to the reader before filling>
```

The table header, with the first column renamed:

| Cell (part · measure · circle) | Figure | Source (lane; family or metric; scope as applied; window; population) | Coverage and caveats |
|---|---|---|---|

The Source cell quotes the `applied` block's scope and definition
sentences for a governed figure, and for a layer figure names the metric
as explore spelled it, the two scope readings in words (the company at any
depth; the subtree or the exclusion) and the day bounds. The Coverage cell
carries the label from the data-notes format's closed list, the footnote
names the cell carries, and for a computed cell the two figures it came
from. A board-view row says which Part B row it repeats. The appendix is
delivered with the packet, outside the document, for whoever re-runs it.

## What stays untouched

- **Part A**, the applicant's own statement.
- **The "applicant median" column** of Part B: filled by someone else
  after the window closes.
- **Every "Not in LFX" cell** except the maintainers floor in the third
  circle.
- **The template's structure**: rows, headers, numbering and wording. The
  skill fills by measure and circle; it never adds, removes or renames a
  row. A template measure no recipe covers is left as the template has it,
  and the reply says which.
- **The membership tier the template was written for**: when it differs
  from the applicant's real tier, the mismatch is said to the reader
  before any cell is filled, the reader chooses the template, and the
  snapshot carries the real tier and term. The figures do not depend on
  the tier; the application form does.
