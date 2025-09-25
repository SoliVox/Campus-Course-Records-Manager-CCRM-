# Campus Course & Records Manager (CCRM)

> A Java-based academic management system for educational institutions

## 📖 Overview
CCRM is a **Java 17 Maven multi-module project** with three submodules:
- **ccrm-core** → domain classes, datastore, services
- **ccrm-io** → import/export JSON/CSV, backup
- **ccrm-app** → CLI launcher and menu

The system manages students, courses, and enrollments using an in-memory datastore with import/export to JSON/CSV.  
Includes **demo mode** (option `9` in menu) that runs scripted inputs automatically from `data/demo-input.txt`.

---

## 🚀 Getting Started

### Prerequisites

Before running this project, ensure you have the following installed:

- **Java Development Kit (JDK) 17 or higher**
  - Download from [Oracle](https://www.oracle.com/java/technologies/downloads/) or [OpenJDK](https://adoptium.net/)
  - Verify installation: `java -version` should show version 17+
- **Apache Maven 3.8 or higher**
  - Download from [Maven Official Site](https://maven.apache.org/download.cgi)
  - Verify installation: `mvn -version`
- **Git** (to clone the repository)
- A terminal/command prompt

### Installation & Setup

1. **Clone the repository**
   ```bash
   git clone <your-repository-url>
   cd Campus-Course-Records-Manager-main
   ```

2. **Build the project**
   ```bash
   mvn clean install
   ```
   This will:
   - Compile all Java source files
   - Run any tests
   - Package the modules into JAR files
   - Install dependencies

3. **Run the application**
   ```bash
   mvn -pl ccrm-app exec:java -Dexec.mainClass="edu.ccrm.cli.Launcher"
   ```
   
   **Alternative: Run directly with Java**
   ```bash
   java -cp "ccrm-app/target/ccrm-app-1.0-SNAPSHOT.jar;ccrm-core/target/ccrm-core-1.0-SNAPSHOT.jar;ccrm-io/target/ccrm-io-1.0-SNAPSHOT.jar" edu.ccrm.cli.Launcher
   ```
   
   *Note: On Unix/Linux/Mac, use `:` instead of `;` as the classpath separator*

### Quick Start - Demo Mode

Try the demo mode to see the application in action:

1. Start the application using one of the methods above
2. When you see the menu, choose option `9` for Demo Mode
3. The system will automatically run pre-configured scenarios from `data/demo-input.txt`

```
Menu: 1-Students 2-Courses 3-Enrollment 4-IO 9-Demo 0-Exit
Choice: 9
```

---

## 📂 Project Structure (detailed)
```
ccrm-parent/
├── pom.xml
├── ccrm-core/
│   ├── domain/       # Student, Course, Enrollment, etc.
│   ├── datastore/    # In-memory DB
│   ├── service/      # Interfaces + impl
│   ├── exception/    # Custom exceptions
│   ├── util/         # IdGenerator, Validators
│   └── config/       # AppConfig (Singleton)
├── ccrm-io/
│   ├── ImportExportService.java
│   ├── BackupService.java
│   └── AppDirs.java
├── ccrm-app/
│   ├── CliMenu.java
│   ├── DemoRunner.java
│   └── Launcher.java
├── data/
│   ├── students.json
│   ├── courses.json
│   └── demo-input.txt
├── test-data/
│   ├── students.csv
│   └── courses.csv
└── output/
```

---

## 🕰 Evolution of Java
- **1995**: Java 1.0 – Write once, run anywhere
- **1998**: Java 2 (J2SE, J2EE, J2ME introduced)
- **2004**: Java 5 (Generics, Annotations, Enums)
- **2011**: Java 7 (NIO.2, try-with-resources)
- **2014**: Java 8 (Streams, Lambdas, Optional, Date/Time API)
- **2017**: Java 9 (Modules)
- **2019–2025**: Java 11, 17, 21 LTS – modern APIs, Records, Sealed Classes

---

## ☕ Java ME vs SE vs EE
| Edition | Purpose | Example Use Cases |
|---------|---------|------------------|
| **ME (Micro Edition)** | Lightweight, resource-constrained devices | Embedded systems, feature phones |
| **SE (Standard Edition)** | Core Java libraries + APIs | Desktop apps, CLI apps (like CCRM) |
| **EE (Enterprise Edition)** | Adds web, enterprise APIs | Servlets, JSP, Jakarta EE, enterprise backends |

---

## 🔑 JDK, JRE, JVM Explained
- **JVM** (Java Virtual Machine): Executes compiled bytecode.
- **JRE** (Java Runtime Environment): JVM + standard libraries to *run* Java apps.
- **JDK** (Java Development Kit): JRE + compiler + dev tools to *build* apps.

---

## 🖥 Install on Windows
1. Download **JDK 17** from [Oracle](https://www.oracle.com/java/technologies/downloads/).
2. Install and set environment variables:
    - `JAVA_HOME=C:\Program Files\Java\jdk-17`
    - Add `%JAVA_HOME%\bin` to `PATH`
3. Verify:
   ```
   java -version
   javac -version
   ```
4. Install **Eclipse IDE** → Add Maven plugin if not preinstalled.
5. Import project: *File → Import → Existing Maven Project → select ccrm-parent/pom.xml*

(*📸 Insert your screenshots here*)

---

## 📑 Mapping Syllabus → Implementation
| Syllabus Topic | Where in Project |
|----------------|------------------|
| OOP (Encapsulation, Inheritance, Polymorphism) | `domain/Student.java`, `domain/Instructor.java`, `domain/Course.java` |
| Abstraction (interfaces) | `service/StudentService.java`, `CourseService.java` |
| Packages | `edu.ccrm.domain`, `edu.ccrm.service`, etc. |
| Exception Handling | `exception/DuplicateEnrollmentException.java` |
| Collections Framework | `DataStore` uses `ConcurrentHashMap`, `List`, `Set` |
| Generics | Service methods with generics (`List<Student>`) |
| I/O (File, NIO.2) | `ImportExportService`, `BackupService` |
| Threads/Concurrency | `ConcurrentHashMap` in `DataStore` |
| Date/Time API | `Enrollment.java` uses `LocalDate` |
| Assertions | `Person.java` constructor (`assert id > 0`) |

---

---

## 🎯 How to Use

The application provides an interactive menu system. Here's what each option does:

### Main Menu Options:
- **1** - Student Management (Add new students, list all students)
- **2** - Course Management (Add courses, list courses, search by instructor)
- **3** - Enrollment Management (Enroll students in courses)
- **4** - Import/Export (CSV import, JSON export, backup data)
- **9** - Demo Mode (Automated demonstration)
- **0** - Exit (Saves data automatically)

### Example Usage:

**Adding a Student:**
```
Choice: 1
1-Add 2-List
>> 1
RegNo: R2025001
Name: John Doe  
Email: john.doe@university.edu
```

**Adding a Course:**
```
Choice: 2
Action (add/list/search): add
Course code (e.g., CS-101): CS-201
Title: Data Structures
Credits: 4
Instructor: Dr. Smith
Dept: Computer Science
```

**Enrolling a Student:**
```
Choice: 3
StudentId: 1000
Course code (ex: CS-101): CS-201
```

## 🔧 Troubleshooting

### Common Issues:

1. **"Command not found: mvn"**
   - Maven is not installed or not in your PATH
   - Install Maven and ensure it's added to your system PATH

2. **"No suitable JDK found"**
   - Ensure JDK 17+ is installed and JAVA_HOME is set correctly
   - Check: `echo $JAVA_HOME` (Unix/Linux/Mac) or `echo %JAVA_HOME%` (Windows)

3. **"Permission denied" errors**
   - On Unix/Linux/Mac: `chmod +x mvnw` (if using Maven wrapper)
   - Ensure you have write permissions in the project directory

4. **ClassNotFoundException**
   - Ensure all JAR files are in the classpath
   - Try rebuilding: `mvn clean install`

### System Requirements:
- **Memory**: At least 512 MB RAM available for the JVM
- **Disk Space**: ~50 MB for project and dependencies
- **OS**: Windows 10+, macOS 10.14+, or Linux (any modern distribution)

---

## 📊 Features in Detail

### Data Management
- **In-Memory Storage**: Fast operations with ConcurrentHashMap for thread safety
- **JSON Persistence**: Export/import student and course data
- **CSV Import**: Bulk load student data from spreadsheets
- **Automatic Backup**: Timestamped backups with configurable retention

### Business Logic
- **Credit Validation**: Prevents over-enrollment (18 credit limit per semester)
- **Duplicate Prevention**: No duplicate enrollments in the same course
- **Data Integrity**: Consistent student IDs and course codes across the system

### User Experience
- **Interactive CLI**: Intuitive menu-driven interface
- **Demo Mode**: Pre-configured scenarios for testing and demonstration
- **Error Handling**: Graceful handling of invalid inputs and edge cases
---
## 🖥 Screen Shots
# 1. java installation verification
![java-verification.png](https://raw.githubusercontent.com/tipubandlapalli/Campus-Course-Records-Manager/refs/heads/main/resources/java-verification.png)

# 2. project set up and run ( run the commands as described above)
![project-set-up.png](https://raw.githubusercontent.com/tipubandlapalli/Campus-Course-Records-Manager/refs/heads/main/resources/project-set-up.png)
```
mvn clean install
mvn -pl ccrm-app exec:java
```

# 3. demo menu
![menu.png](https://raw.githubusercontent.com/tipubandlapalli/Campus-Course-Records-Manager/refs/heads/main/resources/menu.png)

# 4. project folders structure
![project-folders-structure.png](https://raw.githubusercontent.com/tipubandlapalli/Campus-Course-Records-Manager/refs/heads/main/resources/project-folders-structure.png)
---
