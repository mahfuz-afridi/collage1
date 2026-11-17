# MASTER PROMPT: Teachers & Staff Page for BAF Shaheen College Chattogram

## 1. Role and goal

Act as a senior frontend developer, UI/UX designer, and accessibility specialist.

Extend my **existing** college website by adding one dedicated **Teachers & Staff** page. It must look and behave like a natural part of the current site, work perfectly on **phone, tablet and PC**, and support **both Dark Mode and Light Mode**.

Do not just describe a plan. **Write the complete, working code**, then verify it.

I do NOT want: a new website, a new homepage, a faculty-management system, login, admin dashboard, database or fake API. I want a clean, simple, polished page where visitors can see our teachers, grouped by department.

---

## 2. Existing project (inspect first)

The site is **plain HTML + CSS + JavaScript** (no framework):

- `index.html` – homepage (header with logo and nav, hero, stats, "Why Choose Us", history slider, quick-links grid, footer)
- `homee.css` – homepage styles
- `script.js` – mobile menu + history slider
- `images/logo.png`, `clg.png`, `anim1.png`–`anim3.png`
- `login/logn.html` – login page

Before coding, read the files I provide and reuse: the logo, college name ("BAF Shaheen College Chattogram", tagline "Learn. Grow. Succeed."), nav links, footer content, fonts (Inter) and the mobile-menu behavior. If I attach a screenshot, treat it as the visual reference.

Rules:
- Keep the homepage and every existing link working. Change `index.html` as little as possible.
- Do not create duplicate navbars or duplicate pages.
- Do not invent the college's official name, logo, address, phone, email or social links. Keep the existing placeholders as they are.

---

## 3. Files to create / change

Create:
- `teachers.html` – the page
- `teachers.css` – styles for the page (dark and light theme variables, responsive rules)
- `teachers.js` – rendering, search/filter, theme toggle, mobile menu
- `teachers-data.js` – the teacher data (single source of truth)

Modify `index.html` only to:
1. Add a **"Teachers & Staff"** link to the main nav pointing to `teachers.html` (if one already exists, update it instead of adding a second).
2. Point the existing quick-link item "Teacher & Staff" to `teachers.html`.

On `teachers.html`:
- Same header (logo, college name, nav) and footer as the homepage, with a working link back to `index.html`.
- The "Teachers & Staff" nav item has an active state (`aria-current="page"`).
- Mobile hamburger menu works (opens/closes; closes on link tap, Esc, outside tap, and when resized to desktop).

---

## 4. Page content

**Title:** Teachers & Staff
**Intro:** "Meet our dedicated faculty members across different academic departments."

Order of content:
1. Page title + intro.
2. Compact stats computed from the data (not hard-coded): Total Teachers **34**, Departments **6**, Science **13**, Commerce **7**, Humanities **5**.
3. Light toolbar: a search box (matches name, subject or department, case-insensitive, trims spaces), a department dropdown ("All Departments" + six departments), a clear-search button, and a live result count ("Showing X of 34 teachers"). Search and dropdown work together. If nothing matches, show a friendly empty state with a "Show all teachers" button.
4. Six department sections, each with a clearly visible heading and teacher count.

### Departments (in this order)

1. Science — বিজ্ঞান বিভাগ
2. Commerce — ব্যবসায় শিক্ষা বিভাগ
3. Humanities — মানবিক বিভাগ
4. English Department
5. Bangla Department
6. ICT Department

### Table in every department

Columns exactly: **SL | Teacher Name | Subject | Employee ID**

- SL restarts from 1 in every department.
- Employee ID shows **যাচাই প্রয়োজন** for every teacher (IDs are not verified yet). Never invent or guess an ID. Store it as `employeeId: null` in the data and render the fallback text, so I can later add real IDs by editing only the data file.
- Show all teachers even though IDs are missing. Do not merge or de-duplicate people who share a subject or a similar name.
- When a filter/search is active, keep SL numbering consistent (either original numbers or re-numbered, but be consistent) and never show a teacher twice.

---

## 5. Teacher data (authoritative – use exactly as written)

Keep every name, initial, capital letter, dot and spelling exactly as given. Do not correct anything (for example, "Bayzeeed" stays "Bayzeeed").

**Science — বিজ্ঞান বিভাগ (13)**
1. Mohammad Azizur Rahman — Chemistry
2. Emran Uddin Shah — Physics
3. Nur Akther — Biology
4. Rabeya Basry — Biology
5. Rahnuma Tabassum — Chemistry
6. Jayema Zahur Shefta — Biology
7. Sohrab Bin Ahmed — Physics
8. Jannatul Ferdosh Sharmin — Mathematics
9. Md. Azharul Islam — Physics
10. Mohammed Rabiul Alam — Physics
11. Nazmul Hasan Arif — Physics
12. Mohammad Mushabber Ahmad — Biology
13. Purnima Bhowmick — Chemistry

**Commerce — ব্যবসায় শিক্ষা বিভাগ (7)**
1. Md. Rubel Hossen Khan — Finance & Banking
2. Sanjida Khanam — Finance & Banking
3. Muhammad Moshiur Rahman Shyok — Accounting
4. MST Shintia Subarna — Business Organization & Management
5. S. K. Zayed Al Samad — Accounting
6. Mohammed Shahab Uddin — Business Organization & Management
7. Dabashis Rudra — Management

**Humanities — মানবিক বিভাগ (5)**
1. Rajib Barua — Logic
2. Mohammad Salauddin — Islamic History & Culture
3. Md. Shah Akram — Economics
4. Md. Jawad Ul Alam Chowdhury — Civics & Citizenship
5. Muhammad Shahedur Rahaman — Geography

**English Department (3)**
1. Md. Mamum-Ur-Rashid — English
2. Kazi Mohd. Rashedul Islam — English
3. Mohammad Morshedul Alam — English

**Bangla Department (4)**
1. Abu Muhammed Asheq Elahi — Bangla
2. A. S. M. Saifullah Bayzeeed — Bangla
3. Shamsul Arefeen — Bangla
4. Trisa Das — Bangla

**ICT Department (2)**
1. Omar Faruk Siddique — ICT
2. Md. Didarul Hossain — ICT

**Integrity check:** 13 + 7 + 5 + 3 + 4 + 2 = **34 teachers in 6 departments**. If anything in this brief says 35, the department lists above are correct. Do not add a 35th person. Give each record a stable `id` (e.g. `sci-01`), `name`, `subject`, `department`, `employeeId`. Render all sections from this one array with one reusable render function (no copy-pasted HTML). Escape text when inserting into the DOM.

---

## 6. Visual design

Match the existing college identity: academic, professional, restrained.

- Fonts: Inter for body/UI (already used). Merriweather (or the site's existing serif) for headings. Add **Noto Sans Bengali** as a fallback so Bangla text renders well.
- Radius 10–14px, thin borders, subtle shadows, consistent spacing and a clear type scale (`clamp()` for headings).
- Avoid neon colors, heavy gradients, glassmorphism, flashy animation or decorative clutter. Only subtle hover/transition effects, disabled under `prefers-reduced-motion`.
- Department headings need clear hierarchy: English name, Bangla name beside/under it, teacher count, and an accent underline or left border.
- Tables: header row with distinct background, thin row dividers, gentle zebra or hover highlight, good padding, SL column narrow, long subjects wrap naturally (no clipping).

### Design tokens (CSS variables; reuse the site's own colors if they already exist)

| Token | Dark (default) | Light |
|---|---|---|
| Page background | #0B1425 | #F8FAFC |
| Section background | #101C31 | #FFFFFF |
| Card / table background | #14223A | #FFFFFF |
| Table header background | #1B2D4B | #EFF6FF |
| Primary text | #F8FAFC | #0F172A |
| Secondary text | #A9B8CC | #475569 |
| Border | #2B3C58 | #E2E8F0 |
| Accent | #3B82F6 | #2563EB |
| Accent hover | #60A5FA | #1D4ED8 |

Use `#2563EB` for filled buttons in both themes so white button text keeps enough contrast. Define colors once as CSS variables so I can change the theme in one place.

---

## 7. Dark Mode and Light Mode (mandatory)

1. A real, working theme toggle button in the navbar, styled like the existing header controls, with sun/moon icons (show the icon of the theme you will switch to), an accurate `aria-label` ("Switch to light theme" / "Switch to dark theme") and `aria-pressed`.
2. Switching updates the **whole page**: header, nav, background, title, stats, toolbar, inputs, dropdown, tables, buttons, empty state, footer, focus rings.
3. Save the choice in `localStorage` (key `bafsc-theme`, wrapped in try/catch) and restore it on the next visit.
4. Default is Dark. If nothing is saved, use Dark.
5. No "flash of wrong theme": set `data-theme` with a tiny inline script in `<head>` before the CSS paints. Set `color-scheme` for each theme.
6. Search text, selected department and scroll position must not reset when the theme changes.
7. Both themes must pass readable contrast (body text at least 4.5:1).
8. Homepage: do not redesign it. The homepage is currently light-themed, so make the teachers page header match its logo and nav layout. If it is easy and low-risk, share the same `bafsc-theme` key so a future toggle on the homepage stays in sync; otherwise leave the homepage unchanged and tell me.

---

## 8. Responsive design (phone, tablet, PC)

Mobile-first CSS using Grid/Flexbox, relative units and `clamp()`. No horizontal page scroll at any width.

**Phone (320–599px)**
- Compact header with hamburger menu; theme toggle always visible.
- Toolbar stacks vertically; inputs full width; touch targets at least 44px.
- **Do not squeeze a 4-column table.** Each table row becomes a stacked card: teacher name as the title, then labelled lines "Subject: …" and "Employee ID: …", with the SL number shown as a small badge. Implement with `data-label` attributes and CSS (keep real `<table>` semantics on larger screens). Keep it accessible to screen readers.
- Stats in 2 columns (first card full width).

**Tablet (600–899px)**
- Real table layout with comfortable padding, or a balanced 2-column card layout; toolbar in one row (search wide, dropdown beside it).
- Stats in 3 columns.

**Laptop / PC (900px and above)**
- Centered container (max about 1200px), full-width tables with SL / Name / Subject / Employee ID columns clearly aligned, inline navigation, stats in one row of 5.

Also: usable at 200% zoom, landscape phones, and 1920px+ monitors (content stays centered, nothing stretches awkwardly). Long names and long subjects (e.g. "Business Organization & Management") must wrap without breaking the layout.

---

## 9. Accessibility and UX

- Semantic landmarks (`header`, `nav`, `main`, `footer`), one `h1`, `h2` per department, real `<table>` with `<caption>` (visually hidden is fine), `<th scope="col">`.
- Visible labels for search and dropdown, visible keyboard focus, skip-to-content link.
- Result count uses `aria-live="polite"`.
- Don't rely on color alone. Respect `prefers-reduced-motion`.
- Bangla text uses `lang="bn"`.

---

## 10. Technical rules

- Plain HTML/CSS/JS only, matching the existing project. No frameworks, no build step, no heavy libraries.
- Font Awesome via the existing CDN link is fine for icons.
- No console errors, no unresolved paths, no unused buttons. Every visible control must work.
- Do not add teacher photos, emails, phone numbers, degrees, biographies, job titles or any other information I did not provide.
- Keep code clean and commented where helpful. Keep data separate from presentation.

---

## 11. Verify before finishing

Check and report only what you actually ran or inspected:

1. Exactly 34 teachers render, with correct per-department counts (13/7/5/3/4/2) and no duplicates; names and subjects match section 5 exactly.
2. Every Employee ID cell shows "যাচাই প্রয়োজন".
3. Search by name, subject and department; dropdown filter; both combined; clear/reset; empty state; result count.
4. Theme toggle works, persists after reload, no flash, everything readable in both themes.
5. No horizontal overflow and no clipped text at 320, 375, 430, 768, 1024, 1280, 1440 and 1920px, in both themes.
6. Nav link and quick-link open `teachers.html`; the logo/Home link returns to `index.html`; the active nav state is visible; the mobile menu works.
7. Keyboard navigation works for menu, theme toggle, search and dropdown.

If you can open a browser or preview, check the real rendered page. If you cannot, say clearly that the layout was not visually tested.

---

## 12. Final answer format

Give me:
1. The complete code for every created or changed file (with file names).
2. A list of files created/modified and the exact edit made to `index.html`.
3. Where the files go and how to open the site (folder structure).
4. How to add real Employee IDs later (edit `employeeId` in `teachers-data.js`) and how to add or edit a teacher.
5. A short, honest summary of which checks were completed.

Do not stop at a plan, a wireframe or partial code.
