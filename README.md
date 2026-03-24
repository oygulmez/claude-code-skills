# SEO Audit Skill for Claude Code

A comprehensive technical SEO audit skill for [Claude Code](https://claude.com/claude-code). Crawls all pages of a website and performs 200+ technical SEO checks with page-by-page reporting.

## What It Does

This skill turns Claude Code into a full-site technical SEO auditor. It's designed for:

- **Pre-launch audits** — Catch SEO issues before going live
- **Live site audits** — Monitor and fix technical SEO health on production sites

## Features

- **Full site crawl** — Discovers all pages via sitemap.xml, robots.txt, and internal link crawling
- **200+ technical SEO checks** across 12 weighted categories
- **Page-by-page reporting** — Shows exactly which errors are on which pages
- **Priority system (P0–P3)** — Critical issues first, improvements last
- **AI/LLM readiness** — Checks llms.txt, AI crawler policies, and structured data for AI search
- **Weighted scoring** — 100-point scale with category breakdowns
- **Actionable fixes** — Every issue comes with a specific solution and code examples
- **Auto-save report** — Saves `seo-audit-report-[domain]-[date].md` to your working directory

## Audit Categories

| Category | Weight | What It Checks |
|----------|--------|----------------|
| Crawlability & Indexability | 15% | robots.txt, sitemap, canonical, meta robots |
| On-Page SEO Elements | 12% | title, meta description, headings, alt text |
| URL Structure & Redirects | 10% | clean URLs, redirect chains, consistency |
| Internal Link Structure | 10% | crawl depth, orphan pages, broken links |
| HTTPS & Security | 10% | SSL, security headers, mixed content |
| Structured Data | 10% | Schema.org, JSON-LD, validation |
| Mobile Compatibility | 8% | viewport, tap targets, responsive |
| Performance Signals | 8% | render-blocking, DOM size, image optimization |
| Duplicate Content | 7% | title/desc duplication, canonical implementation |
| International SEO | 5% | hreflang, language tags |
| Social Media Tags | 3% | Open Graph, Twitter Cards |
| AI/LLM Compatibility | 2% | llms.txt, AI crawler management |

## Installation

### Global (all projects)

```bash
# Clone to Claude Code skills directory
mkdir -p ~/.claude/skills/seo-audit
cp SKILL.md ~/.claude/skills/seo-audit/SKILL.md
```

### Per project

```bash
# Clone to project's .claude directory
mkdir -p .claude/skills/seo-audit
cp SKILL.md .claude/skills/seo-audit/SKILL.md
```

## Usage

In Claude Code, simply run:

```
/seo-audit https://yoursite.com
```

Claude will:
1. Discover all pages (sitemap + internal link crawling)
2. Analyze each page against 200+ technical SEO criteria
3. Generate a detailed report with scores and prioritized fixes

## Example Output

```
# TEKNIK SEO DENETIM RAPORU

Site: https://example.com
Taranan Sayfa Sayisi: 24
Genel SEO Skoru: 72/100

## Sorun Ozeti
| Oncelik | Sayi |
|---------|------|
| P0 - Kritik | 2 |
| P1 - Yuksek | 5 |
| P2 - Orta | 8 |
| P3 - Dusuk | 12 |
```

## Technical SEO Checks Include

### Site-Wide
- robots.txt validation and AI crawler policies
- XML sitemap completeness and validity
- HTTPS enforcement and security headers (HSTS, CSP, X-Frame-Options)
- Server response and compression (Brotli/Gzip)
- URL structure consistency (trailing slash, www/non-www, case)
- Redirect chains and loops
- Internal link architecture and crawl depth
- Duplicate content detection
- Site migration readiness checks

### Per Page
- Title tag (length, uniqueness, relevance)
- Meta description (length, uniqueness)
- Meta robots and indexing directives
- Canonical tag validation
- Heading hierarchy (H1–H6)
- Image optimization (alt text, dimensions, lazy loading, modern formats)
- Structured data / Schema.org (JSON-LD)
- Hreflang and international SEO
- Open Graph and Twitter Cards
- JavaScript SEO (SSR, crawlable links)
- Core Web Vitals signals (render-blocking, CLS prevention, DOM size)
- Accessibility (ARIA, labels, lang attribute)
- Content quality signals (word count, text/HTML ratio)

### AI & LLM Readiness
- llms.txt file presence
- AI crawler management (GPTBot, ChatGPT-User, ClaudeBot, anthropic-ai, etc.)
- E-E-A-T signals (author info, citations, contact info)
- Content structure for AI consumption

## Requirements

- [Claude Code](https://claude.com/claude-code) CLI
- Internet access (for WebFetch)

## License

MIT

## Contributing

Contributions are welcome! Feel free to open issues or pull requests for:
- New SEO checks
- Updated criteria based on search engine changes
- Bug fixes
- Translations
