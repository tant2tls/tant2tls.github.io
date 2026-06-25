# tant2tls.github.io

Personal academic page for Tan Ngo.

## Deploy to GitHub Pages

1. Create a new repo on GitHub named exactly `tant2tls.github.io` (must match your username).
2. From this folder:
   ```bash
   git init
   git add .
   git commit -m "Initial site"
   git branch -M main
   git remote add origin https://github.com/tant2tls/tant2tls.github.io.git
   git push -u origin main
   ```
3. GitHub Pages auto-publishes from `main`. Live at `https://tant2tls.github.io` within ~1 minute.

## Local preview

Just open `index.html` in a browser. No build step.

For a real server (so relative links work cleanly):
```bash
python -m http.server 8000
# visit http://localhost:8000
```

## Customize

- **Add your photo**: drop a square `profile.jpg` (recommended 400×400 or larger) next to `index.html`. The page picks it up automatically; if missing, it falls back to "TN" initials.
- **Add your CV PDF**: drop `CV.pdf` next to `index.html`. The "CV" link in the header points to it.
- **Edit content**: everything is in `index.html`. Sections are labeled with HTML comments.
- **Add a publication**: copy a `<div class="pub">` block in the Publications section.
- **Add a news item**: copy a `<li>` block in the News section.
