# Doryangel.web.google.studio.v3
DoryAngel Website v3
Project Plan — React + GitHub + n8n
Prepared for Dori Shnaider  •  April 20, 2026  •  v1.0
1. Executive summary
Goal: Replace the current Wix site (doryangel.com, ~$350/yr) with a modern, mobile-first React site hosted on GitHub + Netlify (~$25/yr) while keeping Joy's blog workflow intact and connecting lead capture to the existing n8n automation stack.
Total build time: 7 working days.
Year-one cost: ~$25 vs. $350 on Wix. Savings: ~$325/year.
Outcome: Better mobile UX, full design control, integration with n8n/Airtable, lower cost, no vendor lock-in.
2. Tech stack
Layer
Tool
Cost
Notes
Code
React (single-page app)
$0
Full design control
Version control
GitHub (private repo)
$0
Backup + history
Hosting
Netlify
$0
Auto-deploy on GitHub push
Domain
doryangel.com
$15/yr
Move from Wix registrar
Form handler
n8n webhook
$0
Matches automation stack
Blog source
Google Drive (Markdown)
$0
Joy writes .md files
Blog pipeline
n8n → GitHub → Netlify
$0
Auto-publish on save
Analytics
Plausible (optional)
$9/mo
Privacy-friendly
Portal
Buildium (existing)
Existing
Link out, no rebuild


3. Project phases
Phase 1 — Pre-build decisions (Day 1)
Gather everything before writing code. Output = planning doc in Google Drive.
Content inventory: pull all pages from current Wix site into one master doc
Legal pages: copy Privacy, Disclaimer, SMS consent verbatim (no rewriting)
Blog migration: export 20 Wix posts → convert to Markdown files in Google Drive
Buildium link: confirm doryangel.managebuilding.com as tenant/owner portal URL
Form routing: n8n webhook endpoints defined for each form
Phase 2 — Build (Days 2–4)
React components for every page.
Page
Source
Notes
Home
Rebuilt
Hero, pricing tiers, 6 pillars, stakeholder cards
About / Vision
Migrated
Modernize layout, keep content
Owners
New
Flat-fee pitch, consultation CTA
Tenants
Migrated
Link to Buildium portal
Brokers
Migrated
Partnership pitch
Vendors (new)
New
Contractor partnership pitch
Services Shop
Migrated
3 products (inspection, exterm, app fee)
Portfolio
Migrated
Project showcase
Blog
New
20 posts migrated, Markdown-based
Contact
Rebuilt
Form → n8n webhook
Book Online
Linked
Existing Cal.com link
Privacy Policy
Verbatim
Lawyer-reviewed text from current site
Disclaimer
Verbatim
Lawyer-reviewed text from current site
Sign In / Portal
Linked
External to Buildium


Phase 3 — Blog automation (Day 5)
Google Drive folder is the source of truth. Joy drops Markdown files; n8n publishes them.
Flow
Step 1 — Joy writes post in Google Drive folder as .md file with frontmatter
Step 2 — n8n Google Drive trigger watches folder for new/updated files
Step 3 — n8n optionally calls Claude API for SEO meta + excerpt generation
Step 4 — n8n GitHub node commits file to /content/blog/ in the repo
Step 5 — Netlify webhook detects GitHub push, rebuilds site in ~60 seconds
Step 6 — Post live on doryangel.com/blog
Markdown frontmatter structure
Each .md file starts with:
---title: "Post title"date: 2026-04-20category: "Management" | "Investments"author: "Joy Guevarra"excerpt: "Short summary for blog listing page"image: "/images/post-slug.jpg"---
Phase 4 — Lead capture (Day 6)
Custom React forms post to n8n webhook endpoints. Each form routes to Airtable + Telegram alert.
Form
n8n endpoint
Routes to
Owner inquiry
/webhook/owner-lead
Airtable Leads + Telegram @doryangelbot
Broker inquiry
/webhook/broker-lead
Airtable Leads + Alexa agent follow-up
Vendor application
/webhook/vendor-app
Airtable Vendors table
Newsletter (future)
/webhook/newsletter
TBD email platform


Phase 5 — Legal (Day 6, parallel)
Migrate all legal pages verbatim from current Wix site. Do not rewrite without a lawyer.
Privacy Policy — copy from current Wix site (dated Dec 19, 2025)
SMS consent language (HELP/STOP, TCPA-compliant) — already on current site
Disclaimer — "not a licensed broker" language — already on current site
Terms of Service — verify if current Wix has one, lawyer review if drafting new
Cookie notice — review if needed for EU/CA visitors
Phase 6 — Deploy (Day 7)
Push final code to GitHub private repo
Connect GitHub repo to Netlify (2 clicks)
Netlify auto-deploys on every push
Test everything on staging URL
Point doryangel.com DNS from Wix → Netlify
Keep Wix dormant 30 days as fallback, then cancel
4. Automations — v1 scope
Only these two automations launch with v1. Others move to post-launch roadmap.
#
Automation
Trigger
Action
Value
1
Blog auto-publish
Google Drive .md file added/updated
n8n → GitHub → Netlify rebuild
Joy publishes from familiar workflow; scheduling via file date
2
Lead capture
Owner/broker/vendor form submit
n8n → Airtable + Telegram alert
Instant notification, lead in CRM, zero manual triage


Explicitly out of scope for v1
Tenant maintenance intake on site — handled by Buildium portal link
AI chatbot — move to Month 2 if needed
Newsletter signup — move to Month 2
Dynamic pricing calculator — move to Month 3
Compliance Bot product — separate project
5. Post-launch automation roadmap
Reference list for future iterations. Not part of v1 build.
Tier
Automation
Trigger
When to build
2
AI chatbot on site
Visitor asks question
Month 2
2
Newsletter signup
Email form submit
Month 2
2
Abandoned form recovery
Form start without submit
Month 2
2
Google reviews widget
Weekly cron
Month 2
3
Compliance Bot product
Visitor uploads address
Month 3+
3
Dynamic pricing calculator
Visitor enters unit count
Month 3+
3
Blog SEO auto-optimize
New post published
Month 3+
3
Analytics weekly digest
Weekly cron
Month 3+


6. Cost comparison
Item
Current (Wix)
New (React+GitHub)
Annual delta
Platform + hosting
$350/yr
$0
-$350
Domain
Bundled
$15/yr
+$15
Form handler
Bundled
$0 (n8n)
$0
Blog CMS
Bundled
$0 (GDrive+n8n)
$0
Analytics (optional)
Bundled
$0–108/yr
$0 to +$108
Total
$350/yr
$15–123/yr
-$227 to -$335


Payback: immediate. No upfront migration fee. Monthly ongoing savings fund Month 2 automations.
7. Open decisions
Confirm these before Phase 2 build starts:
Plausible analytics ($9/mo) — yes or GA4 for free
Google Drive folder path where Joy will drop Markdown files
n8n webhook URLs (Dori to provide or generate)
Telegram alert routing (all to @doryangelbot, Chat ID 509562379 — confirm)
Domain migration date (recommended: after 7-day staging test)
Wix cancellation date (recommended: +30 days after go-live)
8. Risks & mitigations
Risk
Mitigation
Joy struggles with Markdown
30-min training + template .md file with frontmatter pre-filled
DNS propagation issues at launch
Do DNS switch on low-traffic day; keep Wix live in parallel 30 days
Legal copy gets out of sync
All legal pages migrated verbatim; lawyer review before go-live
n8n webhook downtime
Form has fallback mailto: link to office@doryangel.com
Buildium portal URL changes
Single source of truth in one config file, easy update
Lost SEO rankings
301 redirects from old Wix URLs to new URLs; keep sitemap.xml


9. Next actions
In priority order:
Dori confirms open decisions above
Claude delivers Phase 1 content inventory doc
Claude + Dori review inventory before Phase 2 build starts
Joy gets Markdown template + 30-min walkthrough
Dori provides or generates n8n webhook URLs

— End of plan —
