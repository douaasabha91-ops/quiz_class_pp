# Interactive Quiz System (ClassPoint-like)

An interactive quiz application built with Python, Streamlit, and PostgreSQL that simulates ClassPoint-like functionality. This system allows presenters to create quizzes and launch interactive sessions, while participants can join using session codes and answer questions in real-time.

## Features

### Presenter Features
- Create and manage multiple-choice quizzes
- Add questions with 2-4 answer options
- Launch quiz sessions with unique session codes
- View active sessions
- Monitor real-time results with interactive charts
- Track participant responses and accuracy

### Participant Features
- Join sessions using 6-character session codes
- Answer multiple-choice questions
- View submission status
- See if answers were correct/incorrect

## Technology Stack

- **Python 3.x** - Application logic
- **Streamlit** - Web interface for both presenters and participants
- **PostgreSQL** - Database for storing quizzes, sessions, and responses
- **psycopg2** - PostgreSQL database connectivity
- **Plotly** - Interactive data visualization
- **Pandas** - Data manipulation

## Database Schema

The system uses the following PostgreSQL tables:

1. **users** - Stores user information (id, name, role)
2. **quizzes** - Stores quiz metadata (id, title, created_at, created_by)
3. **questions** - Stores quiz questions (id, quiz_id, text, options A-D, correct_answer)
4. **sessions** - Stores active quiz sessions (id, quiz_id, session_code, is_active)
5. **responses** - Stores participant answers (id, question_id, user_id, session_id, answer, is_correct)

## Installation

### Prerequisites
- Python 3.9-3.11 recommended (3.14 may have compatibility issues)
- PostgreSQL 12 or higher
- pip (Python package manager)

**Windows Users:** If you encounter installation errors, see [INSTALL_WINDOWS.md](INSTALL_WINDOWS.md) for detailed troubleshooting.

### Step 1: Clone or Download the Project

```bash
cd quiz_classpoint_pp
```

### Step 2: Install Python Dependencies

**Option A: Quick install (may fail on Windows)**
```bash
pip install -r requirements.txt
```

**Option B: Windows users with build errors**
```bash
# Run the automated setup script
setup_windows.bat

# OR install manually (see INSTALL_WINDOWS.md)
```

**Option C: Using Anaconda (recommended for Windows)**
```bash
conda create -n quiz_system python=3.11
conda activate quiz_system
conda install -c conda-forge streamlit pandas plotly python-dotenv psycopg2
```

### Step 3: Set Up PostgreSQL Database

1. Install PostgreSQL if not already installed
2. Create a new database:

```bash
psql -U postgres
CREATE DATABASE quiz_system;
\q
```

3. Run the schema file to create tables:

```bash
psql -U postgres -d quiz_system -f schema.sql
```

### Step 4: Configure Environment Variables

1. Copy the example environment file:

```bash
cp .env.example .env
```

2. Edit the `.env` file with your PostgreSQL credentials:

```
DB_HOST=localhost
DB_PORT=5432
DB_NAME=quiz_system
DB_USER=postgres
DB_PASSWORD=your_actual_password
```

## Running the Application

### Start the Streamlit Application

```bash
streamlit run app.py
```

The application will open in your default web browser at `http://localhost:8501`

## Usage Guide

### For Presenters

1. **Login**
   - Open the application
   - Select "Login as Presenter"
   - Enter your name

2. **Create a Quiz**
   - Navigate to "Create Quiz" in the sidebar
   - Enter a quiz title
   - Add questions with 2-4 multiple-choice options
   - Specify the correct answer for each question
   - Click "Done Adding Questions" when finished

3. **Launch a Session**
   - Navigate to "Launch Session"
   - Select a quiz from the dropdown
   - Click "Launch Session"
   - Share the generated 6-character session code with participants

4. **Monitor Active Sessions**
   - Navigate to "Active Sessions"
   - View all running sessions
   - End sessions when complete

5. **View Results**
   - Navigate to "View Results"
   - Select a session to analyze
   - View interactive bar charts showing response distributions
   - See accuracy percentages for each question

### For Participants

1. **Login**
   - Open the application
   - Select "Login as Participant"
   - Enter your name

2. **Join a Session**
   - Enter the 6-character session code provided by the presenter
   - Click "Join Session"

3. **Answer Questions**
   - Read each question carefully
   - Select your answer from the multiple-choice options
   - Click "Submit Answer"
   - See immediate feedback on whether your answer was correct

4. **Leave Session**
   - Click "Leave Session" button when done

## Project Structure

```
quiz_classpoint_pp/
├── app.py                  # Main Streamlit application
├── database.py            # Database operations and queries
├── schema.sql             # PostgreSQL database schema
├── requirements.txt       # Python dependencies
├── .env.example          # Environment variables template
├── .env                  # Your local configuration (not in git)
└── README.md             # This file
```

## Key Functions

### Database Operations (database.py)

- `create_user()` - Register new users
- `create_quiz()` - Create new quizzes
- `add_question()` - Add questions to quizzes
- `create_session()` - Generate session with unique code
- `submit_response()` - Record participant answers
- `get_question_results()` - Aggregate results for visualization

### Application Pages (app.py)

- `login_page()` - User authentication
- `presenter_interface()` - Presenter dashboard
- `participant_interface()` - Participant view
- `display_session_results()` - Real-time results visualization

## Features Implemented

✅ Multiple-choice quiz creation
✅ PostgreSQL database integration
✅ Unique session code generation
✅ Real-time answer submission
✅ Interactive results visualization (bar charts)
✅ Presenter and participant interfaces
✅ Session management (launch/end)
✅ Answer correctness tracking
✅ Clean and intuitive UI

## Troubleshooting

### Database Connection Issues
- Verify PostgreSQL is running: `pg_isready`
- Check credentials in `.env` file
- Ensure database exists: `psql -U postgres -l`

### Module Import Errors
- Reinstall dependencies: `pip install -r requirements.txt`
- Use a virtual environment to avoid conflicts

### Session Code Not Working
- Verify session is active in "Active Sessions"
- Session codes are case-sensitive (automatically converted to uppercase)
- Check if session was ended by presenter

## Demo Video

A demonstration video showing:
1. Presenter creating a quiz
2. Launching a session
3. Participant joining and answering questions
4. Viewing real-time results

(Video file to be created separately)

## Assignment Requirements Checklist

- [x] Python 3.x application logic
- [x] Streamlit web interface
- [x] PostgreSQL database
- [x] psycopg2 database connectivity
- [x] Presenter interface (create quizzes, launch sessions, view results)
- [x] Participant interface (join with code, submit answers)
- [x] Multiple-choice questions
- [x] Session code generation
- [x] Live results visualization (bar charts)
- [x] Minimum database tables (users, quizzes, questions, responses, sessions)
- [x] PostgreSQL transactions
- [x] Clean and readable UI
- [x] Source code with comments
- [x] README with setup instructions

## Future Enhancements

- Real-time auto-refresh for results
- Question timers
- Leaderboard functionality
- Export results to CSV/PDF
- Question banks and categories
- Image support in questions
- True/False and short answer questions

## License

Educational project for ISDI 506 - Communication Infrastructures & Platforms for Ambient Intelligence

## Author

Created as part of the Interactive Quiz Add-in Assignment
