# keep-it-warm

Keeps a [Render](https://render.com) free-tier web service warm by pinging it every ~10 minutes via a GitHub Actions scheduled workflow, preventing it from spinning down due to inactivity.

## How it works

The workflow in [`.github/workflows/keep-warm.yml`](.github/workflows/keep-warm.yml) runs on a cron schedule (`*/10 * * * *`) and sends a `curl` request to the target URL.

Currently configured to ping: **https://cineorama.onrender.com**

## Changing the target URL

Edit the `RENDER_URL` value in `.github/workflows/keep-warm.yml`:

```yaml
env:
  RENDER_URL: https://your-app.onrender.com
```

## Manual run

Go to the **Actions** tab → **Keep Render App Warm** → **Run workflow**.

## Notes

- GitHub Actions scheduled workflows may be delayed a few minutes during low-activity periods — this is normal and still prevents the ~15 minute Render free-tier sleep timeout.
- Make sure the target URL responds with a reachable page (not behind auth) so the `curl` ping succeeds.
