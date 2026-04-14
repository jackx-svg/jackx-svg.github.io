# jackx-svg.github.io

Hexo personal blog powered by the Butterfly theme.

## Development

```bash
npm ci
npm run server
```

## Build

```bash
npm run build
```

## Deployment

GitHub Pages deployment is handled by `.github/workflows/deploy.yml`.

Push source changes to the `main` branch. GitHub Actions installs dependencies, builds the Hexo site, uploads the generated `public` directory as a Pages artifact, and deploys it to GitHub Pages.

Do not commit `node_modules`, `public`, `.deploy_git`, `db.json`, or local backups.
