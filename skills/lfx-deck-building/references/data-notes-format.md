<!-- Copyright The Linux Foundation and each contributor to LFX. -->
<!-- SPDX-License-Identifier: MIT -->

# The data-notes appendix — format

The appendix is the deck's audit trail: one row per figure, so that an
engineer can take any row, re-run the stated call, and either reproduce the
figure or find the pipeline that drifted. It goes at the back of the deck
(one or more slides) or on a companion page the deck links to.

## Header, once per deck

Before the table, state once:

```
Conventions
  Window:          <trailing twelve months to yyyy-mm-dd | calendar yyyy | ...>
  Org grain:       <legal entity | parent company, subsidiaries folded>
  Population:      bots excluded by convention; shares on the
                   org-attributed base; unattributed share stated below
  Headcount/volume: people for "how many"; work for "share"
  Source lanes:    headline figures = standard metrics; <exceptions listed>
  Captions:        the grain and the label on the slide itself, not only here
  Scope per slide: stated on each figure slide; sections: <section → scope>
Note: LF region grouping is provisional pending stakeholder sign-off

Run date:          <yyyy-mm-dd> (figures pulled <yyyy-mm-dd> to <yyyy-mm-dd>);
                   the run date stands for freshness — no lane reports a
                   data refresh time
Unattributed:      <n>% of <metric> in <scope>, <window>, has no resolved
                   organisation; org shares are computed on the rest
```

## The table

Empty:

| Slide | Figure | Source (lane; family or metric; scope as applied; window; population) | Coverage and caveats |
|---|---|---|---|
| | | | |

One filled row, placeholders only (`<n>` stands for the figure; nothing
here is a real value):

| Slide | Figure | Source (lane; family or metric; scope as applied; window; population) | Coverage and caveats |
|---|---|---|---|
| `<slide id>` | "`<n>` companies are members of CNCF" | Standard metric; memberships, one figure; CNCF and its subprojects as one figure; as of `<yyyy-mm-dd>`; `<the definition sentence the tool returned>` | Governed. Memberships attach at foundation level. Count, not revenue: the list-price value is a separate figure. |

The *Source* cell is the provenance block of the querying playbook,
compressed: lane first, then the family or the metric as named by the tool,
then the scope exactly as the `applied` block reported it (the name, and
whether it covered the tree or the subsidiaries), then the window as
concrete dates or the as-of date, then the population sentence the tool
returned. Column names, keys and SQL stay out of the table; the compiled
SQL is kept with the working files and produced on request.

## Rules for the Coverage column

Every row says what the figure does and does not cover. At minimum:

- **The label.** One of: *Governed* (standard metric); *Ad hoc* (semantic
  layer); *Generated SQL* (SQL assistant); *Visible to you* (service
  tools); *Interim recipe* (the meeting-metrics workaround); *Published*
  (a cited external figure, no LFX lane).
- **Unattributed share**, whenever the figure is an organisation share or
  an organisation ranking: "computed on the org-attributed base;
  unattributed share stated in the header".
- **"Visible to you"** on every figure counted from the service tools
  (rosters, meetings, participants, membership records): the count is what
  the caller's identity could see, not an LF total.
- **"Generated SQL"** on every SQL-assistant figure, with the scope line
  the tool returned (LF-wide, or the slugs) repeated in the cell.
- **"Interim recipe"** on any aggregate meeting metric, worded
  "attendances" (records), not "attendees" (people).
- **Distinct count** where the figure is people or organisations: "distinct;
  rows of the breakdown do not sum to it".
- **Partial period** where the last period of a series is to-date.
- **Attachment level** where a project-level reading is legitimately empty
  or sits at foundation level (memberships, registrations, sponsorships).
- **Different grain** where two figures on one slide must not be divided
  (membership count and list-price value).
- **Vocabulary** where organisations on the slide come from the enrichment
  spelling rather than CRM legal names.
- **Region grouping provisional** where a region appears.
- **Published, cited** where the figure is not LFX data: the source, the
  document and the year, and "not reconciled against LFX".
- **Carried, not regenerated** where a graphic or figure was copied from an
  earlier deck: the source deck.

A row whose Coverage cell is empty is a figure nobody has thought about.
