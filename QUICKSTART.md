# Quick Start Guide

## Installation Complete! ✅

All Python packages are installed. Follow these steps to run your quiz system.

## Step 1: PostgreSQL Setup (5 minutes)

### Install PostgreSQL
Download from: https://www.postgresql.org/download/windows/

During installation:
- Set a password for the `postgres` user (remember this!)
- Port: 5432 (default)
- Accept other defaults

### Create Database

Open Command Prompt or PowerShell and run:

```bash
# Connect to PostgreSQL
psql -U postgres

# Enter your password when prompted
# Then run this SQL command:
CREATE DATABASE quiz_system;

# Exit
\q
```

### Load Database Schema

```bash
# Navigate to project directory
cd "c:\M2R-ISDI\ISDI 506 - Communication Infrastructures & Platforms for Ambient Intelligence\quiz_classpoint_pp"

# Load schema
psql -U postgres -d quiz_system -f schema.sql
```

## Step 2: Configure Environment (1 minute)

Create `.env` file in the project directory:

```bash
copy .env.example .env
```

Edit `.env` (use Notepad) and set your PostgreSQL password:

```
DB_HOST=localhost
DB_PORT=5432
DB_NAME=quiz_system
DB_USER=postgres
DB_PASSWORD=YOUR_POSTGRES_PASSWORD_HERE
```

## Step 3: Run the Application (30 seconds)

```bash
# Navigate to project directory
cd "c:\M2R-ISDI\ISDI 506 - Communication Infrastructures & Platforms for Ambient Intelligence\quiz_classpoint_pp"

# Run the app
python -m streamlit run app.py
```

The app will open in your browser at `http://localhost:8501`

## Quick Test

### Test as Presenter:
1. Click "Login as Presenter"
2. Enter your name: "Test Teacher"
3. Click "Create Quiz" in sidebar
4. Title: "Sample Quiz"
5. Add a question:
   - Question: "What is 2+2?"
   - A: "3"
   - B: "4"
   - C: "5"
   - Correct: B
6. Click "Launch Session"
7. Note the session code (e.g., "ABC123")

### Test as Participant (in another browser/tab):
1. Open `http://localhost:8501` in incognito/private window
2. Click "Login as Participant"
3. Enter name: "Test Student"
4. Enter session code from above
5. Answer the question
6. See if you got it right!

### View Results:
1. Go back to Presenter window
2. Click "View Results" in sidebar
3. Select your session
4. See the bar chart with responses!

## Common Commands

### Run the app:
```bash
python -m streamlit run app.py
```

### Stop the app:
Press `Ctrl+C` in the terminal

### Check if PostgreSQL is running:
```bash
pg_isready
```

### Connect to database:
```bash
psql -U postgres -d quiz_system
```

## Troubleshooting

### "Module not found" error
Reinstall dependencies:
```bash
python -m pip install streamlit pandas plotly "psycopg[binary]" python-dotenv
```

### "Connection refused" error
- PostgreSQL is not running
- Check Windows Services for "postgresql" service
- Or restart: `pg_ctl restart`

### "Password authentication failed"
- Check password in `.env` file
- Make sure it matches your PostgreSQL password

### Streamlit doesn't open browser
Manually go to: `http://localhost:8501`

## Project Structure

```
quiz_classpoint_pp/
├── app.py                 # Run this file
├── database.py           # Database operations
├── schema.sql            # Database structure
├── .env                  # Your config (create this)
├── .env.example         # Config template
└── README.md            # Full documentation
```

## Need More Help?

- Full documentation: [README.md](README.md)
- Windows installation: [INSTALL_WINDOWS.md](INSTALL_WINDOWS.md)
- Installation status: [INSTALLATION_SUCCESS.md](INSTALLATION_SUCCESS.md)

---

**Ready to go!** Run `python -m streamlit run app.py` to start!
