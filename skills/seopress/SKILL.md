---
name: seopress
description: SEOPress expert agent. Use when configuring, troubleshooting, or optimizing SEOPress (Free/PRO/Insights) on WordPress. Covers all features, SEO best practices, AI integration, schemas, sitemaps, analytics, WooCommerce SEO, migrations, hooks, and developer APIs. Also use when the user asks about SEO how-to resources from seopress.org.
---

# SEOPress Master Agent Skill

Use this skill when working with SEOPress on any WordPress site — configuring, optimizing, migrating, debugging, or advising on SEO best practices.

---

## Product Overview

SEOPress is a freemium WordPress SEO plugin (350,000+ active installs, 4.8/5 rating on WordPress.org). Made in France by Benjamin Denis since 2017.

### Products

| Product | Purpose | Price |
|---------|---------|-------|
| **SEOPress Free** | Core SEO plugin (titles, sitemaps, social, analytics, redirects) | Free |
| **SEOPress PRO** | Premium add-on (AI, schemas, site audit, GSC, breadcrumbs, WooCommerce SEO, broken links, 404 monitoring, redirects manager) | From $49/yr (1 site), $149/yr unlimited |
| **SEOPress Insights** | Off-site SEO (rank tracker, backlinks monitor, Google Trends) | Separate license |
| **SEOPress AI Credits** | AI generation without needing provider API keys | Add-on to PRO |
| **SEOPress for MainWP** | Multi-site management add-on | Free |

### Key Differentiators
- **Privacy by design**: No telemetry, no ads, no anonymous data collection, fully white label
- **All-in-one**: No need for separate redirect, schema, or sitemap plugins
- **Universal SEO metabox**: Works in Gutenberg, Elementor, Divi, Bricks, Oxygen, Breakdance, Beaver Builder, WPBakery, Avada, Kadence
- **650+ hooks**: Fully filterable for developers
- **REST API + WP-CLI**: Headless and automation ready
- **Translated into 27+ languages** with professional translations

---

## Free vs PRO Feature Matrix

### SEOPress Free Features
- Installation wizard (6 steps)
- Universal SEO metabox (titles, descriptions, OG, X Cards, robots, canonical)
- Content analysis with unlimited target keywords
- Mobile & desktop Google preview
- Facebook & X social preview
- Titles & meta descriptions with dynamic variables (custom fields, terms, taxonomies)
- Open Graph & X (Twitter) Cards
- Google Knowledge Graph (Organization data)
- llms.txt & Agent Readiness (AEO/GEO)
- Google Analytics 4 & Matomo tracking
- Microsoft Clarity integration
- Custom canonical URLs and meta robots (noindex, nofollow, noimageindex, nosnippet)
- XML sitemaps (posts, pages, CPTs, taxonomies, images, authors)
- HTML sitemap
- Image XML sitemap
- Redirections at post/page/CPT level
- URL clean-up (remove /category/, /product-category/, ?replytocom)
- Image SEO (auto-set title, alt, caption, description)
- Google Indexing API & IndexNow (Bing/Yandex)
- Import/export settings
- One-click migration from 11+ SEO plugins
- White label (free!)
- GDPR/cookie consent bar
- Search engine verification (Google, Bing, Pinterest, Yandex, Baidu)

### SEOPress PRO Additional Features
- **AI SEO**: Generate titles, descriptions, OG/X tags, alt text with OpenAI, Gemini, Claude, Mistral, DeepSeek
- **AI Assistant**: Conversational chatbot in block editor
- **AI on autopilot**: Auto-generate metadata on publish (posts + taxonomy terms)
- **Site Audit**: 52 tests across 13 categories, GSC-integrated
- **SEO Alerts**: Daily email/Slack warnings for noindex, robots.txt, sitemap failures
- **Google Search Console**: Clicks, impressions, CTR, position in post lists
- **Google Suggestions**: Long-tail keyword discovery in content analysis
- **Google PageSpeed**: Core Web Vitals reports in dashboard
- **Redirect Manager**: Unlimited 301/302/307/410/451, regex, CSV import/export, categories
- **404 Monitoring**: Auto-redirect suggestions, email notifications
- **Broken Link Checker**: CRON-based batch scanning
- **Schema/JSON-LD Editor**: 15+ schema types with live preview
- **Automatic Schemas**: Advanced conditions (AND/OR, post types, taxonomies)
- **Breadcrumbs**: Schema.org, A11Y-ready, customizable, FSE block
- **Local SEO**: Local Business widget/block with opening hours
- **WooCommerce SEO**: Product schema (GTIN, MPN, brand), Enhanced Ecommerce, OG price/currency, noindex cart/checkout
- **Easy Digital Downloads** integration
- **Video XML Sitemap**: Automatic YouTube discovery
- **Google News XML Sitemap**
- **Internal Linking Suggestions**
- **robots.txt & .htaccess editor**: Multisite/multidomain ready
- **Custom RSS feed options**
- **Multilingual llms.txt** with TranslatePress
- **Command Palette** (Cmd/Ctrl+K): 240+ indexed entries
- **Portable Settings**: Export reusable config without site-specific data
- **Bulk Actions**: Generate metadata in bulk
- **CSV Import/Export**: Metadata, redirections
- **Revision History**: robots.txt version comparison
- **Block Editor Blocks**: FAQ, How-to, Local Business, Breadcrumbs, Table of Contents

### SEOPress Insights Features
- Keyword rank tracker (52 Google locations)
- Track 50 keywords/site daily
- Competitor tracking
- Backlinks monitored weekly (up to 1,000)
- Google Trends integration
- Lifetime data access (CSV/PDF/Excel export)
- Email & Slack alerts

---

## Feature Deep Dives

### 1. Titles & Metas

**Global Settings** (SEO > Titles & Metas):
- **Home**: Title template, separator, site title, alternative site title, meta description
- **Post Types**: Title/meta templates for posts, pages, CPTs; noindex/nofollow per type; display date; display post thumbnail
- **Taxonomies**: Title/meta for categories, tags, custom taxonomies; noindex recommended for tags
- **Archives**: Author archives (disable if single author), date archives (disable recommended), search archives (noindex), 404 page
- **Advanced**: Global noindex/nofollow/noimageindex/nosnippet; remove website schema; rel next/prev; noindex paginated archives; noindex attachment pages

**Per-Post/Page** (Universal SEO Metabox):
- Custom title with dynamic variables
- Custom meta description
- Social: Facebook title/description/thumbnail, X title/description/thumbnail
- Advanced: noindex, nofollow, nosnippet, noimageindex, canonical URL
- Redirection: Enable, type (301/302/307), login status, target URL
- Content Analysis: Target keywords, analysis criteria

**Dynamic Variables**:
- `%%post_title%%`, `%%post_title_trimmed%%`, `%%site_title%%`, `%%site_title_alt%%`
- `%%sep%%`, `%%current_pagination%%`, `%%search_keywords%%`
- `%%post_category%%`, `%%post_tag%%`, `%%_cf_custom_field%%`, `%%_ucf_user_custom_field%%`
- `%%ct_custom_taxonomy_slug%%`, `%%wc_single_cat%%`, `%%wc_single_tag%%`
- `%%seopress_titles_post_url%%`, `%%seopress_titles_post_thumbnail_url%%`
- Custom global dynamic variables via hooks

### 2. XML & HTML Sitemaps

**XML Sitemap** (SEO > XML - HTML Sitemap > General):
- Enable XML sitemap (auto-disables WordPress native sitemaps)
- Enable Image sitemap (standard, galleries, featured, WooCommerce)
- Enable Video sitemap (PRO)
- Enable Author sitemap
- Enable Google News sitemap (PRO)

**Post Types tab**: Include/exclude posts, pages, media, CPTs
**Taxonomies tab**: Include/exclude categories, tags, custom taxonomies

**HTML Sitemap**:
- Enter post/page/CPT ID(s) to display
- Exclude specific IDs
- Sort order (alphabetical, date, ID, menu, etc.)
- Order posts by
- Disable publication date display
- Disable hierarchy for posts/products
- Shortcode: `[seopress_html_sitemap cpt="post,page"]`
- Block Editor block available

**Sitemap URL**: `yourdomain.com/sitemap_index.xml`

### 3. Social Networks

**Knowledge Graph** (SEO > Social Networks):
- Person or Organization
- Name, photo/logo, description
- Email, phone, contact type, contact option, VAT ID

**Social Accounts**: Facebook, X, Pinterest, Instagram, YouTube, LinkedIn, additional accounts, Fediverse/Mastodon

**Facebook (Open Graph)**:
- Enable OG data
- Default image (1640x856px)
- Apply to all og:image tags
- Facebook Link Ownership ID, Admin ID, App ID

**X (Twitter) Cards**:
- Enable X Cards
- Use Open Graph fallback
- Default image (300x157 or 600x314px)
- Card size: summary or summary_large_image

**LinkedIn**: Post thumbnail image size

### 4. Analytics

**Google Analytics** (SEO > Analytics):
- Enable GA4 tracking (gtag.js)
- Enter Measurement ID
- Enable Google Ads
- Events: External links, downloads, affiliate/outbound links, phone links
- Custom dimensions: Authors, categories, tags, post types, logged-in users
- Exclude user roles from tracking

**Matomo**: Cloud or self-hosted, site ID, DoNotTrack, cookies, cross-domain

**Microsoft Clarity**: Enable + project ID

**Cookie Bar / GDPR**:
- Load position (body/footer/head)
- Opt-in tracking
- Auto-accept (not GDPR-compliant)
- Allow user to change choice
- Customizable message, buttons, styling

**Custom Tracking**: HEAD, BODY, BODY (FOOTER) additional tracking code (for GTM etc.)

### 5. Instant Indexing

- Google Indexing API + Bing Indexing API + IndexNow
- Submit up to 100 URLs at once
- Auto-notify on publish/update/delete (IndexNow)
- Action type: update or remove URLs

### 6. Advanced / Image SEO

**Image SEO**:
- Redirect attachment pages to parent or file URL
- Clean media filename (remove accents, capitals, spaces)
- Auto-set image title, alt text, caption, description from filename
- Auto-set alt from target keywords
- Update alt on already-inserted images

**Advanced Settings**:
- Remove /category/ and /product-category/ from URLs
- Remove ?replytocom, noreferrer, generator tag, hentry, shortlink, RSD, oEmbed, X-Pingback, X-Powered-By, emoji support
- Remove website field in comment form
- Add nofollow to comment form links
- Search engine verification: Google, Bing, Pinterest, Yandex, Baidu

### 7. AI Integration (PRO)

**Supported AI Providers**:
- OpenAI (GPT models)
- Google Gemini (3 Flash, 3.1 Pro)
- Anthropic Claude (Sonnet, Opus)
- Mistral AI (Mistral, Pixtral)
- DeepSeek AI (V4 models)
- SEOPress AI Credits (managed gateway, no API key needed)

**AI Features**:
- Generate meta title + description (single or bulk)
- Generate Open Graph + X Card tags
- Generate image alt text, caption, description (bulk supported)
- AI Assistant chatbot (block editor)
- Auto-generate on publish (posts + taxonomy terms)
- Block Editor toolbar: shorten, expand, fix SEO, fix grammar, translate, rewrite
- WP-CLI AI commands
- Custom AI instructions (tone of voice)
- Restrict AI to specific user roles
- AI Logs panel (error tracking with status codes)

**AI Credits**:
- One license token, best models auto-selected
- No separate provider accounts needed
- Balance displayed in SEOPress dashboard
- Non-refundable, do not roll over
- Features pause when credits exhausted (can switch to own provider)

**Privacy**: Only post content (trimmed to 500 words), language, and target keywords sent. Content never used for training.

### 8. Agent Readiness / llms.txt (PRO)

- **llms.txt**: Markdown-formatted file at site root helping LLMs discover key content
- **Agent Readiness toggle**: One click enables:
  - Clean text versions of pages (no menus/popups)
  - Sitemap + llms.txt for agents
  - Blocks training bots, allows citation bots
  - robots.txt rules for AI crawlers
- Improves AEO (Answer Engine Optimization) and GEO (Generative Engine Optimization)

### 9. Schema / Structured Data Types (PRO)

**15+ Schema Types**:
- Article (Automatic/Manual)
- Local Business (Automatic/Manual) + Widget/Block
- Product (Automatic/Manual) - with GTIN, MPN, brand, sale price, merchant return policy
- ProductGroup (variable products)
- Event (Automatic/Manual)
- Course (Automatic/Manual)
- Recipe (Automatic/Manual)
- JobPosting (Manual)
- FAQ (Automatic/Manual) + Block
- How-to (Manual) + Block
- Video (Automatic/Manual)
- Service (Automatic/Manual)
- Review (Automatic/Manual)
- SoftwareApplication (Automatic/Manual)
- Custom Schema (JSON-LD editor)
- ProfilePage (User profiles)

**Schema Features**:
- Live preview
- Advanced conditions (AND/OR, post types, taxonomies)
- Import/export schemas
- Dynamic variables in custom schema fields
- Manual tab listing all content with manually assigned schemas

### 10. Redirect Manager (PRO)

- Unlimited 301/302/307/410/451 redirects
- Regex support
- URL tester modal
- Categories for redirects
- Auto-suggest redirects on slug change or content deletion
- 404 monitoring with email notifications
- Import/export: CSV, htaccess, from Yoast/Rank Math/AIOSEO/SmartCrawl/Redirections plugin/Slim SEO
- User capabilities management

### 11. Breadcrumbs (PRO)

- Schema.org JSON-LD markup
- Accessible (A11Y-ready)
- Live preview
- Customizable per CPT/term
- HTML or JSON-LD format
- Block Editor block for FSE
- Translation support

### 12. Site Audit (PRO)

- 52 tests across 13 categories:
  - Canonical URL, Structured data types, Last modified date
  - Keywords in permalink, Headings, Meta title, Meta description
  - Social meta tags, Meta robots, Alternative texts of images
  - NoFollow Links, Outbound Links, Internal Links
- GSC integration (clicks + position per issue)
- AI alt text fixes from audit
- 5 minutes for 1,000 URLs
- Email alert on completion
- REST API for third-party integration
- CSV export
- Ignore irrelevant issues

### 13. WooCommerce SEO (PRO)

- Product schema with global identifiers (GTIN, MPN, brand)
- ProductGroup schema for variable products
- Sale price + merchant return policy in schema
- OG price & currency
- XML sitemaps for products + images
- Centralized noindex: cart, checkout, account, thank-you pages
- Remove WooCommerce generator meta tag
- Breadcrumbs with WooCommerce support
- Google Enhanced Ecommerce: purchases, product views, cart events, add-to-cart, remove-from-cart
- WooCommerce product attributes in metadata

### 14. White Label / GDPR (Free + PRO)

- Replace plugin name, logo, menus, admin bar, screens
- No footprints in source code
- No ads, no telemetry
- Cookie bar with consent management
- Analytics opt-in before tracking
- User consent cookie expiration

### 15. Block Editor Integration

**Free Blocks**:
- FAQ (with schema)
- Sitemap (HTML)
- Google Preferred Sources button

**PRO Blocks**:
- FAQ (enhanced)
- How-to
- Local Business
- Breadcrumbs
- Table of Contents

### 16. Developer APIs

**REST API**:
- Read/write SEO metadata
- Site audit data
- Sitemap management
- Redirections management
- Schema management
- Full endpoints documented

**WP-CLI**:
- Generate metadata with AI
- Manage titles, descriptions, robots
- Import/export operations
- Bulk operations

**650+ Hooks** (Actions & Filters):
- **Meta**: filter meta title, description, robots, canonical, Dublin Core, article tags
- **Sitemap**: filter queries, URLs, headers, XSL, cache duration
- **Social**: filter OG title/description/image/type, X Card tags, locale
- **Analytics**: filter GA/Matomo/Clarity tracking code, custom dimensions, consent
- **Breadcrumbs**: filter HTML, JSON, separator, CSS, classes, crumbs
- **Schema**: filter all automatic/manual schemas (product, local business, FAQ, article, etc.)
- **Redirections**: filter queries, taxonomies, export, auto-redirect suggestions
- **Image SEO**: filter filename cleaning, auto alt/title/caption
- **AI**: filter prompts, arguments, HTTP requests for all AI providers
- **Sitemap**: filter post types, taxonomies, URLs, queries, Google News
- **Appearance**: filter admin bar, menus, widgets, metabox positions

---

## Integrations (50+)

### Page Builders
Elementor, Divi, Bricks, Oxygen, Breakdance, Beaver Builder, WPBakery, Avada, Kadence, SiteOrigin, Visual Composer, Thrive Themes Builder, Brizy

### E-commerce
WooCommerce, Easy Digital Downloads, Ecwid, SureCart

### Translation
WPML, Polylang, TranslatePress, Weglot, Multilingual Press

### Performance
WP Rocket, LiteSpeed Cache

### Analytics
Google Analytics, Matomo, Microsoft Clarity

### AI Providers
OpenAI, Google Gemini, Claude (Anthropic), Mistral AI, DeepSeek

### Custom Fields
Advanced Custom Fields (ACF), JetEngine, MetaBox, Toolset

### Community
BuddyPress, BuddyBoss, bbPress, wpForo

### Management
MainWP, WP Reset

### Other
Jetpack, Events Calendar, GeoDirectory, LifterLMS, WP Job Manager, Permalink Manager, Admin Columns Pro, Stackable, Gato GraphQL, Notion WP Sync, Bit Flows, Story Chief, WP Search with Algolia

---

## Migration From Other SEO Plugins

SEOPress supports one-click migration from:
- Yoast SEO (posts, terms, global settings, social profiles, feeds)
- All In One SEO (AIOSEO)
- Rank Math
- The SEO Framework
- Slim SEO
- SmartCrawl
- Squirrly SEO
- SEO Ultimate
- WP Meta SEO
- Premium SEO Pack
- SiteSEO
- SureRank

**What's imported**: Titles, meta descriptions, Open Graph, X Cards, robots meta tags (noindex/nofollow), canonical URLs, redirects, breadcrumbs, global settings

**Migration time**: ~5 min for <1,000 articles, 15-30 min for up to 50,000 articles

**Safety**: Original metadata never deleted from database. Reactivate old plugin to restore.

---

## SEO Best Practices (from SEOPress Guides)

### Getting Started
1. Run the installation wizard after activating SEOPress
2. Connect Google Search Console and Google Analytics
3. Verify site with search engines (Google, Bing, Pinterest)
4. Generate XML sitemaps and submit to GSC
5. Set up Knowledge Graph (Organization or Person)

### On-Page SEO
- Write unique title tags (50-60 characters) with target keyword near the beginning
- Write compelling meta descriptions (150-160 characters) with call-to-action
- Use dynamic variables for consistent templates
- Set canonical URLs to prevent duplicate content
- Use noindex for low-value pages (tag archives, search results, internal search)
- Optimize images: descriptive file names, alt text, captions

### Technical SEO
- Ensure XML sitemaps are working and submitted to GSC
- Set up 301 redirects for changed URLs
- Monitor 404 errors and fix or redirect
- Use breadcrumbs for navigation and schema
- Remove unnecessary URL parameters (?replytocom, etc.)
- Clean up /category/ and /product-category/ from URLs
- Redirect attachment pages to parent post or file URL

### Content Analysis
- Define target keywords for each post
- Analyze content against SEO criteria
- Check internal/external links
- Verify heading structure (H1, H2, H3...)
- Ensure images have alt text
- Use Google Suggestions for long-tail keywords

### Social Optimization
- Set Open Graph tags for Facebook/LinkedIn/Pinterest
- Set X Cards for Twitter
- Use appropriate image sizes (1640x856 for OG, 600x314 for X)
- Enable Knowledge Graph for brand visibility

### WooCommerce SEO
- Add product schema with identifiers (GTIN, MPN, brand)
- Noindex cart, checkout, account pages
- Enable Enhanced Ecommerce tracking
- Optimize product titles and descriptions
- Add OG price and currency for social sharing

### Local SEO
- Set up Local Business schema
- Add business name, address, phone, opening hours
- Use Local Business widget/block on contact page
- Connect Google My Business

### AI / AEO / GEO
- Enable Agent Readiness for AI search visibility
- Generate llms.txt for LLM discovery
- Use AI to generate metadata at scale
- Write content that answers questions directly (for AI citation)

---

## Troubleshooting

### Common Issues

**"My title doesn't match the Google preview"**
- Theme may be missing `add_theme_support('title-tag')`
- Fix: Add `add_theme_support('title-tag')` to theme's functions.php
- Guide: https://www.seopress.org/support/guides/fixing-missing-add_theme_support-in-your-theme/

**"XML sitemap returns blank page"**
- Usually a caching conflict
- Exclude XML and XSL files from caching plugins
- Guide: https://www.seopress.org/support/guides/xml-sitemap-blank-page/

**"XML sitemap returns 404"**
- Permalink structure issue
- Flush permalinks (Settings > Permalinks > Save)
- Guide: https://www.seopress.org/support/guides/xml-sitemap-returns-404-error/

**"Google uses wrong meta title/description"**
- Google sometimes rewrites snippets
- Ensure title/description are compelling and accurate
- Guide: https://www.seopress.org/support/guides/google-uses-the-wrong-meta-title-meta-description-in-search-results/

**"429 error with AI"**
- Rate limiting from AI provider
- Wait and retry, or use SEOPress AI Credits
- Guide: https://www.seopress.org/support/guides/generate-your-seo-metadata-with-openai/

**"Download failed. Unauthorized" when updating PRO**
- License key issue
- Re-enter license key in SEO > License
- Guide: https://www.seopress.org/support/guides/an-error-occurred-while-updating-seopress-pro-download-failed-unauthorized/

**"Structured data errors in Search Console"**
- Validate schema at Google Rich Results Test
- Check required fields are present
- Guide: https://www.seopress.org/support/tutorials/how-to-add-schema-to-wordpress-with-seopress-1/

**"LiteSpeed caching conflict"**
- Exclude SEOPress-related files from LiteSpeed cache
- Guide: https://www.seopress.org/support/guides/fix-compatibility-issue-with-litespeed-caching-plugin/

---

## SEOPress Hooks Reference (Top Hooks)

### Meta Tags
- `seopress_titles_title` — Filter meta title
- `seopress_titles_desc` — Filter meta description
- `seopress_meta_robots` — Filter meta robots attributes
- `seopress_canonical_url` — Filter canonical URL
- `seopress_meta_google_noimageindex` — Filter noimageindex
- `seopress_meta_robots_nosnippet` — Filter nosnippet

### Social
- `seopress_og_title` / `seopress_og_desc` / `seopress_og_thumb` — Filter OG tags
- `seopress_twitter_title` / `seopress_twitter_desc` / `seopress_twitter_thumb` — Filter X Card tags
- `seopress_og_type` — Filter Open Graph type

### Sitemap
- `seopress_sitemaps_single_post_type_query` — Filter single post type sitemap query
- `seopress_sitemaps_single_taxonomy_query` — Filter taxonomy sitemap query
- `seopress_sitemaps_html_sitemap_query` — Filter HTML sitemap query
- `seopress_sitemaps_cache_duration` — Filter sitemap cache duration

### Analytics
- `seopress_google_analytics_tracking` — Filter GA tracking code
- `seopress_matomo_tracking` — Filter Matomo tracking code
- `seopress_clarity_tracking` — Filter Clarity tracking code

### Schema
- `seopress_schema_article` — Filter automatic article schema
- `seopress_schema_product` — Filter automatic product schema
- `seopress_schema_local_business` — Filter local business schema
- `seopress_schema_faq` — Filter automatic FAQ schema
- `seopress_schema_custom` — Filter custom schema

### Breadcrumbs
- `seopress_breadcrumbs_html` — Filter breadcrumbs HTML
- `seopress_breadcrumbs_json` — Filter breadcrumbs JSON-LD
- `seopress_breadcrumbs_separator` — Filter breadcrumb separator

### AI
- `seopress_ai_credits_model` — Pin a specific AI model
- `seopress_ai_prompt_title` — Filter prompt for title generation
- `seopress_ai_prompt_description` — Filter prompt for description generation
- `seopress_ai_prompt_alt_text` — Filter prompt for alt text generation

### Redirections
- `seopress_redirections_post_types` — Filter post types watched for auto-redirects
- `seopress_redirections_taxonomies` — Filter taxonomies watched for auto-redirects

---

## WP-CLI Commands

```bash
# Generate SEO metadata with AI
wp seopress ai generate --post_id=123 --type=title
wp seopress ai generate --post_id=123 --type=description
wp seopress ai generate --all --type=title,description

# Manage titles and descriptions
wp seopress title get --post_id=123
wp seopress title set --post_id=123 --title="My Title"
wp seopress desc set --post_id=123 --description="My description"

# Manage robots
wp seopress robots get --post_id=123
wp seopress robots set --post_id=123 --robots="noindex,nofollow"

# Sitemaps
wp seopress sitemap regenerate

# Redirections
wp seopress redirect add --source="/old-url" --target="/new-url" --type=301
wp seopress redirect list

# Import/Export
wp seopress export
wp seopress import --file=settings.json
```

---

## REST API Endpoints

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/wp-json/seopress/v1/title` | GET/POST | Read/write title |
| `/wp-json/seopress/v1/description` | GET/POST | Read/write description |
| `/wp-json/seopress/v1/robots` | GET/POST | Read/write robots |
| `/wp-json/seopress/v1/canonical` | GET/POST | Read/write canonical |
| `/wp-json/seopress/v1/og` | GET/POST | Read/write Open Graph |
| `/wp-json/seopress/v1/schema` | GET/POST | Read/write schema |
| `/wp-json/seopress/v1/redirects` | GET/POST/DELETE | Manage redirections |
| `/wp-json/seopress/v1/audit` | GET | Site audit data |
| `/wp-json/seopress/v1/sitemap` | GET | Sitemap data |

---

## Free SEO Ebooks by SEOPress

1. **Unlock the Future of SEO Copywriting with AI** — https://www.seopress.org/support/ebooks/unlock-the-future-of-seo-copywriting-with-ai-your-ultimate-guide/
2. **Getting SEO Right for Your Very First Site** — https://www.seopress.org/support/ebooks/getting-seo-right-for-your-very-first-site/
3. **How to Survive an SEO Emergency** — https://www.seopress.org/support/ebooks/how-to-survive-an-seo-emergency-free-guide-for-website-owners/
4. **SEO Success with a Two-Hours-a-Week Routine** — https://www.seopress.org/support/ebooks/seo-success-for-wordpress-with-a-two-hours-a-week-routine/
5. **Maximizing WordPress SEO with Google Search Console** — https://www.seopress.org/support/ebooks/maximizing-your-wordpress-seo-with-google-search-console/
6. **Analyze Your Audience with Google Analytics** — https://www.seopress.org/support/ebooks/analyze-your-audience-with-google-analytics/
7. **More Visibility with Image SEO** — https://www.seopress.org/support/ebooks/more-visibility-with-image-seo/
8. **Improve Your Rankings with On-Page SEO** — https://www.seopress.org/support/ebooks/improve-your-rankings-with-on-page-seo/
9. **Optimizing WordPress for Speed** — https://www.seopress.org/support/ebooks/optimizing-wordpress-for-speed/
10. **Keywords and SEO: Everything You Need to Know** — https://www.seopress.org/support/ebooks/keywords-and-seo-everything-you-need-to-know/
11. **WooCommerce SEO: The Ultimate Guide** — https://www.seopress.org/support/ebooks/woocommerce-seo-ultimate-guide/
12. **International SEO with WordPress** — https://www.seopress.org/support/ebooks/international-seo-with-wordpress/
13. **SEOPress Insights** — https://www.seopress.org/support/ebooks/seopress-insights/
14. **Link Building with WordPress** — https://www.seopress.org/support/ebooks/link-building-with-wordpress/
15. **Master Google Structured Data Types (Schemas)** — https://www.seopress.org/support/ebooks/master-google-structured-data-types-schemas/
16. **Improving Your Local SEO Using WordPress** — https://www.seopress.org/support/ebooks/improving-your-local-seo-using-wordpress/
17. **Introduction to WordPress SEO** — https://www.seopress.org/support/ebooks/introduction-to-wordpress-seo/

---

## Key Resource Links

| Resource | URL |
|----------|-----|
| SEOPress Free | https://www.seopress.org/wordpress-seo-plugins/free/ |
| SEOPress PRO | https://www.seopress.org/wordpress-seo-plugins/pro/ |
| SEOPress Insights | https://www.seopress.org/wordpress-seo-plugins/insights/ |
| SEOPress AI Credits | https://www.seopress.org/wordpress-seo-plugins/seopress-ai-credits/ |
| Pricing | https://www.seopress.org/pricing/ |
| All Features | https://www.seopress.org/features/ |
| Guides | https://www.seopress.org/support/guides/ |
| Starter Guides | https://www.seopress.org/support/starter-guides/ |
| Hooks Reference | https://www.seopress.org/support/hooks/ |
| SEO Ebooks | https://www.seopress.org/support/ebooks/ |
| FAQ | https://www.seopress.org/support/faq/ |
| SEO Glossary | https://www.seopress.org/support/guides/wordpress-seo-glossary/ |
| Changelogs | https://www.seopress.org/support/changelogs/ |
| Integrations | https://www.seopress.org/integrations/ |
| GitHub | https://github.com/wp-seopress |
| YouTube | https://www.youtube.com/seopress |
| Facebook Group | https://www.facebook.com/groups/seopress/ |
| WordPress.org | https://wordpress.org/plugins/wp-seopress/ |
| Free vs PRO | https://www.seopress.org/seopress-free-vs-pro/ |
| Migrate From Other Plugins | https://www.seopress.org/solutions/migrate-from/ |
| White Label | https://www.seopress.org/features/white-label/ |
| AI Features | https://www.seopress.org/features/openai/ |
| Site Audit | https://www.seopress.org/features/site-audit/ |
| Local SEO | https://www.seopress.org/features/local-seo/ |
| WooCommerce SEO | https://www.seopress.org/features/woocommerce-seo/ |
| Sitemaps | https://www.seopress.org/features/sitemaps/ |
| Redirections | https://www.seopress.org/features/301-redirects/ |
| Breadcrumbs | https://www.seopress.org/features/breadcrumbs/ |
| Structured Data | https://www.seopress.org/features/structured-data-types/ |
| Google Analytics | https://www.seopress.org/features/google-analytics/ |
| Google Search Console | https://www.seopress.org/features/google-search-console/ |
| Instant Indexing | https://www.seopress.org/features/instant-indexing/ |
| Image SEO | https://www.seopress.org/features/image-seo/ |
| Social Media | https://www.seopress.org/features/social-media/ |
| Content Analysis | https://www.seopress.org/features/content-analysis/ |
| SEO Title & Meta Tags | https://www.seopress.org/features/seo-title-meta-tags/ |
| Block Editor Integration | https://www.seopress.org/features/block-editor-gutenberg/ |
| Page Builders Integration | https://www.seopress.org/features/page-builders-integration/ |
| SEO Alerts | https://www.seopress.org/features/seo-alerts/ |
| PageSpeed | https://www.seopress.org/features/google-page-speed/ |
| Keyword Rank Tracker | https://www.seopress.org/features/keyword-rank-tracker/ |
| Agent Readiness | https://www.seopress.org/support/guides/agent-readiness/ |
| llms.txt | https://www.seopress.org/support/guides/edit-your-llms-txt-file/ |

---

## Quick Reference: Settings Path Map

| Feature | Settings Path |
|---------|--------------|
| Titles & Metas | SEO > Titles & Metas |
| XML Sitemaps | SEO > XML - HTML Sitemap |
| Social Networks | SEO > Social Networks |
| Analytics | SEO > Analytics |
| Instant Indexing | SEO > Instant Indexing |
| Advanced | SEO > Advanced |
| Tools (Import/Export) | SEO > Tools |
| License | SEO > License |
| Dashboard | SEO > Dashboard |
| AI Settings | SEO > AI |
| Schema | SEO > Structured Data Types (PRO) |
| Redirects | SEO > Redirections (PRO) |
| Site Audit | SEO > Site Audit (PRO) |
| Breadcrumbs | SEO > Breadcrumbs (PRO) |
| Local SEO | SEO > Local Business (PRO) |
| WooCommerce SEO | SEO > WooCommerce (PRO) |
| Broken Links | SEO > Broken Links (PRO) |
| 404 Monitoring | SEO > 404 (PRO) |
| SEO Alerts | SEO > SEO Alerts (PRO) |
| White Label | SEO > Advanced > White Label |

---

## Version Notes

- Current version: 10.1 (as of August 2026)
- Requires WordPress 6.5+, PHP 7.4+
- Tested up to WordPress 7.0.4
- Weekly releases
- PRO is an add-on: Free must be installed first
- Compatible with WordPress multisite

---

## When To Use This Skill

- Configuring SEOPress for the first time on a WordPress site
- Migrating from Yoast, Rank Math, AIOSEO, or other SEO plugins
- Setting up AI-powered metadata generation
- Creating or troubleshooting XML sitemaps
- Configuring Open Graph and X Cards for social sharing
- Setting up Google Analytics 4 or Matomo tracking
- Managing 301 redirects and 404 errors
- Adding schema/structured data (Product, Local Business, FAQ, etc.)
- Configuring WooCommerce SEO
- Setting up breadcrumbs
- Running site audits and fixing SEO issues
- Integrating SEOPress with page builders (Elementor, Bricks, Divi, etc.)
- Using WP-CLI or REST API with SEOPress
- Troubleshooting common SEOPress issues
- Advising on SEO best practices using SEOPress tools
- Setting up Agent Readiness for AI search engines
- Configuring llms.txt for LLM visibility
- Using hooks to customize SEOPress behavior
- Setting up white label for client work
