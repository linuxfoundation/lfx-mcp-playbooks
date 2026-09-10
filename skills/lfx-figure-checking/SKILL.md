---
name: lfx-figure-checking
description: Checks a stated LFX figure against a fresh read and explains a difference by its mechanism — why two tools, two reports or two runs give two numbers for what sounds like one question, which one to quote, and how to write the reconciliation. Use whenever someone asks to verify, audit, reconcile, cross-check or sanity-check a number about Linux Foundation projects, members, contributors, events, health, meetings or governance, asks "why do these differ", "is this figure right", "can we still say this", or wants a deck, a report or a slide checked against LFX data before it goes out.
---
<!-- Copyright The Linux Foundation and each contributor to LFX. -->
<!-- SPDX-License-Identifier: MIT -->

# Checking LFX figures

A figure on a slide, in a report or in a chat transcript came from
somewhere: a tool, a window, a population, a vocabulary, a day. Checking
it means reading it again from the right place and, when the fresh read
differs, naming the mechanism that separates the two. Two LFX tools asked
what sounds like the same question routinely return two different
numbers, and both are usually right about different things. The failure
this playbook exists to prevent is the average, the larger number, or
"sources disagree".

The fresh read itself is the querying playbook's job (`lfx-data-querying`:
which tool, discovery, the answer with its provenance). This playbook
starts when a figure already exists and the question is whether it holds.
Read the tool guidance once per session before any call:
`read_lfx_standard_metrics_guidance` and `read_lfx_semantic_layer_guidance`
own every parameter and switch; nothing here restates them.

## 1. What a stated figure carries

Before re-reading anything, pin down what the stated figure claims to be.
Most differences are decided here, not in the tools.

- **Its source kind.** Three kinds exist and are never reconciled against
  each other: a warehouse reading (the standard metrics, the semantic
  layer, the SQL assistant: every record loaded, no per-caller
  visibility); an LFX v2 record reading (the count tool, the searches, the
  rosters: records of projects onboarded into LFX v2, filtered to what the
  caller may see, the population LFX applications show their users); and a
  published figure (an annual report, a press release, a partner's page:
  cited to its publisher, never rebuilt). A slide that quotes one kind is
  checked against that kind.
- **Its population.** Memberships or organisations; contributors or
  participants; occurrences, attendances or people; seats or people;
  accepted speakers or every proposal. The word on the slide is not the
  grain; the grain is what was counted as one.
- **Its scope and window.** LF-wide with no project, a foundation with its
  tree, one bucket; a calendar year, a trailing year, year to date bounded
  at the day it was read; a status as of a day. A window read weeks apart
  moves with the data, and the current period is partial on both reads.
- **Its vocabulary and grain of organisation.** CRM legal name or enriched
  spelling; account alone or parent with subsidiaries folded; conformed
  country or raw billing string.
- **Its label.** A label can be wrong while the number is right: a
  per-mention sum called "de-duplicated", a seat count called
  "maintainers", a series-person count called "meetings". Check the label
  against the mechanism, not only the number against a fresh number.

## 2. The procedure

1. **Read the stated figure's claim** in the terms above. If the slide or
   the transcript does not say, infer the likeliest reading and say that
   it was inferred.
2. **Take the fresh read from the matching place**, through the querying
   playbook: the governed family where one covers it, the layer for a
   slice, the record tools for a caller-visible count, the SQL assistant
   only where nothing else expresses it. Read the population, scope and
   window back from the `applied` block, the scope line or the record
   fields, never from the request you meant to send.
3. **Compare, and name the mechanism.** Walk
   [references/why-figures-differ.md](references/why-figures-differ.md)
   by domain; most differences are one mechanism, and a large one is
   usually scope. The mechanism is stated in the reader's words: what
   each side counted and why that yields a different number.
4. **Give the verdict** in one of five words, and mean it:
   - **ours** — the stated figure is mis-keyed, mis-scoped or mislabelled;
     the fresh read is the one to quote, and the trap is named;
   - **both** — two defensible readings of a stated choice (population,
     field, grain, source kind); the slide must declare which, and the
     check says what each is;
   - **same** — agrees within the drift the window allows; a few percent
     on a live figure is time, not error;
   - **open** — not checkable under this identity (a gated tool, a
     private scope); say what identity could check it;
   - **unverifiable** — a published figure with no LFX population behind
     it; cite it to its publisher and stop.
5. **A difference no mechanism explains is not a finding.** It is a
   discovery failure on one side: a wrong literal, a wrong slug, a shell
   account, an unbounded window, a partial period. Fix the read and check
   again. "Sources differ" never goes in a check.
6. **Other dashboards and pages are not a reconciliation surface.** They
   differ by registration, cleaning and curation; say what the LFX figure
   covers and stop.

## 3. The mechanisms, by domain

The catalogue lives in
[references/why-figures-differ.md](references/why-figures-differ.md), one
entry per mechanism, grouped so a check reads one section:

- **Memberships and organisations** — status-based versus date-based
  counts; pairs versus organisations; tier rows above the total; account
  alone versus the group; list price versus dues billed; new memberships,
  arrivals, churn and departures; the roll-forward residues; billing
  country versus conformed country.
- **Projects and scope** — a foundation's slug versus its own bucket;
  whole tree, one level, one hop; the umbrella versus LF-wide; a
  consortium and its fund; twin slugs; attachment level.
- **People and activity** — contributors, participants, contributions;
  bots; unattributed and placeholder rows; headcount versus volume;
  maintainers as people versus seats; the maintainer roster as of a build.
- **Events and training** — accepted speakers versus proposals;
  registrations, registrants, checked-in; sponsorship assets versus
  sponsors; platform training versus the published figure.
- **Health and value** — score versions; LF-hosted versus the index
  population; scored versus unscored rows.
- **Meetings and rosters** — attendances, attendees, invitees,
  occurrences; potential impressions versus potential audience; indexed
  in LFX v2 versus the warehouse; roster versus inference.
- **Time** — trailing versus calendar; UTC days versus the session clock;
  all time versus the sum of windows; partial periods and future-dated
  installs; run date, not refresh date.

The traps that produce a plausible wrong number instead of an error, each
with its symptom, cause and check:
[references/gotchas.md](references/gotchas.md). A check that finds one of
them names it as the cause.

## 4. Writing the check

A check is written for the person who owns the figure, in their words.
Tool names, field names and SQL stay in the provenance. The shape that
survives review:

- **One row per figure**, in a table: the figure as stated (with its
  label), the fresh read, the mechanism in a sentence, the verdict word.
  Group rows by domain; put "ours" rows before "both" rows so the reader
  sees what must change before what must be declared.
- **Every fresh read carries its provenance** exactly as the querying
  playbook writes it: tool, scope, window, population, run date, and the
  label where the figure is not governed. A verifier must be able to
  re-run each row.
- **Drift is stated once**, at the top: the stated figure's date and the
  fresh read's date, and the note that a live figure moves between them.
- **Nothing is averaged or reconciled to a third number.** Where the
  slide must choose, the check says the two choices and which the
  playbooks recommend for a headline: the governed reading, the warehouse
  for an LF-wide total, the record tools for "in LFX v2 today, visible to
  you".
- **A label correction is its own finding**, even when the number stands.
- **No figure is verified from memory.** Every number in a check came
  from this session's reads; a number remembered from an earlier session
  is re-read.

## 5. Before delivering a check

- Each row names its mechanism or says the difference is drift; no row
  says "sources differ".
- Each fresh read was taken from the source kind the stated figure claims,
  and the `applied` block, scope line or record fields were read back.
- The current period is bounded at today on both sides of every series
  comparison.
- Gated or private reads are marked open with the identity that could
  close them, not silently dropped.
- Published figures are cited, not rebuilt.
- The verdict words are used as defined; a "both" row says what each
  reading is; an "ours" row names the trap.
