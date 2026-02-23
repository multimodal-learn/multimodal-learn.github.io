# Workshop Website Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build a single-page static website for the IROS 2026 workshop "Small Data, Rich Sensing: Multimodal Learning for Robotic Manipulation" hosted at http://multimodal-learn.github.io/

**Architecture:** Single `index.html` file at repo root using Tailwind CSS via CDN for styling and Inter font from Google Fonts. No build toolchain. Each section is a `<section>` element with an `id` for smooth-scroll nav linking. Sections alternate white/light-gray backgrounds.

**Tech Stack:** HTML5, Tailwind CSS (CDN v3), Inter (Google Fonts), vanilla JS (scroll behavior only)

---

## Content Reference

All content comes from the design doc at `docs/plans/2026-02-23-website-design.md`. Key data:

**Organizers:**
- Haonan Chen — Postdoctoral Scholar, Harvard University — haonan_chen@seas.harvard.edu — https://haonan16.github.io/
- Shuijing Liu — Postdoctoral Scholar, UT Austin — shuijing.liu@utexas.edu — https://shuijing725.github.io
- Yuxiang Ma — Ph.D. student, MIT — yxma20@mit.edu — https://yuxiang-ma.github.io/
- Mingyo Seo — Ph.D. student, UT Austin — mingyo@utexas.edu — https://mingyoseo.com/
- Raven Huang — Postdoctoral Scholar, Stanford University — ravenh@stanford.edu — https://qingh097.github.io/

**Speakers:**
- Jie Tan — Google DeepMind
- David Hsu — National University of Singapore
- Jiajun Wu — Stanford University
- Yunzhu Li — Columbia University

**Schedule:** 8:30am Welcome → 8:45 Speaker 1 → 9:15 Speaker 2 → 9:45 Poster/Coffee → 10:15 Speaker 3 → 11:00 Speaker 4 → 11:30 Debate → 12:15 Conclusion → 12:30 End

---

### Task 1: Scaffold index.html with head and nav

**Files:**
- Create: `index.html`

**Step 1: Create the file with HTML boilerplate, Tailwind CDN, Inter font, and sticky nav**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Small Data, Rich Sensing — IROS 2026 Workshop</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet" />
  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: { sans: ['Inter', 'sans-serif'] },
          colors: { navy: { DEFAULT: '#1e3a8a', light: '#3b5fc0' } }
        }
      }
    }
  </script>
  <style>
    html { scroll-behavior: smooth; }
  </style>
</head>
<body class="font-sans text-gray-800 bg-white">

  <!-- NAV -->
  <nav id="navbar" class="sticky top-0 z-50 bg-white border-b border-gray-200">
    <div class="max-w-6xl mx-auto px-4 py-3 flex items-center justify-between">
      <span class="font-semibold text-navy text-sm hidden md:block">Small Data, Rich Sensing</span>
      <div class="flex items-center gap-5 text-sm font-medium text-gray-600">
        <a href="#overview" class="hover:text-navy transition-colors">About</a>
        <a href="#speakers" class="hover:text-navy transition-colors">Speakers</a>
        <a href="#schedule" class="hover:text-navy transition-colors">Schedule</a>
        <a href="#cfp" class="hover:text-navy transition-colors">CFP</a>
        <a href="#organizers" class="hover:text-navy transition-colors">Organizers</a>
        <a href="#cfp" class="ml-2 px-3 py-1.5 rounded border border-navy text-navy hover:bg-navy hover:text-white transition-colors">Submit</a>
      </div>
    </div>
  </nav>

  <!-- SECTIONS WILL GO HERE -->

</body>
</html>
```

**Step 2: Open index.html in a browser and verify**

Open `index.html` in a browser (or use a local server: `python3 -m http.server 8000`).
Expected: Sticky nav bar visible at top with all links, "Small Data, Rich Sensing" title on left.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: scaffold index.html with nav"
```

---

### Task 2: Hero section

**Files:**
- Modify: `index.html` (replace `<!-- SECTIONS WILL GO HERE -->`)

**Step 1: Add hero section after the nav closing tag**

```html
  <!-- HERO -->
  <section class="bg-white py-20 px-4 text-center">
    <div class="max-w-3xl mx-auto">
      <p class="text-sm font-semibold text-navy uppercase tracking-widest mb-4">IROS 2026 Workshop</p>
      <h1 class="text-4xl md:text-5xl font-bold text-gray-900 leading-tight mb-4">
        Small Data, Rich Sensing
      </h1>
      <p class="text-xl md:text-2xl text-gray-500 font-light mb-2">
        Multimodal Learning for Robotic Manipulation
      </p>
      <p class="text-base text-gray-400 mb-8">Half-day Workshop &bull; Abu Dhabi, UAE</p>
      <div class="flex justify-center gap-4 flex-wrap">
        <a href="#cfp" class="px-6 py-3 rounded border-2 border-navy text-navy font-semibold hover:bg-navy hover:text-white transition-colors">
          Call for Papers
        </a>
        <a href="#schedule" class="px-6 py-3 rounded border-2 border-gray-300 text-gray-600 font-semibold hover:border-navy hover:text-navy transition-colors">
          Program
        </a>
      </div>
    </div>
  </section>

  <!-- SECTIONS WILL GO HERE -->
```

**Step 2: Verify in browser**

Expected: Large centered title, subtitle, venue line, two buttons side by side.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add hero section"
```

---

### Task 3: Overview section

**Files:**
- Modify: `index.html`

**Step 1: Replace `<!-- SECTIONS WILL GO HERE -->` with overview section**

```html
  <!-- OVERVIEW -->
  <section id="overview" class="bg-gray-50 py-16 px-4">
    <div class="max-w-3xl mx-auto">
      <h2 class="text-2xl font-bold text-navy mb-6">About the Workshop</h2>
      <p class="text-gray-700 leading-relaxed mb-6">
        Foundation models trained on internet-scale data have achieved impressive generalization
        on vision and language domains, but robotic manipulation is fundamentally contact-rich.
        Success and safety often hinge on signals that vision alone cannot reliably infer —
        including touch, force/torque, proprioception, and audio. This mismatch creates a
        <em>sensory gap</em>: foundation models excel at semantics and geometry, yet we still
        lack a clear understanding of when vision-only policies break under contact, friction,
        compliance, occlusion, and real-time constraints.
      </p>
      <p class="text-gray-700 leading-relaxed mb-8">
        This workshop brings together researchers in foundation models, tactile/haptic sensing,
        state estimation, and control to address a central question:
      </p>
      <blockquote class="border-l-4 border-navy pl-5 py-2 bg-white rounded-r shadow-sm">
        <p class="text-lg font-semibold text-navy italic">
          "Is vision all we need for manipulation, or what additional sensing and interaction
          modeling is minimally necessary?"
        </p>
      </blockquote>
    </div>
  </section>

  <!-- TOPICS -->
  <section id="topics" class="bg-white py-16 px-4">
    <div class="max-w-5xl mx-auto">
      <h2 class="text-2xl font-bold text-navy mb-10 text-center">Topics of Interest</h2>
      <div class="grid md:grid-cols-3 gap-6">
        <div class="border border-gray-200 rounded-lg p-6">
          <h3 class="font-semibold text-gray-900 mb-3">Foundation Models &amp; VLA</h3>
          <p class="text-sm text-gray-600 leading-relaxed">
            Vision–language–action models, failure-mode analysis, sensory sufficiency evaluation,
            and principled ablations under contact.
          </p>
        </div>
        <div class="border border-gray-200 rounded-lg p-6">
          <h3 class="font-semibold text-gray-900 mb-3">Rich Sensing</h3>
          <p class="text-sm text-gray-600 leading-relaxed">
            Tactile and haptic sensing, force/torque, proprioception, audio perception,
            sensor design, simulation, and calibration.
          </p>
        </div>
        <div class="border border-gray-200 rounded-lg p-6">
          <h3 class="font-semibold text-gray-900 mb-3">Multimodal Learning &amp; Control</h3>
          <p class="text-sm text-gray-600 leading-relaxed">
            Multimodal fusion, representation learning, contact-aware control, uncertainty
            estimation, and recovery in small-data regimes.
          </p>
        </div>
      </div>
    </div>
  </section>

  <!-- SECTIONS WILL GO HERE -->
```

**Step 2: Verify in browser**

Expected: Gray background overview section with quote callout, then white 3-column topic cards below.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add overview and topics sections"
```

---

### Task 4: Invited speakers section

**Files:**
- Modify: `index.html`

**Step 1: Replace `<!-- SECTIONS WILL GO HERE -->` with speakers section**

Speaker photos are not yet available — use placeholder avatars from `https://ui-avatars.com` for now (format: `https://ui-avatars.com/api/?name=Jie+Tan&size=200&background=1e3a8a&color=fff`). Organizers can replace with real photos later by adding image files to an `assets/` folder.

```html
  <!-- SPEAKERS -->
  <section id="speakers" class="bg-gray-50 py-16 px-4">
    <div class="max-w-5xl mx-auto">
      <h2 class="text-2xl font-bold text-navy mb-10 text-center">Invited Speakers</h2>
      <div class="grid grid-cols-2 md:grid-cols-4 gap-8">

        <div class="text-center">
          <img src="https://ui-avatars.com/api/?name=Jie+Tan&size=200&background=1e3a8a&color=fff"
               alt="Jie Tan"
               class="w-28 h-28 rounded-full mx-auto mb-3 object-cover" />
          <p class="font-semibold text-gray-900">Jie Tan</p>
          <p class="text-sm text-gray-500">Google DeepMind</p>
        </div>

        <div class="text-center">
          <img src="https://ui-avatars.com/api/?name=David+Hsu&size=200&background=1e3a8a&color=fff"
               alt="David Hsu"
               class="w-28 h-28 rounded-full mx-auto mb-3 object-cover" />
          <p class="font-semibold text-gray-900">David Hsu</p>
          <p class="text-sm text-gray-500">National University of Singapore</p>
        </div>

        <div class="text-center">
          <img src="https://ui-avatars.com/api/?name=Jiajun+Wu&size=200&background=1e3a8a&color=fff"
               alt="Jiajun Wu"
               class="w-28 h-28 rounded-full mx-auto mb-3 object-cover" />
          <p class="font-semibold text-gray-900">Jiajun Wu</p>
          <p class="text-sm text-gray-500">Stanford University</p>
        </div>

        <div class="text-center">
          <img src="https://ui-avatars.com/api/?name=Yunzhu+Li&size=200&background=1e3a8a&color=fff"
               alt="Yunzhu Li"
               class="w-28 h-28 rounded-full mx-auto mb-3 object-cover" />
          <p class="font-semibold text-gray-900">Yunzhu Li</p>
          <p class="text-sm text-gray-500">Columbia University</p>
        </div>

      </div>
    </div>
  </section>

  <!-- SECTIONS WILL GO HERE -->
```

**Step 2: Verify in browser**

Expected: 4 circular avatar placeholders in a row, each with name and affiliation below.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add invited speakers section"
```

---

### Task 5: Schedule section

**Files:**
- Modify: `index.html`

**Step 1: Replace `<!-- SECTIONS WILL GO HERE -->` with schedule section**

```html
  <!-- SCHEDULE -->
  <section id="schedule" class="bg-white py-16 px-4">
    <div class="max-w-3xl mx-auto">
      <h2 class="text-2xl font-bold text-navy mb-10 text-center">Program</h2>
      <div class="overflow-hidden rounded-lg border border-gray-200">
        <table class="w-full text-sm">
          <thead class="bg-navy text-white">
            <tr>
              <th class="px-6 py-3 text-left font-semibold w-28">Time</th>
              <th class="px-6 py-3 text-left font-semibold">Event</th>
            </tr>
          </thead>
          <tbody>
            <tr class="bg-white"><td class="px-6 py-3 font-mono text-gray-500">8:30 AM</td><td class="px-6 py-3 text-gray-800">Welcome</td></tr>
            <tr class="bg-gray-50"><td class="px-6 py-3 font-mono text-gray-500">8:45 AM</td><td class="px-6 py-3 text-gray-800">Invited Talk 1</td></tr>
            <tr class="bg-white"><td class="px-6 py-3 font-mono text-gray-500">9:15 AM</td><td class="px-6 py-3 text-gray-800">Invited Talk 2</td></tr>
            <tr class="bg-gray-50"><td class="px-6 py-3 font-mono text-gray-500">9:45 AM</td><td class="px-6 py-3 text-gray-800">Poster Session &amp; Coffee Break</td></tr>
            <tr class="bg-white"><td class="px-6 py-3 font-mono text-gray-500">10:15 AM</td><td class="px-6 py-3 text-gray-800">Invited Talk 3</td></tr>
            <tr class="bg-gray-50"><td class="px-6 py-3 font-mono text-gray-500">11:00 AM</td><td class="px-6 py-3 text-gray-800">Invited Talk 4</td></tr>
            <tr class="bg-white"><td class="px-6 py-3 font-mono text-gray-500">11:30 AM</td><td class="px-6 py-3 text-gray-800">Panel Debate: <em>Is vision all we need?</em></td></tr>
            <tr class="bg-gray-50"><td class="px-6 py-3 font-mono text-gray-500">12:15 PM</td><td class="px-6 py-3 text-gray-800">Conclusion</td></tr>
            <tr class="bg-white border-t border-gray-200"><td class="px-6 py-3 font-mono text-gray-400">12:30 PM</td><td class="px-6 py-3 text-gray-400">Workshop Ends</td></tr>
          </tbody>
        </table>
      </div>
    </div>
  </section>

  <!-- SECTIONS WILL GO HERE -->
```

**Step 2: Verify in browser**

Expected: Navy-header table with alternating white/gray rows, monospace time column, full schedule.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add schedule section"
```

---

### Task 6: Call for Papers section

**Files:**
- Modify: `index.html`

**Step 1: Replace `<!-- SECTIONS WILL GO HERE -->` with CFP section**

```html
  <!-- CALL FOR PAPERS -->
  <section id="cfp" class="bg-gray-50 py-16 px-4">
    <div class="max-w-3xl mx-auto">
      <h2 class="text-2xl font-bold text-navy mb-6">Call for Papers</h2>
      <p class="text-gray-700 leading-relaxed mb-6">
        We invite submissions of short papers (4 pages + references) and extended abstracts
        (2 pages) on topics including but not limited to: multimodal sensing for manipulation,
        foundation models for contact-rich tasks, tactile/haptic perception, force/torque
        estimation, multimodal fusion, contact-aware control, and evaluation protocols for
        sensory sufficiency.
      </p>
      <p class="text-gray-700 leading-relaxed mb-6">
        We welcome works-in-progress, ablation studies, negative results, and system papers
        with reproducible artifacts (datasets, protocols, benchmarks). Accepted contributions
        will be presented as posters with optional lightning talks.
      </p>
      <div class="bg-white rounded-lg border border-gray-200 p-6 mb-8">
        <h3 class="font-semibold text-gray-900 mb-3">Important Dates</h3>
        <ul class="text-sm text-gray-600 space-y-2">
          <li><span class="font-medium text-gray-800">Submission deadline:</span> TBD</li>
          <li><span class="font-medium text-gray-800">Notification:</span> TBD</li>
          <li><span class="font-medium text-gray-800">Camera-ready:</span> TBD</li>
          <li><span class="font-medium text-gray-800">Workshop:</span> IROS 2026, Abu Dhabi</li>
        </ul>
      </div>
      <a href="#" class="inline-block px-6 py-3 rounded border-2 border-navy text-navy font-semibold hover:bg-navy hover:text-white transition-colors">
        Submit on OpenReview
      </a>
    </div>
  </section>

  <!-- SECTIONS WILL GO HERE -->
```

**Step 2: Verify in browser**

Expected: Gray-background section with two paragraphs, a white dates card, and a Submit button.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add call for papers section"
```

---

### Task 7: Organizers section and footer

**Files:**
- Modify: `index.html`

**Step 1: Replace `<!-- SECTIONS WILL GO HERE -->` with organizers section and footer**

```html
  <!-- ORGANIZERS -->
  <section id="organizers" class="bg-white py-16 px-4">
    <div class="max-w-5xl mx-auto">
      <h2 class="text-2xl font-bold text-navy mb-10 text-center">Organizers</h2>
      <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-6">

        <div class="text-center">
          <img src="https://ui-avatars.com/api/?name=Haonan+Chen&size=200&background=e0e7ff&color=1e3a8a"
               alt="Haonan Chen"
               class="w-20 h-20 rounded-full mx-auto mb-2 object-cover" />
          <p class="font-semibold text-gray-900 text-sm">Haonan Chen</p>
          <p class="text-xs text-gray-500">Harvard University</p>
          <a href="https://haonan16.github.io/" class="text-xs text-navy hover:underline" target="_blank">website</a>
        </div>

        <div class="text-center">
          <img src="https://ui-avatars.com/api/?name=Shuijing+Liu&size=200&background=e0e7ff&color=1e3a8a"
               alt="Shuijing Liu"
               class="w-20 h-20 rounded-full mx-auto mb-2 object-cover" />
          <p class="font-semibold text-gray-900 text-sm">Shuijing Liu</p>
          <p class="text-xs text-gray-500">UT Austin</p>
          <a href="https://shuijing725.github.io" class="text-xs text-navy hover:underline" target="_blank">website</a>
        </div>

        <div class="text-center">
          <img src="https://ui-avatars.com/api/?name=Yuxiang+Ma&size=200&background=e0e7ff&color=1e3a8a"
               alt="Yuxiang Ma"
               class="w-20 h-20 rounded-full mx-auto mb-2 object-cover" />
          <p class="font-semibold text-gray-900 text-sm">Yuxiang Ma</p>
          <p class="text-xs text-gray-500">MIT</p>
          <a href="https://yuxiang-ma.github.io/" class="text-xs text-navy hover:underline" target="_blank">website</a>
        </div>

        <div class="text-center">
          <img src="https://ui-avatars.com/api/?name=Mingyo+Seo&size=200&background=e0e7ff&color=1e3a8a"
               alt="Mingyo Seo"
               class="w-20 h-20 rounded-full mx-auto mb-2 object-cover" />
          <p class="font-semibold text-gray-900 text-sm">Mingyo Seo</p>
          <p class="text-xs text-gray-500">UT Austin</p>
          <a href="https://mingyoseo.com/" class="text-xs text-navy hover:underline" target="_blank">website</a>
        </div>

        <div class="text-center">
          <img src="https://ui-avatars.com/api/?name=Raven+Huang&size=200&background=e0e7ff&color=1e3a8a"
               alt="Raven Huang"
               class="w-20 h-20 rounded-full mx-auto mb-2 object-cover" />
          <p class="font-semibold text-gray-900 text-sm">Raven Huang</p>
          <p class="text-xs text-gray-500">Stanford University</p>
          <a href="https://qingh097.github.io/" class="text-xs text-navy hover:underline" target="_blank">website</a>
        </div>

      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <footer class="bg-gray-900 text-gray-400 py-8 px-4">
    <div class="max-w-5xl mx-auto flex flex-col md:flex-row items-center justify-between gap-4 text-sm">
      <p>&copy; 2026 Small Data, Rich Sensing Workshop Organizers</p>
      <p>Contact: <a href="mailto:haonan_chen@seas.harvard.edu" class="text-gray-300 hover:text-white transition-colors">haonan_chen@seas.harvard.edu</a></p>
      <div class="flex gap-4">
        <a href="#overview" class="hover:text-white transition-colors">About</a>
        <a href="#speakers" class="hover:text-white transition-colors">Speakers</a>
        <a href="#cfp" class="hover:text-white transition-colors">CFP</a>
      </div>
    </div>
  </footer>
```

**Step 2: Verify in browser**

Expected: 5 organizer avatars in a row (or 2-3 columns on mobile), each with name/institution/website link. Dark footer below with copyright, contact email, and nav links.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add organizers section and footer"
```

---

### Task 8: Final polish — mobile responsiveness and scroll shadow on nav

**Files:**
- Modify: `index.html`

**Step 1: Add scroll shadow to nav using vanilla JS**

Inside `<body>`, before `</body>`, add:

```html
<script>
  window.addEventListener('scroll', () => {
    const nav = document.getElementById('navbar');
    if (window.scrollY > 10) {
      nav.classList.add('shadow-sm');
    } else {
      nav.classList.remove('shadow-sm');
    }
  });
</script>
```

**Step 2: Verify responsive layout**

Open browser DevTools, toggle mobile view (375px width).
Expected: Nav links wrap or collapse gracefully, speaker/organizer cards stack to 2 columns, hero text scales down, buttons stack vertically if needed.

If nav overflows on mobile, replace the nav links div with:
```html
<div class="flex items-center gap-3 text-sm font-medium text-gray-600 flex-wrap justify-end">
```

**Step 3: Verify full page scroll**

Click each nav link, confirm smooth scroll to the correct section.

**Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add nav scroll shadow and mobile layout fixes"
```

---

### Task 9: Add placeholder note for speaker photos

**Files:**
- Modify: `index.html`

**Step 1: Add an HTML comment above each speaker image**

For each of the 4 speakers, add a comment so organizers know where to swap in real photos:

```html
<!-- Replace src with real photo, e.g. assets/jie-tan.jpg (200x200 recommended) -->
<img src="https://ui-avatars.com/api/?name=Jie+Tan&size=200&background=1e3a8a&color=fff" ... />
```

Do the same for the 5 organizer images, pointing to `assets/` folder.

**Step 2: Create assets directory with a README**

```bash
mkdir -p assets
echo "Place speaker and organizer photos here (200x200 px JPG or PNG recommended)." > assets/README.txt
```

**Step 3: Commit**

```bash
git add index.html assets/README.txt
git commit -m "docs: add photo placeholder comments and assets README"
```

---

## Done

The site is now complete and deployable. GitHub Pages will serve `index.html` automatically from the `main` branch root.

**To enable GitHub Pages:** Go to repo Settings → Pages → Source: Deploy from branch `main`, folder `/` (root).

**Next updates to make once content is finalized:**
- Replace `ui-avatars.com` placeholders with real speaker/organizer photos in `assets/`
- Fill in OpenReview submission link in the CFP section
- Fill in paper submission deadlines
- Update "Invited Talk 1–4" in the schedule with actual speaker names once assigned
