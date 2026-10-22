# Faizan Modern Portfolio Template

A high-performance, zero-dependency personal portfolio and showcase engine built with semantic HTML5, modern CSS3, and vanilla JavaScript (ES6+). The project features a dual-viewport layout strategy, client-side project administration with persistent browser storage, sandboxed live previews, and automated viewport-based routing.

---

## Architectural Overview

This template avoids heavy runtime frameworks in favor of native web standards, minimizing bundle size and eliminating compilation steps while achieving optimal Lighthouse performance scores.

The codebase is organized around three primary systems:

1. **Dual-Viewport Layout Pipeline**: Instead of forcing a single complex DOM tree to accommodate vastly divergent mobile and desktop UX patterns, the application maintains two specialized front-end entry points:
   - `index.html`: A multi-view single-page interface for desktop viewports, utilizing CSS class toggling and keyframe animations for view transitions.
   - `mobile.html`: A vertical, touch-optimized document flow featuring an off-canvas navigation drawer and HTML5 History API URL masking.

2. **In-Browser Project Management Engine**: An integrated administrative subsystem embedded directly into the client. The interface is unlocked via a multi-click gesture on the brand identifier, allowing project additions and removals persisted through the Web Storage API (`localStorage`) without requiring an active backend server.

3. **Sandboxed Preview Architecture**: Project cards render live external applications inside sandboxed `<iframe>` wrappers, secured with strict permission policies to protect the host document against untrusted script execution.

---

## Directory Structure

```
faizan-modern-protfolio-template/
|-- .gitattributes          # Line-ending and Git normalization rules
|-- .gitignore              # Ignored patterns for OS, editors, and deployment caches
|-- index.html              # Desktop application entry point and administrative controller
|-- mobile.html             # Mobile-optimized application entry point
|-- README.md               # Engineering documentation
|-- css/
|   |-- mobile.css          # Layout, components, and typography for mobile viewports
|   |-- style.css           # Layout, animations, modals, and views for desktop viewports
|   `-- vars.css            # Root-level CSS custom properties and theme tokens
`-- images/
    `-- image-10.png        # Default author profile image asset
```

---

## Core Specifications

### Desktop View Controller (`index.html`)

- **View Routing**: Transitions between four primary views (`Home`, `Skills`, `Projects`, `Contact`) are orchestrated through class manipulation on the root `#app` container (`show-skills`, `show-projects`, `show-contact`).
- **SVG Kinetic Text Path**: An inline SVG path (`#fullCircle`) continuously animates circular brand typography around the profile centerpiece.
- **Showcase Grid & Pagination**: The projects view renders an array combining static defaults (`DEFAULT_PROJECTS`) and custom items retrieved from storage. Projects are paginated at three items per page with dynamic page calculation.
- **Embedded Sandbox Attributes**: Live previews enforce `loading="lazy"`, `referrerpolicy="no-referrer"`, and a restrictive sandbox attribute (`sandbox="allow-scripts allow-same-origin allow-forms allow-popups"`).
- **DOM Sanitization**: User-supplied values in the admin form pass through an entity-encoding helper (`escapeHtml`) before insertion into the document tree.

### Mobile View Controller (`mobile.html`)

- **Address Bar URL Masking**: Utilizes `window.history.replaceState` upon initial evaluation to strip `mobile.html` from the browser address bar, ensuring canonical root URL presentation.
- **Desktop Redirection Prompt**: Detects viewport widths equal to or exceeding 1024 pixels and provides an option to redirect to the desktop interface.
- **Touch-Friendly Drawer**: Pure CSS and lightweight JavaScript toggling for the off-canvas navigation menu with ARIA accessibility attributes (`aria-expanded`, `aria-label`).

### Administrative Subsystem

- **Authentication Trigger**: The primary brand element (`.faizan`) listens for 5 consecutive click events registered within a 2500-millisecond sliding time window.
- **Credential Validation**: Validates user credentials against an internal identifier and base64-encoded credential string.
- **Storage Schema**: Projects are serialized as JSON objects under the `customProjects_v1` storage key with the following schema:

```typescript
interface CustomProject {
  id: string;          // Format: 'custom-' + timestamp + random token
  name: string;        // Max length: 40 characters
  desc: string;        // Max length: 200 characters
  tags: string[];      // Array of up to 5 string tokens
  type: string;        // Preview type: 'iframe' | 'ecommerce' | 'dashboard' | etc.
  url: string;         // Fully-qualified HTTP/HTTPS URL
}
```

---

## Local Development

Because the project relies on modern web platform APIs (such as `localStorage`, `history.replaceState`, and `iframe` communication), it should be served via a local HTTP server rather than the `file://` protocol.

### Option 1: Node.js (`npx serve`)

```bash
npx serve .
```

### Option 2: Python 3 Built-in HTTP Server

```bash
python -m http.server 8000
```

### Option 3: VS Code Live Server Extension

Open the repository root in VS Code and click **Go Live** on the status bar, or right-click `index.html` and select **Open with Live Server**.

Once running, navigate to `http://localhost:8000` (or the port specified by your server).

---

## Configuration Guide

### 1. Author Metadata & Structured Data

Update the metadata tags in both `index.html` and `mobile.html` to reflect your identity:

- `<title>`: Browser tab title and search engine display.
- `<meta name="description">`: Page description for search indexation and social crawlers.
- `<meta name="keywords">`: Comma-separated technical keywords.
- Open Graph (`og:*`) and Twitter Card (`twitter:*`) tags.
- JSON-LD Structured Data: Update the schema block inside `<head>` in `index.html`:

```json
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "Your Name",
  "jobTitle": "Your Professional Title",
  "knowsAbout": ["HTML5", "CSS3", "JavaScript", "React", "TypeScript", "UI/UX Design"]
}
```

### 2. Admin Credentials

Default administrative credentials are defined within the script block of `index.html`:

- Default Username: `faizan_admin_2026`
- Default Password: `F@izan_Portfolio#2026!`

To update the password:

1. Encode your desired password into base64 (e.g., using `btoa("YourNewPassword")` in the browser console).
2. Update the `ADMIN_USER` and `ADMIN_PASS_B64` constants in `index.html`:

```javascript
const ADMIN_USER = 'your_username';
const ADMIN_PASS_B64 = btoa('your_new_password');
```

To access the panel: Click the brand name ("Faizan") in the desktop layout 5 times in rapid succession.

### 3. Default Projects Catalog

To modify the default projects that display when no custom projects exist in local storage, edit the `DEFAULT_PROJECTS` array located in `index.html`:

```javascript
const DEFAULT_PROJECTS = [
  {
    id: 'd-project-one',
    name: 'Project Title',
    desc: 'Brief summary of the architecture and stack.',
    tags: ['HTML', 'CSS', 'JavaScript'],
    url: 'https://example.com',
    thumb: 'https://example.com/thumbnail.png'
  }
];
```

### 4. Contact and Social Endpoints

Update the anchor links in the contact sections of `index.html` and `mobile.html`:

- YouTube channel reference
- GitHub account URL
- Direct mailto link (`mailto:yourname@example.com`)

---

## Deployment

The repository is structured as a static website and can be deployed instantly to any static hosting provider.

### Vercel

The project contains a pre-configured `.vercel` project mapping. To deploy using the Vercel CLI:

```bash
vercel --prod
```

### Netlify

Drag and drop the project root directory into the Netlify web dashboard, or deploy via the Netlify CLI:

```bash
netlify deploy --prod --dir=.
```

### GitHub Pages

1. Navigate to your repository settings on GitHub.
2. Select **Pages** from the sidebar.
3. Under **Branch**, select `main` and set the folder to `/ (root)`.
4. Click **Save**.

---

## Security and Best Practices

- **Cross-Site Scripting (XSS) Prevention**: All strings rendered from user input in the administrative panel undergo HTML entity encoding through `escapeHtml()` prior to DOM insertion.
- **Iframe Sandboxing**: When loading user-configured URLs inside preview cards, iframes are strictly isolated to prevent access to parent document cookies, local storage, or unwanted navigation.
- **Resource Preconnection**: External font resources (`fonts.googleapis.com` and `fonts.gstatic.com`) use `rel="preconnect"` links to reduce connection negotiation overhead during page load.

---

## Browser Support

- Chrome / Chromium-based browsers: Full support (version 90+)
- Mozilla Firefox: Full support (version 88+)
- Apple Safari: Full support (iOS and macOS, version 14+)
- Microsoft Edge: Full support (version 90+)

---

## License

This project is open-source and available under the terms of the MIT License.
