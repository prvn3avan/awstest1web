# My Website — S3 + GitHub Actions Deploy

## Files
- `index.html`, `style.css` — the site itself
- `.github/workflows/deploy.yml` — auto-deploys to S3 on every push to `main`
- `bucket-policy.json` — attach this to your S3 bucket for public read access

## Setup

1. Replace `your-bucket-name` in **both** `deploy.yml` and `bucket-policy.json` with your actual S3 bucket name.
2. Replace `ap-south-1` in `deploy.yml` with your bucket's AWS region if different.
3. In AWS S3 Console:
   - Create the bucket, enable **Static website hosting**, set `index.html` as the index document.
   - Uncheck "Block all public access."
   - Paste `bucket-policy.json` into the bucket's Permissions → Bucket Policy.
4. In AWS IAM Console:
   - Create a user with only `s3:PutObject`, `s3:DeleteObject`, `s3:ListBucket` permissions scoped to your bucket.
   - Generate an access key pair.
5. In your GitHub repo → Settings → Secrets and variables → Actions, add:
   - `AWS_ACCESS_KEY_ID`
   - `AWS_SECRET_ACCESS_KEY`
6. Push this folder to your GitHub repo's `main` branch. The Action will run automatically and sync files to S3.
7. Visit your S3 static website endpoint (found in Properties → Static website hosting) to see it live.
