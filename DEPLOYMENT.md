# Deploy to Render

1. Push this repository to GitHub.
2. Sign in to [Render](https://render.com), choose **New > Blueprint**, and connect `yashsirsat/seml-project`.
3. Confirm the `seml-bus-tracking` web service from `render.yaml` and deploy it. Render will provide a public `onrender.com` URL when the build finishes.
4. If booking confirmation emails are needed, set `MAIL_USERNAME` and `MAIL_PASSWORD` in the service's environment settings. Do not commit credentials.

The free web service may sleep when idle. User accounts use `DATABASE_URL` when configured; otherwise they use SQLite on Render's ephemeral filesystem. Bookings and live bus locations are held in memory and reset when the service restarts. Configure persistent storage before relying on the app for real bookings or continuous tracking.
