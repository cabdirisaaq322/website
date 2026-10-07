# DownloadHub — free hosting on Render + Cloudflare R2

## PART 1 — Put code on GitHub (5 min)
1. Create account at https://github.com, New repository `downloadhub`, Public.
2. In this folder, run:
```
git init
git add .
git commit -m "DownloadHub store"
git branch -M main
git remote add origin https://github.com/YOURNAME/downloadhub.git
git push -u origin main
```
(Windows will ask login once — allow it.)

## PART 2 — Free R2 bucket so APKs never get deleted (5 min)
Render free disk wipes uploads on every restart. R2 free = 10 GB/month, no card.
1. https://dash.cloudflare.com → sign up → R2 Object Storage → Create bucket `downloads`.
2. R2 → Manage R2 API Tokens → Create API Token (Object Read & Write) → copy Access Key + Secret.
3. Bucket → Settings → Public access → Allow Access via `r2.dev` subdomain → copy that URL (looks like https://pub-xxxx.r2.dev).
4. Save: endpoint = https://<accountid>.r2.cloudflarestorage.com (shown on bucket page), bucket = downloads, keys, public URL.

## PART 3 — Deploy on Render (3 min)
1. https://render.com → sign up with GitHub → New + → Web Service → select `downloadhub` repo.
2. Render detects `render.yaml` + `Dockerfile` automatically. Click Create.
3. After first deploy, go to Environment tab and fill: STORAGE_DRIVER=r2, R2_ENDPOINT, R2_BUCKET=downloads, R2_ACCESS_KEY, R2_SECRET_KEY, R2_PUBLIC_URL → Save → Manual Deploy → Deploy latest.
4. Open https://downloadhub-xxxx.onrender.com — store is live. Admin: /admin (key admin123 — change it in admin Settings!).

## PART 4 — How to upload apps (from your phone or PC)
1. Open YOUR-SITE.onrender.com/admin → type key admin123 → Connect (✅ stats).
2. 🖼 Hero Slider (optional): edit 3 moving pictures first.
3. ⬆ Publish App: name*, developer, category, version, description, changelog.
4. APK file → Choose File → pick .apk from device → Featured/Trending ticks → Publish.
   - File goes straight to your R2 bucket (progress = "Uploading...").
   - No file? Paste Google Drive/MediaFire direct link — Download button redirects there.
5. New app appears on homepage instantly. Tap it → DOWNLOAD → real APK installs.
6. First load after idle takes ~50s (Render free sleeps) — normal.
