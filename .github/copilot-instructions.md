# GitHub Copilot Instructions for NSK Rentals LLC

## Project Overview
This is a static event rental website built with vanilla HTML/CSS/JS and designed for GitHub Pages deployment. The site integrates with Google Forms for order processing and uses Zelle for payments.

## Architecture & Tech Stack
- **Frontend**: Single HTML file with inline JavaScript, Tailwind CSS via CDN
- **Data**: JSON-driven product catalog (`products.json`)
- **Styling**: Tailwind utility classes + minimal custom CSS (`assets/site.css`)
- **Integration**: Google Forms prefill API for order submission
- **Deployment**: GitHub Pages (static hosting)

## Configuration Pattern
All business settings live in the `CONFIG` object at the top of `index.html`:
```javascript
const CONFIG = {
  BUSINESS_NAME: "NSK Rentals LLC",
  ZELLE_EMAIL: "nsk.rentals2025@gmail.com",
  PICKUP_ADDRESS: "13243 Teton St. Frisco TX - 75035",
  GOOGLE_FORM_URL: "https://forms.gle/..." // Critical for order flow
};
```

**Key Pattern**: Never hardcode business details in HTML - always reference `CONFIG` properties and use `{{ CONFIG.PROPERTY }}` syntax in templates that get processed by JavaScript.

## Google Forms Integration
The site uses a sophisticated prefill system for order forms:

1. **Product Mapping**: Products in `products.json` map to form fields via the `qtyMap` object in `buildPrefillURL()`
2. **Entry ID Mapping**: `GOOGLE_FORM_ENTRY_MAP` maps logical field names to Google Form entry IDs
3. **URL Building**: Selected quantities get converted to prefill parameters automatically

**Critical**: When adding new products, update both `products.json` AND the `qtyMap` in the JavaScript section.

## Product Management
Products are defined in `products.json` with this exact schema:
```json
{
  "id": "kebab-case-identifier", 
  "name": "Display Name",
  "price": 5.0,
  "unit": "each|per day",
  "img": "filename.jpg",
  "description": "User-facing description"
}
```

**Key Rules**:
- Product `id` must match keys in the JavaScript `qtyMap` object
- Images go in `/images/` directory, reference by filename only
- Prices are numbers, not strings
- Units should be consistent ("each", "per day")

## JavaScript Patterns
- **Quantity Tracking**: Global `quantities` object tracks user selections by product ID
- **Dynamic DOM**: Products rendered via `fetch('products.json')` and DOM manipulation
- **Event Handling**: All form buttons use `addEventListener` with proper preventDefault
- **URL Building**: Complex Google Forms prefill logic in `buildPrefillURL()`

## Styling Approach
- **Primary**: Tailwind utility classes for all layout and styling
- **Custom CSS**: Minimal additions in `assets/site.css` (smooth scrolling, sticky elements)
- **Design System**: Blue-600 for CTAs, gray-50 backgrounds, card-shadow utility class

## Development Workflow
- **No Build Process**: Direct file editing, view in browser
- **Testing**: Open `index.html` locally, ensure Google Form integration works
- **Deployment**: Push to GitHub, enable Pages in repo settings
- **Content Updates**: Edit `products.json` for inventory, `CONFIG` object for business details

## Common Tasks
- **Add Product**: Update `products.json` + add image + update `qtyMap`
- **Change Business Info**: Modify `CONFIG` object only
- **Update Styling**: Use Tailwind classes first, custom CSS as last resort
- **Form Integration**: Update `GOOGLE_FORM_ENTRY_MAP` with real entry IDs from Google Forms prefill

## Critical Integration Points
- **Google Forms**: The entire order flow depends on correct `GOOGLE_FORM_URL` and entry ID mapping
- **Image Assets**: Product images must exist in `/images/` directory with exact filenames from `products.json`
- **Tailwind CDN**: Site styling depends on Tailwind CDN - don't remove the CDN link

## Debugging Tips
- Check browser console for failed `products.json` fetch
- Verify Google Form URL opens correctly with prefilled quantities
- Ensure all product IDs in JSON match JavaScript `qtyMap` keys
- Test payment flow (Zelle email display, contact information accuracy)