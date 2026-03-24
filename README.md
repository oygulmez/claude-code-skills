# Claude Code Skills Collection

A comprehensive collection of professional skills (slash commands) for [Claude Code](https://claude.com/claude-code). Designed for web developers, SEO specialists, and digital agencies.

## Skills

| Skill | Command | Description |
|-------|---------|-------------|
| **SEO Audit** | `/seo-audit [url]` | Full-site technical SEO audit with 200+ checks, page-by-page reporting |
| **Content SEO** | `/content-seo [topic] [lang] [type]` | SEO-optimized multilingual content creation with E-E-A-T compliance |
| **Schema Generator** | `/schema-gen [type] [url]` | Schema.org JSON-LD structured data generator for any page type |
| **WP Performance** | `/wp-performance [url]` | WordPress performance analysis and Core Web Vitals optimization |
| **WP Doctor** | `/wp-doctor [error]` | WordPress error diagnosis and troubleshooting (WSOD, 500, SMTP, plugin conflicts) |
| **Project Init** | `/project-init [name] [type]` | New project scaffolding with CLAUDE.md, .cursorrules, git, and folder structure |
| **Deploy Check** | `/deploy-check [url]` | Pre-launch checklist: SEO, performance, security, legal (KVKK), analytics |

## Installation

### Global (all projects)

```bash
# Copy all skills to Claude Code skills directory
cp -r skills/* ~/.claude/skills/
```

### Single skill

```bash
# Example: install only seo-audit
mkdir -p ~/.claude/skills/seo-audit
cp skills/seo-audit/SKILL.md ~/.claude/skills/seo-audit/
```

### Per project

```bash
# Copy to project's .claude directory
cp -r skills/* .claude/skills/
```

## Skill Details

### `/seo-audit` — Technical SEO Site Audit
- Crawls all pages via sitemap.xml + internal link discovery
- 200+ technical SEO checks across 12 weighted categories
- Page-by-page error reporting with P0–P3 priority levels
- AI/LLM readiness checks (llms.txt, AI crawler policies)
- Weighted scoring system (100-point scale)

### `/content-seo` — SEO Content Writer
- Keyword research and search intent analysis
- E-E-A-T compliant content creation
- Multiple page types: blog, service, product, landing, FAQ
- Multilingual support (TR, EN, DE, ES, RU, ZH, FR, and more)
- Auto-generates meta tags, slugs, OG tags, alt text suggestions
- Internal linking recommendations and content cluster strategy

### `/schema-gen` — Structured Data Generator
- 12+ schema types: Organization, Article, Product, FAQ, HowTo, MedicalProcedure, Event, Video, Service, Person, BreadcrumbList, WebSite
- Google Rich Results Test compatible
- @graph support for combining multiple schemas
- Auto-detects page type from URL
- Copy-paste ready JSON-LD output

### `/wp-performance` — WordPress Performance Optimizer
- HTML source analysis (DOM size, CSS/JS count, render-blocking resources)
- Core Web Vitals evaluation (LCP, CLS, INP signals)
- Server-specific recommendations (LiteSpeed, Apache, Nginx, Cloudflare)
- Image, CSS, JS, database, plugin, and theme optimization
- Prioritized action plan (5-minute fixes to monthly improvements)

### `/wp-doctor` — WordPress Troubleshooter
- 15+ error type database (WSOD, 500, 502, 503, redirect loops, DB errors, SMTP, etc.)
- Step-by-step diagnosis protocol
- Plugin conflict resolution workflow
- WooCommerce and Elementor specific troubleshooting
- Copy-paste ready fix code (wp-config.php, .htaccess, functions.php)

### `/project-init` — Project Scaffolding
- Supports WordPress, AstroJS, Next.js, and static HTML
- Creates CLAUDE.md with project-specific rules
- Creates .cursorrules for Cursor AI IDE
- Git initialization with proper .gitignore
- Working starter files (not empty templates)

### `/deploy-check` — Pre-Launch Checklist
- 11 categories, 100+ checks
- DNS, SSL, functionality, content, SEO, performance, security
- Legal compliance (KVKK for Turkey, privacy policy, cookie consent)
- Analytics setup verification (GA4, GTM, Meta Pixel)
- WordPress and e-commerce specific checks
- GO / NO-GO decision with scoring

## Requirements

- [Claude Code](https://claude.com/claude-code) CLI
- Internet access (for WebFetch in audit skills)

## License

MIT

## Contributing

Contributions welcome! Open issues or PRs for new skills, updated criteria, or improvements.
