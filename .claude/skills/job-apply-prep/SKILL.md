---
name: job-apply-prep
description: Prepare a complete, ready-to-submit application package (tailored CV, application answers, gap check) for a London growth marketing or strategy consulting role from LinkedIn, Wellfound, or Indeed, and log it to the tracker. Stops short of clicking submit. Use when Vanshita shares a job posting, link, or asks to prep/track an application.
---

# Job Apply Prep

## What this skill does not do
It does not log into LinkedIn, Wellfound, or Indeed, and it does not click
Apply. There is no browser session available that is authenticated as
Vanshita, and automated submission on these platforms would violate their
terms of service and risk her accounts. Every run of this skill ends with
a package ready for Vanshita to review and submit herself.

If Vanshita asks for auto-submission, remind her once why it's out
(ToS/account-ban risk, and a human should see each JD before it goes out),
then continue with the prep-only workflow rather than refusing outright.

## Scope
Only London-based (or explicit remote-UK) roles in growth marketing or
strategy consulting. If a shared posting falls outside this (wrong
location, wrong function, obviously junior/senior mismatch), say so before
building anything, and confirm whether to proceed anyway.

## Intake
Vanshita will hand this a job posting as either:
- A pasted job description (preferred, always works)
- A URL to the posting

For a URL: try WebFetch to pull the page text. LinkedIn, Wellfound, and
Indeed job pages often sit behind login walls or bot detection and the
fetch may return nothing usable. If that happens, say so plainly and ask
her to paste the JD text directly rather than guessing at the role from
the URL or title alone.

## Steps
1. **Intake the JD** per above. Extract: company, role title, seniority,
   location, key requirements, and any application questions posted
   alongside the JD (e.g. "why do you want to work here").
2. **Gap check first, before building anything.** Using the cv-builder
   skill's honesty rules, flag plainly if there's a real experience,
   seniority, or skills gap against this specific posting. If the gap is
   large enough that applying is likely a waste of her time, say so and
   ask whether to proceed.
3. **Invoke the cv-builder skill** to produce the tailored one-page CV
   for this JD (PDF, ATS-friendly, per its format rules). Do not
   duplicate its rules here; defer to it for CV construction and honesty
   constraints.
4. **Draft application answers**, if the posting includes free-text
   questions, following cv-builder's rules on honesty for application
   answers (name real gaps, no invented coverage).
5. **Save the package** to `applications/<company-slug>-<role-slug>/`:
   - `CV.pdf`
   - `answers.md` (if there were application questions)
   - `notes.md`: JD source (URL or "pasted"), gap-check summary, date
     prepared
6. **Log to the tracker** at `applications/tracker.csv`. Append one row
   with: date prepared, company, role, location, source platform
   (LinkedIn/Wellfound/Indeed/other), status (`ready to apply`), gap
   flagged (short phrase or "none"), folder path. Never overwrite
   existing rows; only append.
7. **Hand off clearly.** Tell Vanshita the package is ready, where it
   lives, and restate any gap flagged in step 2. She applies manually.

## Status tracking
When Vanshita reports back that she applied, got a response, an
interview, a rejection, or an offer for a tracked role, update that row's
`status` and `last_updated` columns in `applications/tracker.csv` rather
than creating a new row. Ask which role if it's ambiguous from context.

## What never changes across roles
The honesty rules in cv-builder (real work history only, no fabricated
tools/numbers/budget ownership, hold the line even under pushback) apply
identically here — this skill only adds sourcing, gap-check-first
ordering, packaging, and tracking on top.
