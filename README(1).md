# Waypoint
### A campus guide built around the people who know it best.

Waypoint is a campus information and student knowledge management system designed to make everyday campus life easier. It brings useful location details, student advice, common questions, and campus issue reports into one place, so students and faculty spend less time searching for information and more time getting things done.

> **The idea is simple:** help people find where they need to go, learn what they need to know, and report what needs attention.

---

## Why Waypoint?

A campus can be confusing, especially for new students. Finding a classroom, locating a lab, learning where a facility is, or figuring out whom to ask can take more time than it should. Useful information is often scattered across messages, notice boards, and conversations.

Waypoint gives that information a shared home. It combines a searchable campus directory with practical knowledge contributed by the campus community.

## What can you do with it?

### Find your way around
Browse campus buildings, classrooms, labs, and facilities. Search for a place, check its details, and use QR codes planned for individual locations to open the relevant information page.

### Learn from other students
Students can share tips and practical advice about campus life. Tips are reviewed before appearing publicly, helping keep the information useful and appropriate.

### Report campus issues
Report a problem and link it to the location where it happened. Reports can move through clear statuses:

`OPEN` → `ACKNOWLEDGED` → `IN_PROGRESS` → `RESOLVED`

This gives students a clearer way to follow an issue instead of wondering whether anyone has seen it.

### Get answers in one place
The CampusWiki is planned as a moderated FAQ and knowledge base. Students can submit questions and answers under categories, while administrators review entries before they become visible to everyone.

### Give administrators the tools to manage information
The admin area is intended to support location management, review of student-submitted tips and FAQ entries, and updates to issue statuses. Access to administrative actions should be restricted by role.

---

## How Waypoint helps students

- **Less time searching:** Find campus locations and useful information from one place.
- **A smoother start:** Help new students get familiar with buildings, facilities, and common campus questions.
- **Practical, shared knowledge:** Learn from tips and answers contributed by people who know the campus.
- **A clearer reporting process:** Submit a location-linked issue and check its progress where that feature is available.
- **A stronger campus community:** Share information that can help the next student.

## How Waypoint helps faculty and campus administrators

- **One directory to maintain:** Keep building, room, lab, and facility details organized.
- **A clearer view of reported issues:** Review reports and update their status as work progresses.
- **Useful knowledge in one place:** Approve helpful tips and FAQ entries so reliable information is easier to find.
- **Less repeated answering:** Common questions can be documented and reused instead of answered from scratch each time.
- **Role-based responsibilities:** Separate student actions from administrator tasks.

Waypoint is intended to support communication and organization, not replace official campus policies or emergency reporting procedures.

---

## How it works

At a high level, Waypoint has three parts:

1. **The web interface**  
   HTML, CSS, and JavaScript provide the pages students and administrators use.

2. **The Java backend**  
   A Java application using Javalin handles API requests, application logic, and access checks.

3. **The MySQL database**  
   MySQL is intended to store users, campus locations, tips, issue reports, and FAQ entries. Java connects to the database through JDBC.

The web interface sends requests to the backend. The backend validates the request, performs permitted database operations, and returns a response to the interface.

### Planned information flow

```text
Student or Faculty Member
          |
          v
   Waypoint Web Page
   HTML / CSS / JavaScript
          |
          v
     Javalin API
   Java application logic
          |
          v
    JDBC connection
          |
          v
     MySQL database
```

For example, a student could open the directory, search for a laboratory, view its details, and later report an issue associated with that location. An administrator could review the report and update its status.

---

## Project status

Waypoint is being developed as a college end-semester project, with a focus on a working local MVP.

**Confirmed so far**
- Java and Javalin start successfully on port `7070`.
- The health endpoint at `/api/health` returns JSON.
- The MySQL database named `waypoint` has been created.
- Maven is configured to build and run the Java application.

**Still to be implemented or verified**
- Database tables and JDBC connectivity.
- User registration, login, and role-based access.
- Campus directory and its CRUD operations.
- Student tips and administrator moderation.
- Campus issue reporting and status updates.
- CampusWiki/FAQ and moderation.
- Admin dashboard.
- QR code generation.
- Full frontend functionality.

Features described above are the intended project scope. They should not be treated as finished until they are implemented and tested.

---

## Technology

| Part | Technology |
|---|---|
| Frontend | HTML, CSS, JavaScript |
| Backend | Java, Javalin |
| Database | MySQL |
| Database access | JDBC, MySQL Connector/J |
| Build tool | Maven |
| JSON responses | Jackson Databind |
| QR codes | ZXing planned |

---

## Run it locally

### Requirements
- JDK compatible with the Maven configuration
- Maven
- MySQL Server
- MySQL Workbench or another MySQL client

### 1. Open the project
Open the `Waypoint` folder in VS Code.

### 2. Check the database
In MySQL Workbench, run:

```sql
CREATE DATABASE IF NOT EXISTS waypoint;
USE waypoint;
SHOW TABLES;
```

The database exists, but confirm whether the required tables have been created before running database-backed features.

### 3. Start the application
Open a terminal at the project root and run:

```powershell
mvn clean compile exec:java
```

### 4. Check the health endpoint
Open:

`http://localhost:7070/api/health`

Expected response:

```json
{
  "status": "running",
  "project": "Waypoint"
}
```

The property order may differ. The homepage at `http://localhost:7070` depends on `src/main/resources/public/index.html` being present and saved.

---

## Project structure

```text
Waypoint/
├── pom.xml
├── database/
└── src/
    └── main/
        ├── java/
        │   └── com/
        │       └── waypoint/
        │           └── Main.java
        └── resources/
            └── public/
                ├── index.html
                ├── styles.css      # planned
                └── app.js          # planned
```

Some files shown here are planned and may not exist yet. The current confirmed backend entry point is `Main.java`.

---

## Development principles

Waypoint is being built around a few practical rules:

- **Useful before complicated:** get the main workflows working before adding optional features.
- **Privacy and access control:** protect account information and enforce administrator permissions on the server.
- **Safe database access:** use prepared SQL statements and avoid storing plain-text passwords.
- **Reviewed community content:** keep tips and FAQ entries pending review until approved.
- **Clear status updates:** use defined issue statuses so reports have an understandable lifecycle.
- **Honest project status:** document what works and test each feature before calling it complete.

---

## What's next?

The next development milestone is to verify the database tables, connect Java to MySQL, and add a database health check. After that, the recommended order is:

1. Campus directory and location CRUD.
2. Registration, login, and role-based permissions.
3. Issue reporting and status tracking.
4. Student tips and moderation.
5. CampusWiki/FAQ and moderation.
6. Admin dashboard.
7. QR codes and final testing.

---

## The goal

A better campus experience does not always require a complicated system. Sometimes it starts with knowing where to go, finding a reliable answer, and having a clear way to report a problem.

**Waypoint aims to make those everyday campus tasks easier for students, faculty, and administrators.**
