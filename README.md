# Winnie's Cuisine & Events — Website

Static HTML website for **Winnie's Cuisine & Events**, Nwabude Mall, Centenary City Estate, Enugu.

---

## File Overview

| File | Purpose |
|---|---|
| `index.html` | Homepage — hero, about, experiences, stats, menu preview, gallery, events, testimonials, CTA, contact, footer |
| `menu.html` | Full digital menu with 6 categories and dietary tags |
| `events.html` | Events & catering packages, FAQ, inquiry form |
| `gallery.html` | Masonry photo gallery with lightbox and category filter |
| `contact.html` | Multi-step reservation form, testimonials, location, footer |
| `design-system.html` | Visual reference — colours, typography, components |

---

## Deploying the Site

### Option 1 — Netlify (recommended, easiest)

**Drag & Drop:**
1. Go to [app.netlify.com](https://app.netlify.com) and sign up free
2. Click **Add new site → Deploy manually**
3. Drag the entire `winnies-cuisine` folder onto the upload area
4. Netlify gives you a URL like `https://random-name.netlify.app`
5. Go to **Site settings → Domain management** to connect a custom domain

**Git-connected (auto-deploys on push):**
1. Push this repository to GitHub/GitLab
2. In Netlify: **Add new site → Import an existing project**
3. Select your repo — Netlify detects it's a static site automatically
4. Click **Deploy site** — every `git push` to `main` auto-deploys

### Option 2 — Vercel

1. Go to [vercel.com](https://vercel.com) and sign up free
2. Click **Add New Project → Import Git Repository** (or drag folder)
3. Set Framework Preset to **Other** (it's plain HTML, no build step)
4. Click **Deploy**
5. Go to **Settings → Domains** to add a custom domain

### Option 3 — GitHub Pages (free)

1. Push to GitHub
2. Go to repo **Settings → Pages**
3. Source: **Deploy from branch → main → / (root)**
4. GitHub Pages will serve `index.html` at `https://yourusername.github.io/repo-name/`

---

## Connecting the Contact Forms

The forms currently simulate submission with a 1.2-second delay. Choose one of these backends:

### Option A — Formspree (simplest, free tier available)

1. Sign up at [formspree.io](https://formspree.io)
2. Create a new form — Formspree gives you an endpoint like `https://formspree.io/f/xabc1234`
3. In `contact.html`, find `<form id="enquiry-form"` and add:
   ```html
   <form id="enquiry-form" action="https://formspree.io/f/xabc1234" method="POST">
   ```
4. Remove or replace the `submitForm()` JS function with a standard form submit
5. Formspree emails you every submission and has a dashboard

### Option B — EmailJS (no server, free tier)

1. Sign up at [emailjs.com](https://www.emailjs.com)
2. Connect a Gmail or other email service
3. Create an email template
4. Add to the `<head>` of `contact.html`:
   ```html
   <script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@4/dist/email.min.js"></script>
   <script>emailjs.init("YOUR_PUBLIC_KEY");</script>
   ```
5. Replace the `submitForm()` function body:
   ```js
   const form = document.getElementById('enquiry-form');
   emailjs.sendForm('YOUR_SERVICE_ID', 'YOUR_TEMPLATE_ID', form)
     .then(() => { /* show success */ });
   ```

### Option C — WhatsApp redirect (no backend needed)

Replace `submitForm()` with a function that builds a WhatsApp message from the form data:
```js
function submitForm() {
  const name = document.getElementById('f-name').value;
  const phone = document.getElementById('f-phone').value;
  const msg = encodeURIComponent(`Hello Winnie's! I'd like to make an enquiry.\nName: ${name}\nPhone: ${phone}`);
  // OWNER: Replace with your real number
  window.open(`https://wa.me/2348000000000?text=${msg}`, '_blank');
  // Then show success state
  document.querySelectorAll('.form-panel').forEach(p => p.classList.remove('active'));
  document.getElementById('step-success').classList.add('active');
}
```

---

## Updating Content

### Phone Number & WhatsApp

Search all files for `2348000000000` and replace with your real number (no spaces, no `+`, no dashes):

```
2348012345678   ← 234 (Nigeria) + 08012345678 without the leading 0
```

Also update the display text `+234 800 000 0000` to your real number.

### Email Address

Search for `hello@winniescuisine.com` and replace with your real email.

### Instagram / Social Media

Search for `winniescuisine` (in Instagram and Facebook URLs) and replace with your real handles.

### Menu Prices & Dishes (`menu.html`)

Each menu item looks like:
```html
<!-- OWNER: Update dish name and price -->
<div class="menu-item ...">
  <div>
    <h3>Dish Name Here</h3>
    <p>Description</p>
  </div>
  <span class="price">₦8,500</span>
</div>
```
Change the text and price directly. Add or remove `<div class="menu-item">` blocks as needed.

### Event Package Prices (`events.html`)

Find the package cards and update the `₦` price figures. Each card has a heading like:
```html
<p class="text-3xl font-bold">₦95,000</p>
<span>/ package</span>
```

### Opening Hours (`contact.html` & `index.html`)

Search for `11:00 AM – 10:00 PM` and update all instances if hours change.

### Images

All images currently use [Unsplash](https://unsplash.com) placeholder URLs. To replace them:

1. Upload your real photos to a hosting service (Cloudinary free tier, or your Netlify site's public folder)
2. In each HTML file, find `src="https://images.unsplash.com/...` and replace the URL with your image URL
3. Update the `alt` text to describe your actual photo

**For Open Graph images** (social sharing previews):
- Create a folder `images/` in the project root
- Add files: `og-home.jpg`, `og-menu.jpg`, `og-events.jpg`, `og-gallery.jpg`, `og-contact.jpg` (1200×630px)
- Update the `og:image` meta tags in each file to point to `https://yourdomain.com/images/og-home.jpg` etc.

### Google Maps Embed (`contact.html`)

1. Go to [maps.google.com](https://maps.google.com) and search for your exact address
2. Click **Share → Embed a map → Copy HTML**
3. In `contact.html`, replace the `<iframe>` inside the `<!-- Map -->` comment block with the copied code
4. Keep `width="100%"` and `height="380"` attributes

---

## Going Live Checklist

- [ ] Replace all placeholder phone numbers (`2348000000000`)
- [ ] Replace placeholder email (`hello@winniescuisine.com`)
- [ ] Replace Instagram/Facebook/WhatsApp links with real handles
- [ ] Connect the contact form (Formspree, EmailJS, or WhatsApp redirect)
- [ ] Replace Unsplash images with real restaurant photos
- [ ] Add real OG images (1200×630px) to `/images/` folder
- [ ] Update Google Maps embed with real address
- [ ] Set canonical URLs and OG URLs to your real domain (search `winniescuisine.com` in all files)
- [ ] Buy and connect a custom domain (e.g. `winniescuisine.com`)
- [ ] Enable HTTPS (automatic on Netlify/Vercel/GitHub Pages)
- [ ] Test on mobile (iPhone + Android) and desktop

---

## Tech Stack

- **HTML5** — semantic, accessible markup
- **Tailwind CSS** (CDN) — utility styling with custom design tokens
- **Google Fonts** — Cormorant Garamond (headings) + Inter (body)
- **Vanilla JS** — no frameworks, no build step required
- Zero npm dependencies — open any `.html` file directly in a browser

---

## Need Help?

Contact the developer or reach out via the issue tracker on GitHub.
