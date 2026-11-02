---
name: bricks-playbook
description: Bricks Builder Execution Methodology — Reusable Playbook
---

# Bricks Builder Execution Methodology — Reusable Playbook

> Standard methodology for building WordPress sites with Bricks Builder. Applies to any Bricks project regardless of scope.

## Phase 0: Pre-Build Setup

1. **Install Bricks** — Purchase license from bricksbuilder.io, upload plugin, activate
2. **License Activation** — Bricks → Settings → License → enter key → activate
3. **Enable Builder** — Settings → General → Enable Bricks Builder for your user role
4. **Disable Gutenberg for Bricks** — Settings → Post Types → uncheck Bricks-supported post types in Gutenberg
5. **Set default editor** — User Profile → Bricks Builder as default editor
6. **Configure permalink structure** — Settings → Permalinks → Post name (`/%postname%/`)

## Phase 1: Theme Setup

### Child Theme (Recommended)
1. Create child theme folder: `your-theme-bricks/`
2. Create `style.css` with theme metadata
3. Create `functions.php` with Bricks support:
   ```php
   add_action('after_switch_theme', function() {
       update_option('fresh_theme_fonts', false);
   });
   ```
4. Activate child theme
5. Set homepage and posts page in Settings → Reading

### Direct Theme Installation
1. Upload Bricks theme via Appearance → Themes → Add New → Upload
2. Activate and configure

## Phase 2: Global Settings (Bricks → Settings)

### General
- **Post Types**: Enable Bricks for Posts, Pages, and any custom post types
- **Admin Bar**: Show for your role
- **Google Maps API Key**: Enter if using map elements
- **SVG Support**: Enable for logo and icon uploads

### Builder
- **Maximum nesting level**: 6 (default) — increase for complex layouts
- **Load Google Fonts**: Enable (default) — or disable for self-hosted fonts
- **Save memory limit**: 256M recommended
- **Enable comments**: Disable unless needed
- **Delete Bricks data on uninstall**: Enable for clean removal

### Performance
- **Critical CSS**: Enable — generates above-the-fold CSS automatically
- **Asset versioning**: Enable — busts cache on style changes
- **SVG support**: Enable — allows inline SVG in elements

## Phase 3: Theme Styles

### Global Theme Style
1. Bricks → Settings → Theme Styles
2. Create new theme style: "Global Default"
3. Configure typography:
   - Body: font family, size, line height, color
   - Headings: font family, sizes per level, weight, color
   - Links: color, hover color, underline none
4. Configure colors:
   - Set primary, secondary, accent, text, background colors
   - Use CSS custom properties for consistency
5. Set container width: 1200px (default) or per design
6. Set section padding: 80px top/bottom (adjust per breakpoint)

### Breakpoint Styles
1. Configure breakpoints in Bricks → Settings → Builder → Breakpoints
2. Default breakpoints:
   - Mobile: 767px and below
   - Tablet: 768px – 1024px
   - Desktop: 1025px+
3. Style each breakpoint within the Theme Style
4. Test responsive behavior in builder preview

## Phase 4: Design System Setup

### Color Palette
1. Define brand colors in Theme Styles → Colors
2. Use consistent naming: `--color-primary`, `--color-secondary`, etc.
3. Document in project wiki or design system file

### Typography Scale
1. Define type scale: 12, 14, 16, 18, 20, 24, 32, 48, 64px
2. Set up in Theme Styles → Typography
3. Use relative units (rem) for accessibility

### Spacing System
1. Define spacing scale: 4, 8, 16, 24, 32, 48, 64, 96px
2. Apply via Theme Styles or custom CSS classes
3. Maintain consistency across all sections

## Phase 5: Page Building

### Header & Footer
1. Create Header template: Bricks → Templates → Add New → Header
2. Build header with logo, navigation, CTA
3. Set template conditions: Display on → Entire Website
4. Create Footer template similarly
5. Set footer conditions: Display on → Entire Website

### Section Layout Pattern
1. **Section** — Full-width container
2. **Container** — Inner wrapper (1200px max-width)
3. **Columns** — Grid layout (2-col, 3-col, etc.)
4. **Elements** — Content blocks within columns

### Common Layouts
- **Hero**: Section → Container → Heading + Subheading + CTA
- **Features**: Section → Container → Columns (3) → Icon + Title + Description
- **Testimonials**: Section → Container → Carousel or Grid of testimonial cards
- **CTA Banner**: Section (background color) → Container → Heading + CTA Button
- **Contact Form**: Section → Container → Form element + Map element

## Phase 6: Dynamic Data

### WordPress Data
1. Use `{post_title}` for dynamic headings
2. Use `{post_excerpt}` for summaries
3. Use `{featured_image}` for post thumbnails
4. Use `{author_name}` for bylines
5. Use `{post_date}` for publish dates

### Custom Fields (ACF/Meta Box)
1. Ensure ACF fields are created and assigned to post types
2. Use `{field_field_name}` for ACF fields
3. Use `{repeater_field}` for repeater loops
4. Test dynamic data rendering in preview mode

### Conditional Display
1. Use Element Conditions panel
2. Set conditions based on: post type, category, tag, custom field value
3. Test conditions in preview with different posts

## Phase 7: Query Loops

### Basic Query Loop
1. Add container element
2. Enable "Use query loop" in container settings
3. Configure query:
   - Post Type: Select target post type
   - Posts Per Page: 9 (or as needed)
   - Order By: Date (newest first) or Menu Order
   - Order: DESC
4. Add child elements with dynamic data

### Advanced Queries
1. **Taxonomy Filter**: Filter by category/tag
2. **Meta Query**: Filter by custom field values
3. **Date Query**: Filter by date ranges
4. **Author Query**: Filter by specific authors

### Pagination
1. Add pagination element after query loop container
2. Configure: Previous/Next buttons, page numbers
3. Style pagination to match design

## Phase 8: Interactions & Animations

### Hover Effects
1. Select element → Interactions panel
2. Add interaction: Mouse Enter → Style Change
3. Configure: property, duration, easing
4. Add reverse: Mouse Leave → restore original

### Scroll Animations
1. Add interaction: Scroll Into View → Style Change
2. Configure: trigger point, animation type
3. Use subtle animations: fade-in, slide-up

### Click Interactions
1. Add interaction: Click → Toggle Class
2. Use for: mobile menu, accordion, modal triggers
3. Add CSS classes for states: `.is-open`, `.is-active`

## Phase 9: Forms

### Basic Contact Form
1. Add Form element
2. Configure fields: Name, Email, Message, Submit
3. Set action: Email (configure recipient)
4. Add success/error messages
5. Style form fields to match design

### Advanced Forms
1. **Multi-step forms**: Use form steps with progress indicator
2. **Conditional fields**: Show/hide based on selections
3. **File upload**: Configure allowed file types, size limits
4. **reCAPTCHA**: Add spam protection

## Phase 10: Performance Optimization

### Image Optimization
1. Use WebP format where possible
2. Set appropriate image sizes in Settings → Media
3. Lazy load off-screen images (default in Bricks)
4. Use responsive images with srcset

### CSS Optimization
1. Enable Critical CSS in Bricks settings
2. Minimize custom CSS — use Theme Styles instead
3. Remove unused CSS with plugin if needed

### JavaScript Optimization
1. Defer non-critical JavaScript
2. Remove unused scripts
3. Minimize animation complexity on mobile

### Caching
1. Install caching plugin (WP Rocket, W3 Total Cache)
2. Enable page caching, browser caching, minification
3. Test with GTmetrix or PageSpeed Insights

## Phase 11: Responsive Design

### Mobile-First Approach
1. Design for mobile first, enhance for larger screens
2. Use Bricks breakpoints to adjust layouts
3. Test on real devices, not just browser resize

### Common Mobile Adjustments
1. Stack columns vertically on mobile
2. Reduce font sizes for mobile
3. Increase tap targets (buttons, links)
4. Hide non-essential elements on mobile
5. Simplify navigation (hamburger menu)

### Tablet Adjustments
1. Adjust column widths for tablet
2. Modify spacing for medium screens
3. Test landscape and portrait orientations

## Phase 12: Quality Assurance

### Pre-Launch Checklist
1. **Cross-browser testing**: Chrome, Firefox, Safari, Edge
2. **Mobile testing**: iOS Safari, Android Chrome
3. **Accessibility**: Tab navigation, screen reader, contrast ratios
4. **Performance**: PageSpeed score > 90, no render-blocking resources
5. **SEO**: Meta titles, descriptions, alt text, schema markup
6. **Forms**: Test all form submissions, validation, error messages
7. **Links**: Verify all internal and external links
8. **Images**: Check all images load, no broken references

### Content Review
1. Proofread all text
2. Check image quality and relevance
3. Verify dynamic data displays correctly
4. Test conditional content logic

### Technical Review
1. Check console for JavaScript errors
2. Verify SSL certificate (no mixed content)
3. Test 404 page
4. Verify redirects work

## Phase 13: Launch

### Pre-Launch Steps
1. Remove any maintenance mode
2. Update DNS and SSL if needed
3. Configure email (SMTP if needed)
4. Set up backups (UpdraftPlus or similar)
5. Install security plugin (Wordfence or similar)

### Post-Launch
1. Submit sitemap to Google Search Console
2. Test all forms and interactions live
3. Monitor error logs for 24-48 hours
4. Verify analytics tracking
5. Document any issues for client review

## Phase 14: Maintenance

### Regular Tasks
1. Update WordPress core, themes, plugins monthly
2. Back up weekly (automated)
3. Monitor performance monthly
4. Review security scans
5. Update content as needed

### Bricks Updates
1. Test updates on staging first
2. Review changelog for breaking changes
3. Update child theme if needed
4. Clear cache after updates

## Common Patterns

### Container Width
```css
/* Default container width */
.brxe-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}
```

### Section Spacing
```css
/* Consistent section padding */
.brxe-section {
  padding: 80px 0;
}

/* Mobile adjustment */
@media (max-width: 767px) {
  .brxe-section {
    padding: 40px 0;
  }
}
```

### Button Styles
```css
/* Primary button */
.brxe-button.is-primary {
  background: var(--color-primary);
  color: white;
  padding: 12px 24px;
  border-radius: 4px;
  transition: background 0.3s ease;
}

.brxe-button.is-primary:hover {
  background: var(--color-primary-dark);
}
```

## Troubleshooting

### Builder Won't Load
1. Check PHP memory limit (256M minimum)
2. Increase max execution time in php.ini
3. Disable conflicting plugins
4. Check browser console for errors

### Styles Not Applying
1. Clear Bricks cache (Bricks → Settings → Clear Cache)
2. Clear browser cache
3. Check for CSS specificity conflicts
4. Verify Theme Style is active

### Dynamic Data Not Showing
1. Verify ACF fields are published
2. Check field names match exactly
3. Ensure post has data in the field
4. Test in preview mode

### Performance Issues
1. Enable Critical CSS
2. Optimize images
3. Reduce animation complexity
4. Minimize plugin count
5. Use caching

## Bricks Academy Reference

For detailed tutorials and official documentation:
- **Getting Started**: https://academy.bricksbuilder.io/chapters/getting-started/
- **Builder Interface**: https://academy.bricksbuilder.io/chapters/the-builder/
- **Elements**: https://academy.bricksbuilder.io/chapters/elements/
- **Dynamic Data**: https://academy.bricksbuilder.io/chapters/dynamic-data/
- **Theme Styles**: https://academy.bricksbuilder.io/chapters/theme-styles/
- **Query Loops**: https://academy.bricksbuilder.io/chapters/query-loop/
- **Interactions**: https://academy.bricksbuilder.io/chapters/interactions/
- **Performance**: https://academy.bricksbuilder.io/chapters/performance/
- **Developer Reference**: https://developer.bricksbuilder.io/
- **Hooks & Filters**: https://developer.bricksbuilder.io/hooks/
