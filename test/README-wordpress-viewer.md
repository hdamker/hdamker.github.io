# CAMARA API Overview Viewer - WordPress Edition

## Overview

The WordPress Edition viewer is a specialized version of the CAMARA API Status Viewer designed for seamless integration into the camaraproject.org website. It provides an interactive, filterable overview of all CAMARA APIs with direct links to API detail pages.

## ⚠️ Important Warning

**The data shown in the viewer is NOT final and must be:**
- Updated with the latest API information before publication
- Reviewed for accuracy and completeness
- Verified against the official CAMARA release data
- Checked for correct website URL mappings

## Features

### Core Functionality
- **Interactive Portfolio Categories**: Click category pills to filter APIs by their portfolio category
- **Clickable API Names**: Direct links to API detail pages on camaraproject.org
- **Advanced Filtering**: Search and filter by:
  - API name
  - Maturity level (initial/stable)
  - New API status
  - Repository name
  - Version range
- **Column Sorting**: Click any column header to sort data
- **Results Counter**: Shows filtered vs. total API count
- **Responsive Design**: Adapts to desktop and mobile viewports

### Data Display
- **Released API**: Name with link to detail page
- **Maturity**: API maturity level
- **API version**: Current version number
- **Public release**: Release tag with GitHub link
- **Category**: Portfolio category badge
- **Repository**: Link to GitHub repository
- **New**: Indicator for newly added APIs

## iframe Embedding Behavior

When embedded in an iframe, the viewer automatically:
- **Removes the header** to avoid duplication with the parent page
- **Adjusts padding** for seamless integration
- **Opens links in new tabs** to preserve the parent page context
- **Sends ready messages** to the parent window for integration hooks

## WordPress Integration

### Recommended Embedding Code

```html
<iframe src="https://hdamker.github.io/test/test-wordpress-final.html"
        width="100%"
        height="1400"
        frameborder="0"
        style="border: none;">
</iframe>
```

**Test URL**: `https://hdamker.github.io/test/test-wordpress-final.html`

### Height Recommendations
- **2500px**: Recommended if only footer follows - Shows all 60 APIs without internal scrolling
- **1400px**: Alternative for pages with content below - Shows 25-30 APIs
- **1200px**: Minimum - Shows 20-25 APIs
- **1600px**: Medium - Shows 35-40 APIs

**Note**: If the iframe is the last content element before the page footer, using the full height (2500px) provides the best user experience as it eliminates double scrollbars (page + iframe).

### WordPress Page Setup
1. Create or edit the API Overview page in WordPress
2. Add a Custom HTML block
3. Paste the iframe embed code
4. Adjust the source URL to your hosted viewer file
5. Preview and publish

## Data Generation Process

1. **Prepare JSON data** with API status information
2. **Run augmentation script** to add categories and website URLs:
   ```bash
   node augment-api-categories.js input.json output.json
   ```
3. **Generate viewer HTML**:
   ```bash
   node generate-confluence-viewer-v2.js \
     --template=api-status-viewer-v2-wordpress-final.html \
     output.json \
     final-viewer.html
   ```
4. **Deploy** the generated HTML file to your web server
5. **Embed** using the iframe code above

## Browser Compatibility

- Chrome/Edge 90+
- Firefox 88+
- Safari 14+
- Mobile browsers (iOS Safari, Chrome Mobile)

## Maintenance Notes

- **Update frequency**: Should be updated with each CAMARA release cycle
- **URL verification**: Check that API detail page links remain valid
- **Category updates**: Review portfolio categories for new APIs
- **Data validation**: Ensure version numbers and release tags are accurate

## Support

For issues or questions about the viewer:
- Check the main viewer-v2 README for technical details
- Review the augmentation script for data mapping logic
- Test locally before deploying to production

## Potential Future Refinements

### Sticky Filters with Scrollable Table
A possible enhancement would be to keep the category pills and filters always visible while making only the table scrollable. This approach would:

**Benefits:**
- Keep filtering controls always accessible
- Eliminate need to scroll up to change filters
- Better use of vertical space for data display
- More efficient workflow for users comparing filtered results

**Implementation approach:**
- Use `position: sticky` for filter sections
- Set `max-height` and `overflow-y: auto` on table container
- Calculate appropriate table height based on viewport
- Disable on mobile devices (screens < 768px) for better UX

**Considerations:**
- More complex CSS layout required
- Need to handle responsive behavior carefully
- May feel cramped with limited vertical space
- Requires testing across different screen sizes and browsers

This enhancement would be particularly useful when the viewer is embedded with a fixed height, allowing users to work with filters without losing their scroll position in the results.

---

*Last updated: September 2025*