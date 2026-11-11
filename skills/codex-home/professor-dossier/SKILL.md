---
name: professor-dossier
description: Research and evaluate one professor or PI at a time for PhD outreach decisions, producing a citation-backed standalone HTML dossier. Use when the user asks to evaluate a professor, decide whether a professor is worth contacting, perform 导师调研, create a professor dossier, assess PI funding/lab composition/student backgrounds/recruiting signals, inspect Google Scholar/publications, estimate admitted PhD student profiles, or perform PhD advisor outreach due diligence.
---

# Professor Dossier

## Overview

Create a visual, evidence-backed professor dossier for deciding whether to contact a PI. If the user requests Chinese output, write the final dossier and chat summary in Chinese while preserving official names, paper titles, database names, grant titles, and institution/program names in English when translating would reduce precision. Evaluate the professor and lab opportunity on their own merits unless the user explicitly supplies personal background for a fit layer.

## Required Inputs

If missing, ask for only the information needed to disambiguate the target:

- Professor name.
- Institution or department.
- Field/program context when multiple people share the name.

## Research Workflow

1. Search current web sources. Funding, lab membership, papers, and recruitment status are time-sensitive; browse before making factual claims.
2. Read `references/source-quality.md` before evaluating evidence, demographic information, or uncertainty.
3. If any important official page is blocked, JavaScript-rendered, or only partially readable, read and follow `references/blocked-page-fallbacks.md` before giving up. Do not bypass CAPTCHA, login, paywalls, or access controls; look for legitimate readable copies, indexes, APIs, archives, or user-authorized local saves.
4. If generic web search does not confirm identity, try institution-specific directories and URL patterns before concluding the person is unresolved. For universities, search/open college subdomains, faculty directories, people pages, lab pages, PubMed full-author queries, and NIH RePORTER/NSF searches when relevant. Do not stop after checking only generic lab-site paths such as `/members`, `/team`, or `/people`; also test institution CMS patterns and exact search queries for the lab name.
5. For current and recent PhD students, search public profiles before estimating admissions background. Check lab team pages, alumni pages, LinkedIn/public CVs, personal sites, Google Scholar, PubMed, ORCID, conference bios, thesis pages, and institutional news. If a lab people page is blocked by Cloudflare, JavaScript, login, or other bot protection, record the exact URL as a real source attempt and label member details as `Unknown/Blocked`, not `Not found`.
6. Build an evidence table before writing conclusions. Track claim, status, source URL, access date, and notes.
7. Fill the HTML template at `assets/professor-dossier-template.html`; keep it standalone and usable without a build step.
8. Save the dossier by default to `dossiers/<Institution>_<ProfessorLastName>_dossier.html` in the current workspace. Create the folder if needed. If the user provides a preferred output path, use that path instead.
9. End with a short chat summary in the user's requested language: recommendation, confidence, top risks, next research step, and path to the HTML file.

## Source Targets

Prioritize these sources:

- Official faculty, department, lab, and graduate program pages.
- Google Scholar, ORCID, PubMed, Semantic Scholar, DBLP, or field-appropriate publication indexes.
- NIH RePORTER, NSF Award Search, DoD/DOE/Foundation award pages, and institution news releases for grants.
- Lab people/alumni pages and public LinkedIn pages for academic/professional background.
- Public student profiles, personal websites, public CVs, ORCID/Google Scholar/PubMed author pages, thesis repositories, and conference bios for PhD student pre-admission background.
- Recent papers, preprints, and project pages for direction changes.

Avoid relying on only one source type. Prefer official pages for identity and positions, funding databases for grants, and publication indexes for publication/citation signals.

## Dossier Sections

Include these sections in the HTML:

- Basic profile: institution, department, rank, lab, contact, links.
- Research map: themes, methods, model systems/data, recent direction shifts.
- Publications: Google Scholar profile if available, citation snapshot, recent/high-signal papers, venues, collaboration pattern.
- Funding: active/recent grants, sources, recency, role, and funding risk.
- Lab composition: current members, roles, education/professional background, alumni destinations where public.
- PhD student pre-admission profile: current/recent PhD students' prior institutions, degree path, pre-PhD publications, research employment, and evidence confidence.
- Recruiting/funding signals: explicit PhD openings, program mechanism, rotation/direct admit clues, recent student intake.
- Outreach recommendation: `High`, `Medium`, `Low`, or `Do not contact yet`, with evidence-backed reasons.
- Evidence log: all important claims with source links and access date.

## PhD Student Background Analysis

When the lab has current or recent PhD students, add a "PhD Student Baseline" section. Focus on patterns that help estimate implicit admissions expectations:

- Prior institution and degree path: undergraduate school, master's school, prior PhD program if any, and whether the student appears to be direct-from-undergrad, master's-to-PhD, RA-to-PhD, industry-to-PhD, or clinical/professional-to-PhD.
- Pre-PhD publications: count only papers that can reasonably be dated before the PhD start or before joining the lab. Mark unclear cases as `Unknown`, not zero. For each confirmed or possible paper, include title/year, journal, student author position, whether they are first/co-first/corresponding where public, and journal signal such as impact factor and quartile/rank when a citable source is available.
- Research experience: prior lab roles, thesis projects, research assistant jobs, postbacc, industry research, clinical research, or internships when public.
- Field/method background: methods or domain experience relevant to the PI's lab.
- Pattern summary: give a cautious aggregate such as "visible students commonly had prior research experience; publication baseline is unclear for most profiles."

Do not over-rank schools or infer competitiveness from institution names alone. Use student background evidence to estimate the lab's admissions baseline, not to judge the students.

### Student Search Procedure

For each current or recent PhD student:

0. Build a lab-page URL checklist before concluding a team page is absent. Include:
   - Official faculty profile links and all linked lab/people pages.
   - Search queries: `"<PI full name>" "<institution>" "lab" "people"`, `"<PI last name> lab" "<institution>"`, `"<Lab Name>" "people"`, `site:<institution-domain> "<PI last name>" "lab" "people"`, and `site:<institution-domain>/labs-departments/labs "<PI last name>"`.
   - Institution CMS patterns when visible. For Michigan Medicine / UMich medical research pages, always try `https://medresearch.umich.edu/labs-departments/labs/<slug>/people`, `.../<slug>/research`, and `.../<slug>` where `<slug>` is a normalized lab name such as `angeles-lab`.
   - Common generic paths on independent lab sites: `/people`, `/members`, `/team`, `/lab-members`, `/alumni`, `/join`, `/research`.
   If an official URL exists but the content is blocked, write `Official people page exists but content was blocked from automated access` and cite the URL.
1. Start from the lab/team/alumni page to get the canonical name, role, lab affiliation, and approximate time window. When the canonical page is blocked, use any visible search snippets or alternate public indexes cautiously, and explicitly separate `page exists` from `content verified`.
2. Search LinkedIn/public profile pages with combinations of student name + PI last name + university + department/program. Use LinkedIn only for public education, degree, job, and research-role information.
3. Search Google Scholar, ORCID, PubMed, and Semantic Scholar with student name + PI last name + lab keywords. Attribute papers only when affiliation, coauthors, topic, or lab publication lists support the match. For attributed papers, inspect author lists to capture author order and equal-contribution/corresponding-author notes when available.
4. Search personal websites, public CVs, thesis repositories, conference abstracts, and institutional news for start dates, prior institutions, and pre-PhD research roles.
5. Look up journal metrics for highlighted student papers. Prefer official Journal Citation Reports/Clarivate pages when accessible; otherwise use journal official pages, Scimago/SJR, indexed publisher pages, or clearly dated third-party metric pages. Always record the metric year/source and mark metrics as approximate if they are not from official JCR.
6. Record all student-level findings with confidence: `High` for official/CV/clear LinkedIn or indexed publication matches; `Medium` for consistent but partial evidence; `Low` for same-name ambiguity, missing timelines, or non-official metric sources.

When LinkedIn or Scholar is inaccessible, blocked, or absent, note that explicitly and continue with available public sources. Do not ask the user to log in.

## Recommendation Rules

Use `High` when research activity, funding/recruiting signals, and lab stability are all strong enough to justify outreach now.

Use `Medium` when the lab looks plausible but has meaningful uncertainty, such as unclear openings, stale lab pages, or incomplete funding visibility.

Use `Low` when there are weak recruiting/funding signals, poor evidence recency, major mismatch with PhD training pathways, or little sign of active student mentoring.

Use `Do not contact yet` when the identity is ambiguous, evidence is too sparse, the professor appears inactive/retired/not taking students, or a critical risk needs manual confirmation first.

Always include confidence: `High`, `Medium`, or `Low`. Low confidence means the recommendation is provisional, not necessarily negative.

## Fit Layer

By default, evaluate the professor only. If the user explicitly provides their background, research interests, CV, or asks for personalized fit, add a short "User Fit" section that separates user-specific claims from professor-only claims.
