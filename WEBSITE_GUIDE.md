## Personal Website: Build, Update, and Maintenance Guide

### Overview
This site is built with Astro. It’s a static site that you can develop locally, build to a `dist/` folder, and deploy to any static hosting provider.

### Tech Stack and Requirements
- **Framework**: Astro (package: `astro`)
- **Astro version**: defined in `package.json` (`^5.12.9`)
- **Node**: `>= 18.17` (see `engines.node` in `package.json`)

### Project Structure (key files)
- `src/pages/index.astro`: Home page
- `src/layouts/Layout.astro`: Base HTML layout (sets `<title>`, favicon, etc.)
- `src/components/Welcome.astro`: Example component used on the home page
- `src/assets/`: Project images/assets used by components
- `public/`: Static files copied as-is to the site root (e.g., `favicon.svg`)
- `astro.config.ts`: Astro configuration. Uses `BASE_PATH` env var to set `base` when deploying under a subpath

### Scripts
- `npm run dev`: Start the local dev server (default at `http://localhost:4321`)
- `npm run build`: Build the production site to `./dist/`
- `npm run preview`: Preview the production build locally

### Develop Locally
```sh
npm install
npm run dev
```
Then edit files under `src/` and the browser will live-reload.

### How to Update Content
- **Edit the home page**: Update `src/pages/index.astro`.
- **Create new pages**: Add new `.astro` files under `src/pages/` (e.g., `src/pages/about.astro` will be available at `/about`).
- **Update layout/metadata**: Edit `src/layouts/Layout.astro` (e.g., change `<title>`, add meta tags, analytics, fonts, etc.).
- **Add or update assets**:
  - For files that should have friendly URLs and not be processed, put them in `public/` (served at the site root).
  - For images imported by components, place them in `src/assets/` and import them in `.astro` files.
- **Favicon**: Replace `public/favicon.svg`.

### Configuration
- `astro.config.ts` uses:
  ```ts
  export default defineConfig({
    base: process.env.BASE_PATH ?? "/",
  });
  ```
  - Set `BASE_PATH` when deploying under a subpath (e.g., GitHub Pages repo site):
    ```sh
    # example: deploy at https://user.github.io/repo
    export BASE_PATH="/repo"
    npm run build
    ```
  - For root-level deploys (custom domain or user site), you can leave `BASE_PATH` unset.

### Build and Deploy
1. Build the site:
   ```sh
   npm run build
   ```
   The output is in `dist/`.
2. Deploy the `dist/` folder to your hosting provider:
   - Any static hosting (S3/CloudFront, Nginx, Apache, Netlify, Vercel, GitHub Pages, Cloudflare Pages) works.
   - For providers that build from source, set:
     - **Build command**: `npm run build`
     - **Output directory**: `dist`
     - **Install command**: `npm install`
   - If deploying under a subpath, ensure `BASE_PATH` is set in the build environment.

### Keeping Things Up To Date
- **Dependencies**:
  ```sh
  npm outdated          # see what can be updated
  npm update            # safe, semver-compatible updates
  npm install astro@latest  # upgrade Astro to the latest
  ```
- **Node**: Use `nvm` (or your tool of choice) to stay on Node `>= 18.17`.
- **Astro checks** (optional but helpful):
  ```sh
  npx astro check
  ```

### Common Tweaks
- Update the site title in `src/layouts/Layout.astro`.
- Add meta tags (description, Open Graph, Twitter) in `Layout.astro`.
- Add new sections/components under `src/components/` and include them in pages.

### Troubleshooting
- Blank or broken links under a subpath: confirm `BASE_PATH` matches your deployed subpath and rebuild.
- Favicon not changing: your browser may have cached it; hard-refresh or clear cache.
- Incorrect assets path: files in `public/` are served from `/`, while imported assets under `src/assets/` are bundled and referenced via imports.

### Useful Links
- Astro docs: [https://docs.astro.build](https://docs.astro.build)
- Project structure: [https://docs.astro.build/en/basics/project-structure/](https://docs.astro.build/en/basics/project-structure/)


