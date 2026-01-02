# How to Test the Participant Tracking Feature

## Quick Test Guide (5 minutes)

### Step 1: Start the Application

```bash
python -m streamlit run app.py
```

The app will open at `http://localhost:8501`

### Step 2: Create a Quiz as Presenter

1. Click **"Login as Presenter"**
2. Enter name: `Teacher`
3. Sidebar → **"Create Quiz"**
4. Title: `Test Quiz`
5. Click **"Create Quiz"**

### Step 3: Add Sample Questions

**Question 1:**
- Question: `What is 2+2?`
- A: `3`
- B: `4`
- C: `5`
- D: `6`
- Correct: `B`
- Click **"Add Question"**

**Question 2:**
- Question: `What color is the sky?`
- A: `Red`
- B: `Blue`
- C: `Green`
- D: `Yellow`
- Correct: `B`
- Click **"Add Question"**

Click **"Done Adding Questions"**

### Step 4: Launch Session

1. Sidebar → **"Launch Session"**
2. Select your quiz
3. Click **"Launch Session"**
4. **Copy the session code** (e.g., `ABC123`)

### Step 5: Simulate Multiple Participants

Open 4 different browser windows (or use incognito mode):

**Window 1 (Participant 1):**
- Go to `http://localhost:8501`
- Click "Login as Participant"
- Name: `Alice`
- Enter session code
- Question 1: Choose **B** (correct)
- Question 2: Choose **B** (correct)
- Submit both

**Window 2 (Participant 2):**
- Go to `http://localhost:8501` (new incognito)
- Click "Login as Participant"
- Name: `Bob`
- Enter session code
- Question 1: Choose **B** (correct)
- Question 2: Choose **A** (incorrect)
- Submit both

**Window 3 (Participant 3):**
- Go to `http://localhost:8501` (new incognito)
- Click "Login as Participant"
- Name: `Carol`
- Enter session code
- Question 1: Choose **A** (incorrect)
- Question 2: Choose **B** (correct)
- Submit both

**Window 4 (Participant 4):**
- Go to `http://localhost:8501` (new incognito)
- Click "Login as Participant"
- Name: `Dave`
- Enter session code
- Question 1: Choose **D** (incorrect)
- Question 2: Choose **C** (incorrect)
- Submit both

### Step 6: View Results with Participant Names

1. **Go back to presenter window**
2. Sidebar → **"View Results"**
3. Select your session

### Expected Results

**Question 1: What is 2+2?**

```
Options:
A) 3    B) 4 ✅    C) 5    D) 6

┌─────────────────────────┬─────────────────────────┐
│  Response Distribution  │  Participant Responses  │
├─────────────────────────┼─────────────────────────┤
│  [Bar Chart shows:      │  Answer A ❌ (1 person) │
│   A: 1                  │  • Carol                │
│   B: 2 (green)          │                         │
│   C: 0                  │  Answer B ✅ (2 people) │
│   D: 1]                 │  • Alice                │
│                         │  • Bob                  │
│  Accuracy: 50.0%        │                         │
│  2/4 correct            │  Answer D ❌ (1 person) │
│                         │  • Dave                 │
└─────────────────────────┴─────────────────────────┘
```

**Question 2: What color is the sky?**

```
Options:
A) Red    B) Blue ✅    C) Green    D) Yellow

┌─────────────────────────┬─────────────────────────┐
│  Response Distribution  │  Participant Responses  │
├─────────────────────────┼─────────────────────────┤
│  [Bar Chart shows:      │  Answer A ❌ (1 person) │
│   A: 1                  │  • Bob                  │
│   B: 2 (green)          │                         │
│   C: 1                  │  Answer B ✅ (2 people) │
│   D: 0]                 │  • Alice                │
│                         │  • Carol                │
│  Accuracy: 50.0%        │                         │
│  2/4 correct            │  Answer C ❌ (1 person) │
│                         │  • Dave                 │
└─────────────────────────┴─────────────────────────┘
```

## What to Look For

✅ **Participant names appear** in the right column
✅ **Grouped by answer choice** (A, B, C, D)
✅ **Correct answers** marked with ✅
✅ **Incorrect answers** marked with ❌
✅ **Participant count** shown for each answer
✅ **Bar chart still works** on the left
✅ **Accuracy percentage** displayed

## Troubleshooting

### "No participants have answered yet"
- Make sure you submitted answers as participants
- Verify you're viewing the correct session
- Check that participants joined the right session code

### Participant names don't show
- Refresh the page (F5)
- Make sure you're logged in as presenter
- Verify participants actually submitted their answers

### Database connection error
- Check that PostgreSQL is running
- Verify `.env` file has correct password
- Make sure database was created (`setup_database.bat`)

## Quick Browser Window Setup

For easy testing, use this approach:

1. **Main window**: Presenter (keep this open)
2. **Incognito window 1**: Alice
3. **Incognito window 2**: Bob
4. **Incognito window 3**: Carol
5. **Incognito window 4**: Dave

**Keyboard shortcuts:**
- Chrome/Edge: `Ctrl + Shift + N` (new incognito)
- Firefox: `Ctrl + Shift + P` (new private window)

## After Testing

You can now:
- Create more quizzes
- Test with real students
- Record your demo video showing this feature
- Export/screenshot results for documentation

---

**Feature Working?** ✅ You should now see participant names grouped by their answers!
