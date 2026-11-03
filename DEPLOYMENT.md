# Deploy to Vercel or Render

## Vercel

1. Import the Git repository into Vercel. Set **Root Directory** to the directory containing `app.py`, `requirements.txt`, `templates/`, `static/`, and `msrtc_bus_data_sample.csv` (the repository root for this project).
2. Keep the framework preset on **Other** or allow Vercel to detect Flask. The Python runtime detects the `app` instance in `app.py`; a custom `vercel.json` routing file is not required.
3. Add `SECRET_KEY` as an environment variable with a stable, randomly generated value, then redeploy. Add `DATABASE_URL` for a hosted PostgreSQL database if account data needs to survive function restarts. The Vercel SQLite fallback in `/tmp` is only temporary and is not durable.
4. Open the deployment and check **Runtime Logs** if it still returns an error. A database connection failure usually means `DATABASE_URL` is missing, invalid, or not reachable from Vercel.

The app's CSV file is resolved relative to `app.py`, so it works independently of the function's working directory. Do not commit database credentials or secret keys.

## Render

1. Push this repository to GitHub.
2. Sign in to [Render](https://render.com), choose **New > Blueprint**, and connect `yashsirsat/seml-project`.
3. Confirm the `seml-bus-tracking` web service from `render.yaml` and deploy it. Render will provide a public `onrender.com` URL when the build finishes.
4. If booking confirmation emails are needed, set `MAIL_USERNAME` and `MAIL_PASSWORD` in the service's environment settings. Do not commit credentials.

The free web service may sleep when idle. User accounts use `DATABASE_URL` when configured; otherwise they use SQLite on Render's ephemeral filesystem. Bookings and live bus locations are held in memory and reset when the service restarts. Configure persistent storage before relying on the app for real bookings or continuous tracking.
