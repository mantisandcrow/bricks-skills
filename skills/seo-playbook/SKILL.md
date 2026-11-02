---
name: seo-playbook
description: SEOPress Execution Methodology — Reusable Playbook
---

# SEOPress Execution Methodology — Reusable Playbook

> Standard methodology for deploying SEOPress (Free + PRO) on any WordPress site.

## Phase 0: Pre-Installation

1. Uncheck "Discourage search engines" — WP Settings → Reading → uncheck `blog_public`
2. Verify canonicals work — confirm self-referencing canonicals survive domain change
3. Confirm production domain — DNS pointed and SSL active
4. Note current state — document existing noindex/nofollow settings

## Phase 1: Install & Activate

1. Install SEOPress Free from WordPress.org
2. Activate
3. Install SEOPress PRO (upload zip)
4. Activate PRO add-on
5. Enter license key (SEO → License)
6. Run installation wizard (6 steps):
   - Step 1: Site type
   - Step 2: Organization/Person
   - Step 3: Social accounts
   - Step 4: Analytics (skip for now)
   - Step 5: Sitemaps (enable all)
   - Step 6: Title & meta defaults

## Phase 2: Core Settings — Titles & Metas

### Global Defaults
- Set separator character (en dash `—` recommended)
- Configure site title and alternative site title
- Set meta description for homepage

### Post Types
- Configure title templates for each post type: `%%title%% — %%site_title%%`
- Set display date on/off per content type
- Ensure Noindex is Off for all public content

### Taxonomies
- Title template: `%%term_title%% — %%site_title%%`
- Meta description templates using `%%term_title%%` variable

### Archives
- Disable author archives on single-author sites
- Disable date archives if not needed
- Noindex search archives

### Advanced
- Noindex entire site: Off
- Noindex paginated archives: On
- Noindex attachment pages: On
- Remove WordPress generator tag: On
- Remove shortlink: On
- Remove RSD: On
- Remove oEmbed links: On
- Remove X-Pingback: On
- Remove emoji support: On
- Remove `?replytocom`: On
- Remove `/category/` from URL: On

## Phase 3: XML Sitemaps

1. Enable all sitemap types (Posts, Pages, Custom Post Types, Taxonomies)
2. Enable Image sitemap
3. Enable Video sitemap (if applicable)
4. Set max URLs per sitemap (1000 default)
5. Ping search engines on update: On

## Phase 4: HTML Sitemap

1. Create HTML sitemap page
2. Configure HTML sitemap display settings
3. Add to footer or navigation

## Phase 5: Open Graph & Social

1. Enable Open Graph meta tags
2. Set default og:image
3. Enable Twitter/X Card meta tags
4. Set default card type (summary_large_image)
5. Configure Facebook App ID if available
6. Configure Knowledge Graph (Person or Organization)

## Phase 6: Schema / Structured Data

1. Enable schema markup
2. Set default schema type (WebSite for homepage, Article for posts)
3. Configure schema for each content type
4. Add SameAs links for social profiles
5. Test with Google Rich Results Test

## Phase 7: Analytics

1. Connect Google Analytics 4 (GA4)
2. Set up Microsoft Clarity (heatmaps)
3. Configure cookie bar / GDPR consent
4. Exclude logged-in users from tracking

## Phase 8: Redirects & 404

1. Enable 301 redirect manager
2. Set up redirect monitoring
3. Configure 404 error tracking
4. Create custom 404 page

## Phase 9: Breadcrumbs

1. Enable breadcrumbs
2. Configure separator and template
3. Add schema.org markup to breadcrumbs
4. Style to match site design

## Phase 10: Image SEO

1. Enable alt text auto-generation
2. Enable title attribute auto-generation
3. Configure image filename cleanup
4. Set up lazy loading

## Phase 11: Advanced Cleanup

1. Remove /category/ from URLs
2. Disable author/type archives if not needed
3. Remove unnecessary WordPress head tags
4. Clean up wp_head actions

## Phase 12: Agent Readiness / llms.txt

1. Enable llms.txt generation
2. Write custom content covering:
   - Site purpose and key topics
   - Selected works or highlights
   - Contact information
3. Enable Agent Readiness toggle (PRO)

## Post-Launch Verification Checklist

- [ ] Site appears in Google search
- [ ] XML sitemap loads and is valid
- [ ] HTML sitemap loads and is correct
- [ ] Open Graph tags render correctly (Facebook debugger)
- [ ] Twitter Card validator passes
- [ ] Schema markup validates (Google Rich Results Test)
- [ ] GA4 receiving data
- [ ] 301 redirects working
- [ ] 404 page displays correctly
- [ ] Breadcrumbs display and have schema
- [ ] llms.txt is accessible at /llms.txt
- [ ] All pages have unique titles and descriptions
- [ ] No duplicate content issues
- [ ] Mobile-friendly (Google Mobile-Friendly Test)
- [ ] Page speed acceptable (Google PageSpeed Insights)
