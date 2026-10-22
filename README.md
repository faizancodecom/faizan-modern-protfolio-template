# Modern Developer Portfolio Template

A clean, responsive personal portfolio template designed for developers and designers. The project features a dual-layout architecture with dedicated desktop and mobile views, animated navigation transitions, and zero build tool dependencies.

---

## Overview

This template provides a production-ready baseline for showcasing personal projects, technical skillsets, and contact channels. Built entirely with semantic HTML5, modern CSS3, and vanilla JavaScript, it runs directly in any modern browser without requiring package installations or build steps.

Key characteristics:
- Native Web Standards: Zero framework runtime overhead, fast loading times, and high performance out of the box.
- Dual-Viewport Design: Dedicated layouts tailored specifically for desktop screens (`index.html`) and mobile touchscreens (`mobile.html`) with automated device redirection.
- Accessible Structure: Valid HTML5 semantics with structured metadata for search engines and social sharing.

---

## File Structure

```
faizan-modern-protfolio-template/
|-- .gitattributes          # Git configuration for consistent text line endings
|-- .gitignore              # Rules for ignoring local caches, environment files, and system artifacts
|-- index.html              # Main desktop view with interactive navigation and project showcase
|-- mobile.html             # Mobile-optimized view with touch-friendly navigation drawer
|-- README.md               # Documentation and customization guide
|-- css/
|   |-- mobile.css          # Styling, responsive layouts, and menu styles for mobile view
|   |-- style.css           # Styling, keyframe animations, and view layouts for desktop view
|   `-- vars.css            # Global CSS variables and design tokens
`-- images/
    `-- image-10.png        # Default profile portrait asset
```

---

## Getting Started

### 1. Clone the Repository

Clone the project to your local machine using Git:

```bash
git clone https://github.com/faizancodecom/faizan-modern-protfolio-template.git
cd faizan-modern-protfolio-template
```

### 2. View the Website Locally

Since the template uses static files, you can view it locally using any of the following methods:

#### Method A: Direct Browser Opening
Double-click `index.html` or drag it into any web browser (Chrome, Firefox, Edge, Safari).

#### Method B: VS Code Live Server (Recommended)
1. Open the project folder in VS Code.
2. Install the **Live Server** extension if not already installed.
3. Right-click `index.html` and choose **Open with Live Server**.

#### Method C: Local HTTP Server
Using Python:
```bash
python -m http.server 8000
```
Or using Node.js:
```bash
npx serve .
```

Once started, open `http://localhost:8000` in your web browser.

---

## Customization Guide

You can easily adapt this template for your own profile by modifying the files described below.

### 1. Personal Identity and Metadata

Open both `index.html` and `mobile.html` to update your details:

- **Page Title**: Change the `<title>` tag with your name and profession.
- **Meta Tags**: Update `<meta name="description">`, `<meta name="keywords">`, and `<meta name="author">`.
- **Open Graph / Twitter Cards**: Replace `og:title`, `og:description`, and Twitter card metadata for social preview links.
- **JSON-LD Schema**: Update the structured data block in the `<head>` of `index.html`:

```json
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "Your Name",
  "jobTitle": "Your Professional Role",
  "knowsAbout": ["HTML5", "CSS3", "JavaScript", "React", "Node.js"]
}
```

### 2. Profile Image

Replace the default avatar image with your own portrait:
- Save your image to `images/image-10.png` (or provide a new file name).
- If using a different file name, update the `src` attribute in `index.html` (`.image-1`) and `mobile.html` (`.m-image-wrap img`).

### 3. Skills Section

The skills section displays cards with technology icons and titles.
- In `index.html`: Edit the `.skills-grid` container to add, edit, or remove skills.
- In `mobile.html`: Edit the `.m-skills-grid` container to match your technical competencies.

### 4. Projects Showcase

Default projects are configured in JavaScript arrays within the HTML files:

- **Desktop (`index.html`)**: Locate the `DEFAULT_PROJECTS` array inside the `<script>` block near the bottom of the file:

```javascript
const DEFAULT_PROJECTS = [
  {
    id: 'd-project-one',
    name: 'Project Title',
    desc: 'Brief description of the project architecture and features.',
    tags: ['HTML', 'CSS', 'JavaScript'],
    url: 'https://your-live-demo-link.com/',
    thumb: 'https://your-domain.com/thumbnail.png'
  }
];
```

- **Mobile (`mobile.html`)**: Locate the `PROJECTS` array in the `<script>` section of `mobile.html` and apply the same project information.

### 5. Social and Contact Links

Update your public contact channels:
- In `index.html`: Locate `.page-contact .contact-grid` and update the `href` attributes and display text for your GitHub, YouTube, LinkedIn, or Email.
- In `mobile.html`: Locate `.m-contact-grid` and update the corresponding links.

Example GitHub link:
```html
<a class="contact-card" href="https://github.com/faizancodecom" target="_blank" rel="noopener noreferrer">
  <div class="contact-info">
    <div class="contact-label">GitHub</div>
    <div class="contact-value">faizancodecom</div>
  </div>
</a>
```

### 6. Colors and Styling

- **Theme Tokens**: Modify global CSS values in `css/vars.css` to change primary colors, backgrounds, and accents.
- **Desktop Styles**: Adjust layout spacing, typography, and card transitions in `css/style.css`.
- **Mobile Styles**: Adjust mobile typography, drawer behavior, and padding in `css/mobile.css`.

---

## Deployment

Deploying this portfolio takes only a few minutes on any static hosting platform.

### GitHub Pages

1. Push your repository to GitHub.
2. Go to **Settings** > **Pages** in your repository.
3. Set the source branch to `main` and root directory to `/ (root)`.
4. Click **Save**. Your site will be published at `https://<username>.github.io/<repo-name>/`.

### Vercel

Run the following command from the project root:
```bash
vercel --prod
```
Or import the repository directly via the [Vercel Dashboard](https://vercel.com).

### Netlify

Drag and drop your project directory directly into the [Netlify App](https://app.netlify.com/drop), or deploy via CLI:
```bash
netlify deploy --prod --dir=.
```

---

## License

This project is open-source and free to use under the MIT License.
