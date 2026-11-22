# HI5 Rentals on free hosting

The public fleet and request form are at `/`. The owner signs in at `/admin` to manage vehicles, replace their photos and review requests. Requests stay pending until the owner confirms availability and contacts the customer. The six starter listings come from the previous site. Replace the stock photos with photos of the actual fleet before accepting rentals.

## Deploy

Use a Neon Free Postgres project and the free Render Blueprint in this directory. Set these secrets in Render:

- `DATABASE_URL` is the Neon connection string with SSL enabled.
- `ADMIN_PASSWORD_HASH` is the Werkzeug password hash. Generate it with the app dependencies installed using `python -c 'from getpass import getpass; from werkzeug.security import generate_password_hash; print(generate_password_hash(getpass("Admin password: ")))'`.

Render generates `SECRET_KEY`. The app creates the database tables on first startup. Photos, fleet changes and bookings live in Postgres so they survive Render restarts. The existing static site can stay online until the replacement is verified. The new web service receives its own Render URL.
