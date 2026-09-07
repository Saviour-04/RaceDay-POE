markdown
# RaceDay Event Management System - Part 1


👤 Student Information

Module	Programming 2B
Module Code	PROG6212
Assessment	Portfolio of Evidence (POE) - Part 1
Year	2026
Student Name	[Saviour mkhatshwa]
Student Number	[ST10489983]
GitHub Link: https:https://github.com/Saviour-04/RaceDay-POE/edit/main/README.md


## 📋 Project Overview

RaceDay is a full-stack web-based event management system designed specifically for the South African road running, walking, and cycling community. This platform will allow Event Organisers to create and manage events, categories, and participant results, while Participants can browse upcoming events, enter events, track their personal performance history, and prepare for race day.

**Part 1** focuses on system planning and database design before any code is written.

---

## 👥 User Roles

### Organiser
- Create, edit, and delete events
- Manage event categories (age groups/distance groups)
- Capture participant results (finish times and positions)
- View all event enrolments
- Manage event banner images

### Participant
- Create an account and manage profile
- Browse upcoming events with filtering options
- Enter events by selecting a category
- View personal enrolment history
- Track personal race results and performance

---

## 🗂️ Documentation Structure

All planning documents are stored in the `/docs` folder:
RaceDay-POE/
├── README.md
├── .github/
│ └── workflows/
│ └── validate-docs.yml
└── docs/
├── ERD.png # Entity Relationship Diagram
├── API_Endpoint_Plan.md # Complete API endpoint specifications
└── RaceDay_Database.sql # SQL Server database creation script

text

---

## 📊 Entity Relationship Diagram (ERD)

The ERD represents the full database structure for the RaceDay system with **5 core entities**:

| Entity | Description |
|--------|-------------|
| **User** | Stores user authentication and profile information (Organisers and Participants) |
| **Event** | Stores event details (name, date, location, distance, type) |
| **Category** | Stores event categories (age groups or distance groups) |
| **Enrolment** | Links Participants to Events with selected Categories |
| **Result** | Stores finish times and positions for Participants |

### Entity Relationships
User (1) ──────┬── (∞) Event (as Organiser)
└── (∞) Enrolment (as Participant)

Event (1) ─────┬── (∞) Category
└── (∞) Enrolment

Category (1) ────── (∞) Enrolment

Enrolment (1) ────── (1) Result

text

**View the complete ERD**: [`/docs/ERD.png`](/docs/ERD.png)

---

## 🔗 API Endpoint Plan

The API endpoint plan defines all RESTful endpoints that will be implemented in Part 2.

### Endpoint Categories

| Category | Methods | Description |
|----------|---------|-------------|
| **Authentication** | POST, GET | Register, login, logout, get current user |
| **User Profile** | GET, PUT | View and update user profiles |
| **Events** | GET, POST, PUT, DELETE | Full CRUD operations for events |
| **Categories** | GET, POST, PUT, DELETE | Manage event categories |
| **Enrolments** | GET, POST, PUT, DELETE | Manage participant enrolments |
| **Results** | GET, POST, PUT, DELETE | Manage race results |

### Key Endpoints

| Method | Route | Role | Description |
|--------|-------|------|-------------|
| POST | `/api/auth/register` | Public | Register new user |
| POST | `/api/auth/login` | Public | User login |
| GET | `/api/events` | Public | Get all events |
| POST | `/api/events` | Organiser | Create new event |
| POST | `/api/enrolments` | Participant | Enrol in event |
| POST | `/api/results` | Organiser | Capture race results |

**View the complete API Plan**: [`/docs/API_Endpoint_Plan.md`](/docs/API_Endpoint_Plan.md)

---

## 🗄️ Database Schema

The database is built using **SQL Server Management Studio (SSMS)** with the following schema:

### Tables

| Table | Columns | Primary Key | Foreign Keys |
|-------|---------|-------------|--------------|
| **User** | UserID, Email, PasswordHash, FirstName, LastName, PhoneNumber, DateOfBirth, Role, ProfilePictureUrl, CreatedAt, IsActive | UserID | - |
| **Event** | EventID, OrganiserID, Name, Description, EventDate, Location, Distance, EventType, BannerImageUrl, MaxParticipants, CreatedAt, IsActive | EventID | OrganiserID → User.UserID |
| **Category** | CategoryID, EventID, Name, Description, MinAge, MaxAge, MinDistance, MaxDistance, EntryFee | CategoryID | EventID → Event.EventID |
| **Enrolment** | EnrolmentID, ParticipantID, EventID, CategoryID, EnrolmentDate, Status, BibNumber | EnrolmentID | ParticipantID → User.UserID, EventID → Event.EventID, CategoryID → Category.CategoryID |
| **Result** | ResultID, EnrolmentID, FinishTime, FinishPosition, OverallPosition, IsPublished, Notes | ResultID | EnrolmentID → Enrolment.EnrolmentID |

### Seed Data

The database includes realistic sample data:

- **2 Organisers**: John Organiser, Sarah Events
- **2 Participants**: Mike Runner, Lisa Cyclist
- **3 Events**: Comrades Marathon, Cape Town Cycle Tour, Soweto Marathon
- **8 Categories**: Various age and distance groups for each event
- **4 Enrolments**: Participants enrolled in different events
- **2 Results**: Completed results for confirmed enrolments

### Database Setup

1. Open **SQL Server Management Studio (SSMS)**
2. Connect to your SQL Server instance
3. Open the script: [`/docs/RaceDay_Database.sql`](/docs/RaceDay_Database.sql)
4. Execute the script (F5)
5. Verify database creation:

```sql
-- Check all tables have data
SELECT 'User' AS TableName, COUNT(*) AS RowCount FROM [User]
UNION ALL
SELECT 'Event', COUNT(*) FROM [Event]
UNION ALL
SELECT 'Category', COUNT(*) FROM [Category]
UNION ALL
SELECT 'Enrolment', COUNT(*) FROM [Enrolment]
UNION ALL
SELECT 'Result', COUNT(*) FROM [Result];
Expected Output:

TableName	RowCount
User	4
Event	3
Category	8
Enrolment	4
Result	2
🚀 CI/CD Pipeline
GitHub Actions Workflow
The repository includes a CI/CD workflow that validates the documentation structure on every push:

yaml
name: Validate Documentation

on:
  push:
    branches: [ main, master ]
  pull_request:
    branches: [ main, master ]

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Validate Docs Folder
      run: |
        # Checks for required files in /docs folder
        # ERD.png, API_Endpoint_Plan.md, RaceDay_Database.sql
Build Status
https://github.com/YOUR-USERNAME/RaceDay-POE/actions/workflows/validate-docs.yml/badge.svg

CI/CD Success Screenshot
https://CI-CD_Success.png

📹 Video Presentation
Watch the Part 1 walkthrough explaining the planning documents:

VIDE LINK https://youtu.be/8vEJP-hL4hA

Video covers:

✅ ERD design decisions and entity relationships

✅ API endpoint planning and choices

✅ SQL script demonstration (run live in SSMS)

✅ Database verification and seed data explanation

🛠️ Technologies Used
Part 1 Technologies:
SQL Server Management Studio (SSMS): Database creation and management

Microsoft Word: ERD creation and documentation

Markdown: Documentation formatting

Git & GitHub: Version control and collaboration

GitHub Actions: CI/CD for document validation

Future Parts:
Part 2: ASP.NET Core Web API, Entity Framework Core, xUnit

Part 3: ASP.NET Core MVC, Azure Blob Storage, Docker

📝 Commit History
This repository follows a structured commit strategy with 20+ meaningful commits:

Commit Categories
Category	Examples
Setup	Initial commit, Added docs folder, Configured CI/CD
ERD	Added ERD diagram, Updated entity relationships
API Plan	Added endpoint plan, Completed all endpoints, Added role requirements
Database	Added SQL script, Created User table, Added Event table, Added Categories, Added Enrolments, Added Results, Added seed data, Added indexes
Documentation	Updated README, Added CI/CD screenshot, Added video link
Validation	Added workflow file, Fixed CI/CD issues
📁 Project Structure
text
RaceDay-POE/
├── README.md                          # This file
├── CI-CD_Success.png                  # CI/CD build screenshot
│
├── .github/
│   └── workflows/
│       └── validate-docs.yml          # CI/CD workflow
│
└── docs/
    ├── ERD.png                        # Entity Relationship Diagram
    ├── API_Endpoint_Plan.md           # Complete API endpoint specifications
    └── RaceDay_Database.sql           # SQL Server database script


✅ Part 1 Checklist
☑ ERD created with 5+ entities
☑ All relationships and cardinalities defined
☑ Primary and foreign keys identified
☑ API endpoint plan complete (all 6 columns filled)
☑ All required endpoints planned
☑ Role-based access specified
☑ SQL script creates all tables
☑ Foreign keys and constraints defined
☑ Realistic seed data inserted
☑ Script runs without errors
☑ GitHub repository created
☑ 20+ meaningful commits made
☑ CI/CD workflow configured
☑ Green build achieved
☑ README complete with all sections
☑ YouTube video submitted
🔗 Useful Links
GitHub Repository: https://github.com/YOUR-USERNAME/RaceDay-POE

Video Presentation: https://youtu.be/YOUR-VIDEO-ID

GitHub Actions: https://github.com/YOUR-USERNAME/RaceDay-POE/actions

📚 References
The IIE Assessment Strategy and Policy (IIE009)

The IIE Intellectual Integrity and Property Rights Policy (IIE023)

SQL Server Documentation: https://docs.microsoft.com/en-us/sql/

GitHub Actions Documentation: https://docs.github.com/en/actions







---






