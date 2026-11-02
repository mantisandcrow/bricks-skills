---
name: aeo-playbook
description: AEO Playbook — Answer Engine Optimization
---

# AEO Playbook — Answer Engine Optimization

> Preparing websites for AI search engines, LLM crawlers, and agent-based discovery.

## What is AEO?

AEO (Answer Engine Optimization) ensures your content is discoverable and accurately represented by AI search engines like ChatGPT, Perplexity, Google SGE, and other LLM-powered tools. It complements traditional SEO by focusing on how AI agents read, understand, and surface your content.

## llms.txt Configuration

### What is llms.txt?
A machine-readable file at the root of your site that tells LLMs:
- What the site is about
- Key topics and content
- How to navigate the site
- Contact information

### Standard llms.txt Structure

```
# Site Name

> Brief description of the site and its purpose

## Key Topics
- Topic 1: Description
- Topic 2: Description

## Selected Works / Highlights
- [Title](URL): Brief description
- [Title](URL): Brief description

## Contact
- Email: contact@example.com
- Website: https://example.com
```

### Implementation via SEOPress

1. SEO → Agent Readiness → Enable llms.txt
2. Write custom content (do not auto-generate)
3. Include links to key pages
4. Keep under 500 words
5. Update when site content changes significantly

## Agent Readiness (SEOPress PRO)

1. Enable Agent Readiness toggle
2. Configure which content types are exposed
3. Set crawl permissions for AI agents
4. Monitor agent access in logs

## GEO (Generative Engine Optimization)

- Structure content with clear headings and definitions
- Use schema.org markup (especially Article, FAQPage, HowTo)
- Write concise, factual paragraphs that LLMs can quote
- Include author bylines and publication dates
- Link related content internally

## AI Search Engine Checklist

- [ ] llms.txt present at /llms.txt
- [ ] llms.txt contains accurate site description
- [ ] llms.txt links to key pages
- [ ] robots.txt allows AI crawlers (GPTBot, ClaudeBot, etc.)
- [ ] Schema markup is valid and complete
- [ ] Content has clear headings and structure
- [ ] Author information is present
- [ ] Publication dates are visible
- [ ] Internal linking connects related topics
- [ ] Contact information is accessible
