# Blocked Page Fallbacks

Use this reference whenever an official faculty, lab, people, alumni, or program page is blocked by Cloudflare, CAPTCHA, bot protection, JavaScript rendering, login, or a timeout. The goal is to find legitimate readable public versions or corroborating public evidence. Do not bypass CAPTCHA, defeat access controls, use stolen cookies, scrape private content, or misrepresent the result.

## Required Record

For every blocked page, record:

- Original URL.
- Block type: Cloudflare/CAPTCHA, JavaScript-only, login, 403/401, timeout, robots/noindex, or unknown.
- Access date.
- Fallbacks attempted.
- Whether each fallback returned content, only metadata/snippets, or nothing.

Use wording such as `official people page exists but automated content access was blocked`. Never write `no people page found` when a canonical URL exists but could not be read.

## Fallback Order

1. **Exact URL and canonical variants**
   - Try `https` and `http` if appropriate.
   - Try with and without trailing slash.
   - Try parent pages such as `/labs/<slug>`, `/people`, `/research`, `/publications`, `/join`, `/alumni`.
   - Inspect redirects, canonical URLs, page title, and status codes.

2. **Text-rendering and reader views**
   - Try reader/text services that fetch public pages without requiring login, such as a reader endpoint that prefixes the target URL with `https://r.jina.ai/http://`.
   - Try browser/readability views when available.
   - If the reader returns only the anti-bot page, record that result and continue.

3. **Search index discovery**
   - Search exact URL in quotes.
   - Search page title and lab name with `people`, `members`, `team`, `graduate student`, `research technician`, `postdoc`, `PI`, and institution.
   - Search within domains: `site:<domain> "<PI last name>" "people"`, `site:<domain> "<Lab Name>"`, and institution CMS paths.
   - Use snippets only as weak evidence unless they expose exact names/roles clearly. Prefer finding a source page behind the snippet.

4. **Sitemaps, robots, and feeds**
   - Check `/robots.txt`, `/sitemap.xml`, sitemap indexes, RSS/Atom feeds, and CMS-generated XML feeds.
   - Search sitemap entries for lab slug, people pages, profile pages, and member names.

5. **Structured data and static payloads**
   - Inspect readable HTML for `application/ld+json`, `__NEXT_DATA__`, `window.__NUXT__`, Drupal settings, JSON script tags, or API endpoints.
   - Try official JSON endpoints only when they are public and unauthenticated. Examples include site search APIs, Drupal JSON:API routes, or static JSON assets referenced by the page.
   - Do not brute-force private APIs or use credentials.

6. **Archives and public crawls**
   - Check the Internet Archive/Wayback CDX for the exact URL and parent lab URL.
   - Check Common Crawl indexes when practical.
   - Treat archived lab-member rosters as dated evidence, not current membership.

7. **Institutional mirrors and alternate pages**
   - Look for department, center, graduate program, seminar, award, news, and profile pages that list the same people.
   - Search institution directory pages for the lab name or PI last name.
   - For medical schools and cancer centers, check both school, department, center, and hospital domains.

8. **Publication and funding corroboration**
   - Use PubMed/PMC author affiliations, acknowledgments, author contributions, NIH RePORTER personnel/abstracts, GitHub orgs, ORCID, Google Scholar, and conference bios to identify visible trainees or staff.
   - Clearly label these as publication/funding-derived member signals, not confirmed current lab roster entries.

9. **User-authorized local capture**
   - If the user can access the page in their browser, ask for a local saved HTML/PDF/screenshot or pasted page text.
   - Once provided, parse the local file and cite it as user-provided capture with capture date, while preserving the official source URL.

## Output Rules

- If a readable roster is found, list members with role, source, and access date.
- If only partial evidence is found, separate `Confirmed current roster`, `Possible current members`, and `Publication-derived trainee signals`.
- If no readable roster is found after fallbacks, keep the canonical blocked page in the evidence log and make the next step concrete: e.g., `open official people page manually and save HTML`.
