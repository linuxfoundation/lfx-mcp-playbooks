---
name: lfx-deck-building
description: Produces a deck's worth of LFX figures that stay consistent with each other — conventions fixed before the first query, cross-framing checks, a data-notes appendix, a final consistency pass, and the citation rule for what LFX cannot reproduce. Use when building a board deck, a member report or any multi-figure deliverable from LFX data.
---
<!-- Copyright The Linux Foundation and each contributor to LFX. -->
<!-- SPDX-License-Identifier: MIT -->

# Building a deck from LFX data

A deck fails differently from a single answer: every figure can be
defensible on its own while the deck contradicts itself — one slide counts
members by legal entity and another by parent company; one uses the
trailing twelve months and another the calendar year; one denominator
excludes bots and another does not; one slide is LF-wide and the next is a
single foundation without saying so. This playbook is the discipline that
keeps a deck's figures consistent with each other.

Prerequisite: the `lfx-data-querying` playbook — the lanes, the routing,
the discovery rules and the provenance block. Every figure on every slide
is produced that way. This playbook adds what a deck needs on top.

## 1. Set the conventions first

Before the first call, fix six choices and hold them for the whole deck.
They are written on the data-notes slide (section 3).

1. **Window.** One of: the trailing twelve months to a stated date, or a
   stated calendar period. Concrete dates, everywhere. Any current-period
   figure is bounded at the run date and labelled partial.
2. **Organisation grain.** Legal entity, or parent company with
   subsidiaries folded in. The two answer different questions, and a
   company that is itself a subsidiary disappears as its own row under the
   parent grain. Choose once; say which; and when a slide names a company,
   say what the name covered (the account alone, or it and everything
   under it).
3. **Population.** Bots excluded by convention in contributor and
   activity figures; shares computed on the org-attributed base, with the
   unattributed share stated once on the data-notes slide, not hidden.
4. **Headcount versus volume.** People for "how many"; work for "share".
   Never one presented as the other; distinct counts never summed across
   rows; the two organisation vocabularies never mixed across slides.
5. **Source lane per slide type.** Headline counts, revenue, shares and
   series: standard metrics. A grouping the families lack: the semantic
   layer, labelled ad hoc. Cross-domain shapes only: the SQL assistant,
   labelled as generated SQL, never alone under a headline. Rosters and
   meeting lists: the service tools, labelled "visible to you".
6. **Scope statement per slide.** LF-wide, one foundation and its projects,
   one project, one company — stated on every slide that carries a figure,
   in the reader's words, and held consistent within a section. A scope
   that changes between two adjacent slides is the single most common way a
   deck misleads.

Where a region grouping appears, the slide says the LF region grouping is
provisional pending stakeholder sign-off.

## 2. Cross-framing checks

The data is fluid; there is no table of correct figures to check against.
Instead, every headline figure is confirmed by a second, independent
framing before it goes on a slide. A scoping trap shows up as a jump of
several times, not as noise. Use whichever applies:

- **A foundation total against its projects.** The foundation figure read
  as one folded number, and the same figure broken down by project;
  additive figures reconcile, distinct counts do not sum and the breakdown
  is reported as a breakdown.
- **A tier split against the member total.** The per-tier rows and the
  folded total come from the same scope and date; they reconcile.
- **Contributors ≤ participants ≤ activities.** People with a code
  contribution sit inside people with any collaboration, and both sit
  below the volume of work.
- **One scope level up.** A project's figure sits inside its foundation's;
  a foundation's inside the LF-wide figure. If it does not, one of the two
  scopes is wrong.
- **A second lane where two cover the ground.** A figure from the semantic
  layer or the SQL assistant that a standard metric also covers is read
  from the standard metric too; the governed figure wins, and the
  difference is explained or the figure is dropped.

A figure checked only against itself does not go on a slide.

## 3. The data-notes appendix

Every deck carries a data-notes appendix (one or more slides, or a
companion page) that lets an engineer take any row, re-run it, and either
reproduce the figure or find the pipeline that drifted. Its format is in
[references/data-notes-format.md](references/data-notes-format.md): one
row per figure, in the columns **Slide | Figure | Source | Coverage and
caveats**, where *Source* is the provenance block of the querying playbook
compressed to one cell (lane; family or metric; scope as applied; window;
population) and *Coverage and caveats* says what the figure does and does
not cover.

Once per deck, at the top of the appendix:

- the six conventions of section 1, as chosen, and the region note;
- the run date (or the date range over which figures were pulled), which
  stands for freshness: no lane reports a data refresh time;
- the unattributed share, stated once.

## 4. Final consistency pass

Before the deck ships, re-read every figure against the deck as a whole:

- **One window, one organisation grain, one denominator policy** on every
  slide; where a slide had to differ, the slide itself says so and the
  appendix row explains why.
- **Totals reconcile.** Foundation rows sit inside the LF-wide figure; tier
  rows reconcile to the member total; breakdown slides of distinct counts
  are labelled as breakdowns, never as sums.
- **Year-over-year compares completed periods**, or the partial period is
  labelled as partial on the slide.
- **Every generated-SQL figure is labelled** on the slide and in the
  appendix, and no headline rests on one alone.
- **Every service-tool figure says "visible to you"** and is not presented
  as an LF total.
- **The data-notes slide states** the conventions, the scope of each
  section, the run date and the unattributed share.
- **Every figure was re-run**, not remembered from an earlier draft of the
  deck.

## 5. What LFX never reproduces, and how to cite it

Some figures a deck wants cannot come from the LFX tools, and the honest
move is to cite the source that can carry them — never to present a
platform query as if it reproduced a published headline.

- **Published annual-report figures.** The reports' definitions of members,
  developers and contributing organisations have changed between years;
  only a run of years with one definition can be charted. Cite the report
  and the year on the slide; chart only an internally consistent series and
  say so; never reconcile a report figure against a warehouse figure on the
  same slide.
- **External case studies and third-party numbers.** Cite the publishing
  organisation, the document and its date. Confidence is the source's, not
  LFX's.
- **Graphics carried from earlier decks.** Mark them "carried, not
  regenerated", with the source deck. Nothing on them was produced by a
  pipeline for this deck.
- **Lifetime training claims.** The platform data covers the platform's
  own history; a lifetime headline is a published figure and is cited as
  one.
- **Committee members' countries.** Roster records carry organisation and
  role; country is not a roster field, so a "from N countries" claim about
  a committee is not reproducible.
- **Mentorship and crowdfunding.** Out of scope of the tools; published
  figures, cited as such.
- **Any figure whose population the tools cannot state.** If no lane can
  say who or what was counted, the figure is not reproducible and is not
  presented as LFX data.

On the slide: the source in the reader's words ("LF annual report, <year>";
"<organisation> survey, <year>"). In the appendix: the citation in full.
