# Tutoria Website

A simple, fast, static website for **Tutoria**, a Kolkata-based tutoring consultancy. Built with plain HTML, CSS and JavaScript only — no frameworks, no build step, no database.

Each page is a **single self-contained HTML file** — the CSS lives inside a `<style>` block and the JavaScript lives inside a `<script>` block, right inside every page. There are no separate `.css` or `.js` files to manage.

This README assumes you have never used GitHub or Cloudflare before. Follow the steps in order.

---

## What's in this folder

```
tutoria/
├── index.html        → Homepage (styles + script included inline)
├── about.html         → About Tutoria (styles + script included inline)
├── forms.html         → All forms (styles + script included inline)
├── agreement.html      → Agreement code page for tutors (styles + script included inline)
├── images/
│   └── README.txt        → Notes on what image files to add later
└── README.md               → This file
```

**Important:** because the CSS and JavaScript are duplicated inside each page rather than shared from one file, any change you want reflected on *every* page (like the WhatsApp number, or a footer link) needs to be made in **all four HTML files**, not just one. The steps below tell you exactly where.

---

## Step 1 — Create a GitHub repository

1. Go to [github.com](https://github.com) and sign in (or create a free account).
2. Click the **+** icon in the top-right corner → **New repository**.
3. Name it something like `tutoria-website`.
4. Set it to **Public** or **Private** — either works.
5. Do **not** tick "Add a README file" (you already have one).
6. Click **Create repository**.

## Step 2 — Upload the files

1. On your new repository's page, click **uploading an existing file** (or **Add file → Upload files**).
2. Drag the entire contents of this `tutoria` folder into the upload box — including the `css`, `js` and `images` folders.
3. Scroll down and click **Commit changes**.

Your repository should now show `index.html`, `about.html`, `forms.html`, `agreement.html`, and the `css`, `js`, `images` folders at the top level.

## Step 3 — Create a Cloudflare account

1. Go to [dash.cloudflare.com/sign-up](https://dash.cloudflare.com/sign-up) and create a free account (or sign in).

## Step 4 — Go to Workers & Pages

1. In the Cloudflare dashboard, find **Workers & Pages** in the left-hand menu.
2. Click **Create** → choose the **Pages** tab → **Connect to Git**.

## Step 5 — Select your GitHub repository

1. Authorise Cloudflare to access your GitHub account if asked.
2. Select the `tutoria-website` repository you created in Step 1.
3. Click **Begin setup**.

## Step 6 — Configure the build settings

Since this is a plain static site with no build step, use these settings:

- **Framework preset:** None
- **Build command:** *(leave empty)*
- **Build output directory:** `/` (the root of the repository)

Leave everything else as default.

## Step 7 — Deploy

Click **Save and Deploy**. Cloudflare will publish your site — this usually takes under a minute.

## Step 8 — Open your free URL

Once deployment finishes, Cloudflare gives you a free URL like:

```
https://tutoria-website.pages.dev
```

Open it and click through every page to make sure everything looks right.

## Step 9 — Connect your custom domain (later)

When you're ready to use your own domain:

1. In your Cloudflare Pages project, go to **Custom domains**.
2. Click **Set up a custom domain** and follow the instructions.
3. If your domain is already on Cloudflare, this is usually automatic. If it's registered elsewhere, Cloudflare will show you the DNS records to add.

---

## Making changes after launch

You don't need to touch any code for most updates — just edit the relevant file on GitHub (click the file → pencil/edit icon → **Commit changes**) and Cloudflare will redeploy automatically within a minute.

### Change the WhatsApp number

Each page has its own copy of the script, so open **`index.html`**, **`about.html`**, **`forms.html`** and **`agreement.html`** one at a time, and in each file find this line (near the top of the `<script>` block, towards the bottom of the file):

```javascript
const WHATSAPP_NUMBER = "YOUR_WHATSAPP_NUMBER";
```

Replace `YOUR_WHATSAPP_NUMBER` with your real number in international format, digits only, no `+`, spaces or dashes.
Example: for `+91 98765 43210`, write:

```javascript
const WHATSAPP_NUMBER = "919876543210";
```

Every WhatsApp button and link on that page automatically uses this value — just repeat the same edit in all four files so the number matches everywhere.

### Change the "Call Us" phone number

Just below it in the same `<script>` block, in every file:

```javascript
const CALL_NUMBER = "YOUR_PHONE_NUMBER";
```

Replace with your number in international format, e.g. `"+919876543210"`, in all four HTML files.

### Change testimonials

Open **`index.html`** and search for `Sample testimonial`. Each testimonial is a small block like this:

```html
<article class="testimonial-card">
  <span class="testimonial-tag">Sample testimonial — replace with genuine feedback</span>
  <span class="stars" aria-label="5 out of 5 stars">★★★★★</span>
  <p class="testimonial-quote">"Your real testimonial text goes here."</p>
  <p class="testimonial-meta">Parent · Kolkata</p>
</article>
```

Replace the quote and meta text with real feedback (for example, submissions collected through the "Share Your Experience" form), and remove the `testimonial-tag` line once it's genuine. You can copy this whole block to add more testimonials.

### Change social media links

Open **`index.html`**, **`about.html`**, **`forms.html`** and **`agreement.html`** and search for `YOUR_HANDLE`. You'll find three lines in the footer of each page:

```html
<a href="https://instagram.com/YOUR_HANDLE" ...>Instagram</a>
<a href="https://facebook.com/YOUR_HANDLE" ...>Facebook</a>
<a href="https://youtube.com/@YOUR_HANDLE" ...>YouTube</a>
```

Replace `YOUR_HANDLE` with your real usernames (or full URLs) in each file.

### Replace the logo

Right now the logo is a styled text logo ("TUTORIA") rather than an image, so there's nothing to break. If you'd like to switch to a picture-based logo later:

1. Add your logo file to the `images/` folder (e.g. `images/logo.png`).
2. In each HTML file, find:
   ```html
   <a href="index.html" class="logo" aria-label="Tutoria home">TUTOR<span>IA</span></a>
   ```
3. Replace it with:
   ```html
   <a href="index.html" class="logo" aria-label="Tutoria home">
     <img src="images/logo.png" alt="Tutoria" style="height: 32px;">
   </a>
   ```

### Edit any other text

All page text lives directly in the `.html` files as plain readable sentences — open the relevant file on GitHub, click the pencil icon to edit, change the text between the HTML tags, and commit. You don't need to touch `style.css` or `main.js` for text changes.

---

## About the forms and the agreement page

The three forms on `forms.html` (Tuition Requirement, Share Your Experience, Tutor Registration) and the code box on `agreement.html` currently work as a **frontend-only preview**: when someone submits, they see a friendly confirmation message, but nothing is saved anywhere yet.

The intended future setup, once you're ready to build it:

```
Website Form → Google Apps Script → Google Sheets
```

and for the agreement flow:

```
Tutor → Agreement Code → Verification → Agreement Form → Google Sheets → AutoCrat → Google Docs template → PDF → Tutor + Tutoria
```

The code has clearly marked **INTEGRATION POINT** comments inside the `<script>` block of `forms.html` and `agreement.html` (in the `fakeSubmit()` and `checkAgreementCode()` functions) showing exactly where to plug in a real Google Apps Script Web App URL when that backend is ready. No real agreement codes or secrets are stored anywhere in this code.

---

## Performance and quality notes

- No frameworks or libraries are used — the whole site is lightweight and loads quickly.
- The layout is fully responsive from mobile to large desktop screens.
- The site uses semantic HTML, visible keyboard focus states, and `aria-label`s for accessibility.
- Fonts (Fraunces, Inter, IBM Plex Mono) load from Google Fonts; if you'd prefer to remove the external dependency later, they can be self-hosted, but this isn't required for launch.
