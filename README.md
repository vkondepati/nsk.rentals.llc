# NSK Rentals LLC — Event Rentals Site

A simple static website for event rentals (tables, chairs, tents, accessories) with a Google Form checkout. Built with HTML + Tailwind CDN + vanilla JS. Ready for GitHub Pages.

## Live Structure
```
event-rentals-site/
├─ index.html
├─ products.json
├─ /images/
├─ /assets/
│  └─ site.css
├─ README.md
└─ LICENSE
```

## Business Info (edit in `index.html`)
In the `<script>` `CONFIG` object:
- `BUSINESS_NAME`: `"NSK Rentals LLC"`
- `ZELLE_EMAIL`: `"nsk.rentals2025@gmail.com"`
- `PICKUP_ADDRESS`: `"13243 Teton St. Frisco TX - 75035"`
- `BUSINESS_PHONE` and `BUSINESS_EMAIL`: add if desired
- `GOOGLE_FORM_URL`: **Paste your Google Form prefill URL** (see below)

## Google Form Setup & Prefill
1. Create a Google Form with fields:
   - Name
   - Email or Phone number
   - Address to deliver
   - Number of Rectangle Tables
   - Number of Round Tables
   - Number of Chairs
   - Tents? (Yes/No or quantity)
   - Tarps (quantity)
   - Event backdrop stand (quantity)
   - Dates to be rented
   - Payment method (Zelle / Cash / Card)

2. Get a **prefill link**:
   - In Google Forms, click **⋮ > Get pre-filled link**.
   - Enter sample values, click **Get link**, then copy the URL.
   - You'll see parameters like `entry.1234567890=Sample`.

3. **Map entry IDs** in `index.html`:
   - In the `GOOGLE_FORM_ENTRY_MAP` object, set keys to the corresponding `entry.XXXX` values, for example:
   ```js
   const GOOGLE_FORM_ENTRY_MAP = {
     rect_tables: "entry.1234567890",
     round_tables: "entry.2345678901",
     chairs: "entry.3456789012",
     tents: "entry.4567890123",
     tarps: "entry.5678901234",
     backdrop: "entry.6789012345",
     // Optional:
     name: "entry.7890123456",
     email_or_phone: "entry.8901234567",
     address: "entry.9012345678",
     dates: "entry.0123456789",
     payment_method: "entry.1122334455"
   };
   ```
   - Paste your form's prefill base URL into `CONFIG.GOOGLE_FORM_URL`.

4. The site will attach selected quantities as prefill parameters when opening the form.

> **Note:** If you don't set entry IDs, quantities will fall back to custom keys (e.g., `rect_tables=4`) which most Forms will ignore. Always use real entry IDs for proper prefill.

## Products
Edit `products.json` to change items, prices, images, and descriptions. Add images to `/images/` and set the `img` filename accordingly. Placeholder SVGs are provided; replace with real photos as needed.

## Deploy to GitHub Pages
1. Create a new GitHub repo, e.g., `event-rentals-site`.
2. Upload the files in this folder (or push with git).
3. In the repo: **Settings → Pages → Source: `main` branch, `/root`**. Save.
4. Wait for the page to publish; your site will be at `https://<your-user>.github.io/event-rentals-site/`.

## Accessibility
- Semantic HTML, alt text, visible focus styles.
- Good color contrast and large tappable buttons.

## License
MIT © 2025 NSK Rentals LLC
