# Final Project: Collaborative innovation

## Objective
The final project is the culmination of our journey in IS4010. It is your opportunity to work in a small team to design, build, and present an ambitious application that you are genuinely passionate about. The goal is to move beyond a simple assignment and create something cool, useful, and impressive. This project is designed to simulate a real-world development environment, where collaboration, communication, and creative problem-solving are just as important as the code itself.

## The core idea: collaborative creation
You will form small teams to build a single, cohesive application that showcases your collective skills in python, rust, and AI-augmented development. This is your chance to tackle a bigger problem, build a more feature-rich application, and create a standout portfolio piece that demonstrates your ability to work effectively as part of a technical team.

---

## Group formation and roles

### Group size
* Groups will consist of **2-3 students**. This size is large enough to allow for significant work but small enough to ensure everyone contributes meaningfully.

### Team responsibilities
While there are no formally assigned roles, successful teams often have members who naturally specialize. We encourage you to think about how your team will handle:
* **Project management:** Who will keep track of tasks, deadlines, and ensure the team is communicating effectively?
* **Architecture & design:** Who will take the lead on the high-level design and how the different parts of the application will fit together?
* **Python development:** Who will focus on the python-specific components of the project?
* **Rust development:** Who will focus on the rust-specific components?
* **Testing & QA:** Who will be responsible for writing tests and ensuring the final application is robust and bug-free?

---

## Technical and project requirements

Your group project must adhere to the core technical principles of the course.

### Core requirements
1.  **Meaningful scope:** The project should be more ambitious than something an individual could complete alone.
2.  **Flexible architecture:** The application must be built using **Python or Rust**. Your team has the flexibility to choose the language you feel is best suited for your project.
3.  **AI partnership:** Your team must actively use ai assistants (github copilot, gemini, etc.) for development and document this partnership.
4.  **Version control:** The project must be developed in a shared github repository, with all members contributing commits.

### Project proposal (due end of week 11)
Your team will submit a single `PROPOSAL.md` file in your shared github repository, outlining:
* Your project concept and the problem it solves.
* A list of the core features you plan to build.
* A clear description of the technical architecture, including your **choice of primary language (Python or Rust)** and a brief justification for that choice.
* A breakdown of initial tasks and which team member is responsible for each.

---

## Milestones and deliverables

The project milestones are designed to keep your team on track.

* **Week 9:** Final project is announced and group formation begins.
* **Week 10:** Group formation is finalized.
* **Week 11:** Project proposals due.
* **Week 13 (MVP Check-in):** Your team will present a live, 5-minute demo of a core, working feature of your application.
* **Exam Week (Demo Day):** Your team will give a final 5-7 minute presentation of the completed project to the class.

## Individual accountability and peer evaluation
To ensure that every member contributes fairly, a peer evaluation will be a required part of the final submission. Each student will privately submit a short form evaluating the contributions of their teammates. This evaluation will be a factor in each individual's final project grade.

This collaborative final project is your chance to build something truly memorable. Let's make something awesome.

---

### Example final project ideas
This list is meant to serve as a starting point and inspiration. You are encouraged to be creative and propose your own unique project ideas. The best project is one that your team is genuinely excited to build.

### Python project ideas
Python is an excellent choice for projects involving web data, APIs, and rapid development.

* **GitHub profile analyzer**
    * **Concept:** A command-line tool that takes a GitHub username, fetches data from the public GitHub API, and displays interesting statistics like their most-used languages, most popular repositories, and contribution patterns.
    * **Key skills involved:** Consuming web APIs (`requests`), parsing JSON data, data processing and aggregation, and presenting formatted text to the user.

* **Personal finance CLI tracker**
    * **Concept:** An interactive command-line application where a user can log income and expenses. The data is saved to a local JSON or CSV file, and the user can ask for reports, like "show spending for this month by category."
    * **Key skills involved:** File I/O (JSON or CSV), object-oriented programming (e.g., a `Transaction` class), handling user input, and data processing.

* **Text-based adventure game engine**
    * **Concept:** Build a reusable engine for text-based adventure games. The engine would load game data (rooms, items, descriptions, connections) from a set of JSON files.
    * **Key skills involved:** Heavy use of object-oriented programming (classes for `Player`, `Room`, `Item`), file I/O, and managing complex application state in loops.

### Rust project ideas
Rust is a great fit for performance-critical applications, command-line tools, and systems that require high reliability.

* **Markdown link checker**
    * **Concept:** A command-line tool that scans a given markdown file, finds all the web links within it, and concurrently makes HTTP requests to check if any of the links are broken (e.g., return a 404 Not Found error).
    * **Key skills involved:** File I/O, string parsing, using external crates (e.g., `reqwest` for HTTP requests and `tokio` for async operations), and CLI argument parsing.

* **Simple key-value store**
    * **Concept:** A program that acts like a simple database stored in a single file. It would take commands from the user like `set <key> <value>`, `get <key>`, and `delete <key>`, persisting the changes to disk.
    * **Key skills involved:** Advanced file I/O, using data structures like `HashMap`, error handling with `Result`, and command parsing.

* **"Game of Life" terminal simulation**
    * **Concept:** An implementation of Conway's Game of Life that runs directly in the terminal. The program would calculate each new "generation" of the cellular automaton and print the grid to the console, creating an animation.
    * **Key skills involved:** Managing state in a 2D data structure (e.g., a vector of vectors), implementing game logic, and controlling the terminal output.