# Quick Reference Card

## 🚀 Start the App

```bash
python -m streamlit run app.py
```

---

## 👥 User Roles

### Presenter
- Create quizzes
- Add questions
- Launch sessions
- **NEW:** View which participant chose each answer
- Monitor results in real-time

### Participant
- Join sessions with code
- Answer questions
- **NEW:** Cannot change answers after submission
- See immediate feedback

---

## ✨ New Features

### Feature 1: See Who Answered What
**Location:** Presenter → View Results

**What you see:**
```
Answer A ❌ (2 people)
• Alice
• Bob

Answer B ✅ (3 people)
• Carol
• Dave
• Emma
```

### Feature 2: Answer Locking
**What happens:**
1. Participant selects answer
2. Clicks "Submit Answer"
3. Answer is locked forever
4. Cannot change or resubmit

**Protection:**
- UI blocks interaction
- Database rejects changes
- Warning message shown

---

## 📋 Common Tasks

### Create a Quiz
1. Login as Presenter
2. Sidebar → "Create Quiz"
3. Enter title
4. Add questions (minimum 2 options per question)
5. Click "Done Adding Questions"

### Launch a Session
1. Sidebar → "Launch Session"
2. Select quiz
3. Share the 6-character code with participants

### Join as Participant
1. Login as Participant
2. Enter session code
3. Answer questions
4. Submit (cannot change!)

### View Results
1. Sidebar → "View Results"
2. Select session
3. See:
   - Bar chart (left)
   - Participant names (right)
   - Accuracy metrics

---

## 🔐 Security Features

| Feature | Protection |
|---------|------------|
| Answer submission | Cannot resubmit |
| Data integrity | First answer preserved |
| UI security | Interactive elements removed |
| Database security | Error raised on duplicate |

---

## 🎯 Testing Checklist

### Test Participant Tracking
- [ ] Create quiz with 2+ questions
- [ ] Launch session
- [ ] Have 3+ participants join
- [ ] Each participant answers
- [ ] Go to View Results
- [ ] Verify participant names show under answers

### Test Answer Locking
- [ ] Join as participant
- [ ] Submit an answer
- [ ] Verify radio buttons disappear
- [ ] Verify warning message appears
- [ ] Try refreshing page
- [ ] Verify answer still locked

---

## 📊 Results View Layout

```
┌──────────────────────────────────────────┐
│ Question 1: [Question text]              │
│                                          │
│ Options: A) ... B) ... ✅ C) ... D) ... │
│ ─────────────────────────────────────── │
│                                          │
│ ┌────────────┬─────────────────────────┐│
│ │ Bar Chart  │  Participant Responses  ││
│ │ (60%)      │  (40%)                  ││
│ │            │  Answer A ❌ (2)        ││
│ │ [Chart]    │  • Name 1               ││
│ │            │  • Name 2               ││
│ │ Accuracy:  │                         ││
│ │ 75%        │  Answer B ✅ (3)        ││
│ │            │  • Name 3               ││
│ │            │  • Name 4               ││
│ │            │  • Name 5               ││
│ └────────────┴─────────────────────────┘│
└──────────────────────────────────────────┘
```

---

## 🎓 For Your Demo Video

**Must Show:**
1. Presenter creating quiz
2. Multiple participants joining
3. Participants answering questions
4. **Participant trying to change answer (fails)**
5. **Presenter viewing results with names**
6. Charts and accuracy metrics

**Explain:**
- "Prevents cheating through answer locking"
- "Allows tracking of individual performance"
- "Dual-layer security protection"

---

## 🔧 Troubleshooting

| Problem | Solution |
|---------|----------|
| Can't start app | Run: `python -m streamlit run app.py` |
| Database error | Check .env password |
| Names not showing | Refresh page, verify submissions |
| Answer not locking | Clear cache, restart app |
| Session code invalid | Check if session is active |

---

## 📂 Project Files

**Core Application:**
- `app.py` - Main Streamlit application
- `database.py` - Database operations
- `schema.sql` - Database structure

**Documentation:**
- `LATEST_UPDATES.md` - New features summary
- `FEATURE_PARTICIPANT_TRACKING.md` - Tracking feature
- `FEATURE_NO_RESUBMIT.md` - Lock feature
- `HOW_TO_TEST.md` - Testing guide
- `START_HERE.md` - Getting started
- `README.md` - Full documentation

**Setup:**
- `.env` - Your database configuration
- `requirements.txt` - Python dependencies
- `setup_database.bat` - Database setup script

---

## ⚡ Quick Commands

```bash
# Run application
python -m streamlit run app.py

# Set up database
setup_database.bat

# Check dependencies
python -c "import streamlit, pandas, plotly, psycopg, dotenv"

# Test database connection
python -c "import database; print('Database OK')"
```

---

## 📈 Feature Matrix

| Feature | Presenter | Participant |
|---------|-----------|-------------|
| Create quizzes | ✅ | ❌ |
| Launch sessions | ✅ | ❌ |
| Join sessions | ❌ | ✅ |
| Answer questions | ❌ | ✅ |
| Change answers | ❌ | ❌ (locked) |
| View all results | ✅ | ❌ |
| See participant names | ✅ | ❌ |
| See own correctness | ❌ | ✅ |

---

## 💾 Database Tables

1. **users** - User accounts
2. **quizzes** - Quiz metadata
3. **questions** - Quiz questions
4. **sessions** - Active quiz sessions
5. **responses** - Participant answers (immutable)

---

## 🎯 Key Points

✅ **Two new features** added
✅ **Zero breaking changes** - all old features work
✅ **Enhanced security** - dual-layer protection
✅ **Better insights** - see individual responses
✅ **Professional quality** - ready for demo

---

**Last Updated:** 2026-01-02
**Status:** Production Ready ✅
