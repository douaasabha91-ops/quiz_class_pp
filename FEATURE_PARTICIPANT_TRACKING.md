# Feature: Participant Response Tracking

## Overview

The presenter can now see **which participant chose each answer** in the results view. This provides detailed insights into individual student performance.

## What Changed

### Enhanced Results Display

The results page now shows:

1. **Left Column (60%)**: Bar chart showing response distribution
2. **Right Column (40%)**: List of participants grouped by their answers

### Visual Layout

```
Question 1: What is 2+2?

Options:
A) 3          B) 4 ✅       C) 5          D) 6

┌─────────────────────────────┬──────────────────────────┐
│     Response Distribution   │  Participant Responses   │
│                             │                          │
│  [Bar Chart showing:        │  Answer A ❌ (1 person)  │
│   A: 1 response             │  • John Smith            │
│   B: 3 responses ✅         │                          │
│   C: 0 responses            │  Answer B ✅ (3 people)  │
│   D: 1 response]            │  • Sarah Johnson         │
│                             │  • Mike Davis            │
│  Accuracy: 60.0%            │  • Emily Brown           │
│  3/5 correct                │                          │
│                             │  Answer D ❌ (1 person)  │
│                             │  • Tom Wilson            │
└─────────────────────────────┴──────────────────────────┘
```

## Database Changes

### New Function Added

**File:** `database.py`

```python
def get_question_responses_detailed(question_id, session_id):
    """Get detailed responses for a specific question showing participant names."""
    # Returns: answer, participant_name, is_correct, submitted_at
```

This function retrieves individual participant responses with their names, allowing the presenter to see exactly who chose which answer.

## UI Features

### Participant List

- **Grouped by Answer Choice**: Participants are organized under A, B, C, or D
- **Correct/Incorrect Indicators**: ✅ for correct answers, ❌ for incorrect
- **Participant Count**: Shows how many chose each option
- **Participant Names**: Listed with bullet points for easy reading

### Benefits

1. **Individual Accountability**: See exactly who answered what
2. **Identify Struggling Students**: Quickly spot participants who chose incorrect answers
3. **Recognize High Performers**: See who got the correct answer
4. **Follow-up Support**: Know which students need help on specific topics

## Usage Example

### Presenter View:

1. Navigate to **"View Results"** in the sidebar
2. Select a session
3. For each question, you'll see:
   - The question and all options (with ✅ marking the correct answer)
   - A bar chart showing distribution
   - A detailed list of participants grouped by their answer choice

### Example Output:

```
Question 2: What does HTML stand for?

Options:
A) Hyper Text Markup Language ✅
B) High Tech Modern Language
C) Home Tool Markup Language
D) Hyperlinks and Text Markup Language

Participant Responses:

Answer A ✅ (4 participants)
• Alice Williams
• Bob Thompson
• Carol Martinez
• David Lee

Answer B ❌ (1 participant)
• Eric Rodriguez

Answer D ❌ (2 participants)
• Frank Garcia
• Grace Chen
```

## Privacy Considerations

- Participant names are only visible to presenters
- Participants cannot see other participants' answers
- Results are only accessible during active sessions or to the quiz creator

## Technical Implementation

### Files Modified:

1. **`database.py`**: Added `get_question_responses_detailed()` function
2. **`app.py`**: Updated `display_session_results()` function

### Key Changes:

- Split results display into two columns
- Added participant grouping logic
- Color-coded correct/incorrect answers
- Maintained existing chart functionality

## Testing

To test this feature:

1. **Create a quiz** with multiple questions
2. **Launch a session** and note the session code
3. **Open multiple browser windows** (or incognito windows)
4. **Login as different participants** in each window:
   - Window 1: "Student A"
   - Window 2: "Student B"
   - Window 3: "Student C"
5. **Join the session** using the same session code
6. **Have each participant answer** the questions (choose different answers)
7. **Go back to presenter view** and click "View Results"
8. **Verify** you can see each participant's name under their chosen answer

## Screenshot Guide

When creating your demo video, show:

1. Multiple participants answering the same question
2. The results view showing participant names grouped by answer
3. The visual distinction between correct (✅) and incorrect (❌) answers
4. The accuracy metric alongside the detailed participant list

## Future Enhancements

Possible additions:
- Export results to CSV with participant details
- Leaderboard showing top performers
- Individual participant report cards
- Time tracking (show response times)
- Filter by correct/incorrect answers only

---

**Feature Status**: ✅ Implemented and Ready to Use
