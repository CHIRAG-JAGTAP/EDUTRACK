# EduTrack — Smart Student Portal

EduTrack is a comprehensive web-based student productivity portal designed to centralize every aspect of academic life into a single, unified dashboard. Built with Django on the backend and powered by a clean, responsive frontend, EduTrack addresses a problem every student faces — the constant need to juggle multiple tools, spreadsheets, and apps just to stay on top of their academic responsibilities. From tracking attendance subject-by-subject to predicting CGPA based on current marks, from managing daily tasks with priority levels to maintaining a streak of consistent daily engagement, EduTrack brings all of it together in one place. The portal supports image-based timetable scanning using OCR technology, so students can simply photograph their printed timetable and have subjects and events automatically imported into the system. A built-in practice log lets students document what they studied or coded each day, while a soft skills self-assessment module encourages reflection beyond academics. Every feature is backed by a session-authenticated REST API, with all data stored securely per user. EduTrack was built with the goal of reducing friction for students — so that keeping track of academics takes less time, and actually doing the work takes more.

---

## Features

| Section | Description |
|---|---|
| Home | A summary screen showing today's tasks, attendance average, streak count, and CGPA |
| Task Planner | Add tasks with High, Medium, or Low priority and due dates. Mark them complete when done |
| Practice Log | Write notes about what you studied or coded, organized by category |
| Attendance Tracker | Enter classes held and attended per subject and see your live percentage with warnings |
| CGPA Predictor | Enter marks and credit hours per subject to instantly calculate your predicted CGPA |
| Timetable and Calendar | Upload a photo of your timetable or calendar; the app reads it using OCR and imports subjects and events automatically |
| Streaks and Badges | Log in every day to maintain your streak and earn badges at milestones |
| Soft Skills | Rate yourself on Communication, Teamwork, Time Management, and Problem Solving |
| Analytics | Charts and graphs that visualize attendance, task completion, and skill progress |
| Feedback | Submit feedback with a star rating, mood tag, and category |
| Settings | Update your profile, change your password, or clear all your data |

---

## Built With

- **Python / Django 5** — backend framework
- **SQLite** — database
- **Vanilla JavaScript** — frontend logic
- **CSS Custom Properties** — theming and layout
- **OCR.space API** — image-to-text reading for timetable uploads
- **Font Awesome 6** — icons

---

## Project Structure

```
edutrack_project/
│
├── edutrack/
│   ├── models.py
│   ├── views.py
│   ├── urls.py
│   └── migrations/
│
├── edutrack_project/
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
│
├── static/
│   ├── css/
│   │   ├── dashboard.css
│   │   └── style.css
│   └── js/
│       ├── dashboard.js
│       ├── login.js
│       └── script.js
│
├── templates/
│   └── edutrack/
│       ├── dashboard.html
│       ├── login.html
│       ├── index.html
│       ├── home.html
│       ├── about.html
│       └── contact.html
│
├── manage.py
├── requirements.txt
└── db.sqlite3
```

---

## Installation and Setup

### Option 1 — Terminal (Command Line)

**Step 1 — Verify Python is installed**

Open a terminal and run:
```bash
python --version
```
Python 3.10 or higher is required. Download from [python.org](https://python.org) if needed.

**Step 2 — Extract the project**

Unzip the project archive and open a terminal inside the `edutrack_project` folder.

**Step 3 — Create a virtual environment**
```bash
python -m venv venv
```

**Step 4 — Activate the virtual environment**

On Windows:
```bash
venv\Scripts\activate
```
On Mac or Linux:
```bash
source venv/bin/activate
```
Once active, `(venv)` will appear at the start of your terminal prompt.

**Step 5 — Install required packages**
```bash
pip install -r requirements.txt
```

**Step 6 — Set up the database**
```bash
python manage.py migrate
```
This creates the `db.sqlite3` file with all required tables.

**Step 7 — Start the server**
```bash
python manage.py runserver
```

**Step 8 — Open in your browser**

Navigate to [http://127.0.0.1:8000](http://127.0.0.1:8000)

---

### Option 2 — PyCharm IDE

**Step 1 — Open the project**

- Launch PyCharm
- Click **File → Open**
- Select the `edutrack_project` folder and click **OK**
- Click **Trust Project** if prompted

**Step 2 — Create a virtual environment**

- Go to **File → Settings** (Windows / Linux) or **PyCharm → Preferences** (Mac)
- Navigate to **Project: edutrack_project → Python Interpreter**
- Click the gear icon and select **Add Interpreter → Add Local Interpreter**
- Choose **Virtualenv Environment → New** and click **OK**

PyCharm will create and configure the environment automatically.

**Step 3 — Install dependencies**

Open the built-in terminal (**View → Tool Windows → Terminal**) and run:
```bash
pip install -r requirements.txt
```

**Step 4 — Configure the run profile**

- Click **Run → Edit Configurations**
- Click the **+** button and select **Python**
- Set the following:
  - **Name:** EduTrack
  - **Script path:** point to `manage.py` in the project folder
  - **Parameters:** `runserver`
  - **Python interpreter:** select the virtual environment you created
- Click **OK**

**Step 5 — Run database migrations**

In the PyCharm terminal:
```bash
python manage.py migrate
```

**Step 6 — Start the server**

Click the green **Run** button or press `Shift + F10`.

The terminal will show:
```
Starting development server at http://127.0.0.1:8000/
```

**Step 7 — Open in your browser**

Navigate to [http://127.0.0.1:8000](http://127.0.0.1:8000)

---

## API Reference

All endpoints are prefixed with `/api/`. Protected endpoints return `401 Unauthorized` if no valid session is present.

### Authentication

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/signup/` | Register a new account |
| `POST` | `/api/login/` | Login with email or phone number and password |
| `POST` | `/api/logout/` | End the current session |
| `GET` | `/api/me/` | Retrieve the logged-in user's profile |
| `POST` | `/api/profile/` | Update profile details |
| `POST` | `/api/change-password/` | Change the account password |

### Feature Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `GET / POST` | `/api/attendance/` | Retrieve or save attendance records |
| `GET / POST` | `/api/tasks/` | List all tasks or create a new one |
| `PATCH / DELETE` | `/api/tasks/<id>/` | Edit or delete a specific task |
| `GET / POST` | `/api/notes/` | List or create practice log entries |
| `DELETE` | `/api/notes/<id>/` | Delete a specific practice log entry |
| `GET / POST` | `/api/marks/` | Retrieve or save subject marks |
| `GET / POST` | `/api/skills/` | Retrieve or update soft skill ratings |
| `GET / POST` | `/api/streaks/` | Retrieve or update streak data |
| `GET / POST` | `/api/feedback/` | List or submit feedback |
| `POST` | `/api/clear-data/` | Delete all user data and end the session |

---

## Database Schema

| Table | Description |
|---|---|
| `edutrack_users` | Stores account details including name, email, phone, hashed password, course, and college |
| `edutrack_attendance` | Records classes held and attended per subject for each user |
| `edutrack_marks` | Stores subject name, maximum marks, obtained marks, and credit hours |
| `edutrack_tasks` | Stores task title, priority level, due date, and completion status |
| `edutrack_practice_logs` | Stores study and coding session notes with title, category, and content |
| `edutrack_soft_skills` | One self-rating record per user covering four skill areas |
| `edutrack_streaks` | Tracks current streak, best streak, all logged dates, and earned badges |
| `edutrack_feedback` | Stores star rating, mood, category, subject reference, and message text |

---

## Timetable OCR

The timetable and calendar upload feature uses the [OCR.space](https://ocr.space/) API to extract text from images entirely on the client side. When a student uploads a photo of their timetable, the image is sent to the OCR API, and the returned text is parsed in the browser to identify subject names and dated events. Detected subjects are automatically added to the Attendance and Marks tables, and dated events are created as Tasks in the planner.

The API key is defined in `static/js/dashboard.js`. If you reach the free tier rate limit, obtain a new key from [ocr.space/OCRAPI](https://ocr.space/OCRAPI) and replace it there.


## Team

| Name | Role |
|---|---|
| **Chirag Jagtap** | Developer |
| **Ayush Pandey** | Developer |
| **Chinmay Bhalerao** | Developer |

---

*EduTrack — Built to make academic life more organized, one dashboard at a time.*
