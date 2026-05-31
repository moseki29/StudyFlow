# StudyFlow

Smart study planner with module weighting, personalized timetables, daily reminders, and offline support. Data is stored in **Supabase** (PostgreSQL + Auth).

## Setup

### 1. Create a Supabase project

1. Go to [supabase.com](https://supabase.com) and create a project.
2. Open **Project Settings → API** and copy:
   - Project URL
   - `anon` public key
   - `service_role` secret key (keep private)

### 2. Run the database schema

In Supabase **SQL Editor**, paste and run the contents of:

```
supabase/schema.sql
```

### 3. Configure environment

```bash
cp .env.example .env
```

Edit `.env` with your Supabase keys:

```env
SUPABASE_URL=https://xxxxx.supabase.co
SUPABASE_ANON_KEY=eyJ...
SUPABASE_SERVICE_ROLE_KEY=eyJ...
```

### 4. Install and run

```bash
npm install
npm run init-admin    # creates admin user (once)
npm start
```

Open [http://localhost:3000](http://localhost:3000)

**Default admin** (after `init-admin`):

- Email: `admin@studyflow.local`
- Password: `admin123`

Change via `.env` before running `init-admin`.

## Features

| Feature | Description |
|--------|-------------|
| **Auth** | Sign up / log in via Supabase Auth |
| **Modules** | Upload CSV/JSON with difficulty 1–5 weighting |
| **Timetable** | Auto-generate by student type or upload CSV |
| **Study log** | Methods (revision, practice questions, etc.) + effectiveness |
| **Offline** | PWA cache + localStorage; syncs to Supabase when online |
| **Admin** | User list, stats, activity log (service role API) |

## CSV module format

```csv
name,code,difficulty
Mathematics,MATH101,4
Physics,PHYS201,5
```

## Project structure

```
StudyFlow/
  supabase/schema.sql   # Run in Supabase SQL Editor
  server/               # Express API → Supabase
  public/               # Frontend PWA
  .env                  # Your keys (not committed)
```

## Scripts

| Command | Description |
|---------|-------------|
| `npm start` | Start server |
| `npm run dev` | Start with auto-reload |
| `npm run init-admin` | Create/update admin user in Supabase |

## Security notes

- Never expose `SUPABASE_SERVICE_ROLE_KEY` in the browser.
- The server uses the service role only for API routes after verifying the user's JWT.
- Enable RLS policies in production (included in `schema.sql`).

## License

MIT
