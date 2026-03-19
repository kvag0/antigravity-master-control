🎯 PROJECT OVERVIEW

SYSTEM INSTRUCTION FOR SETUP AGENTS: > Read this document thoroughly. Use the "Technical Stack" and "Core Features" to populate the [PROJECT_OVERVIEW_PLACEHOLDER] and [PROJECT_OBJECTIVES_PLACEHOLDER] in the agent templates. Use the "Constraints" to add strict rules to the @Security_Lead and @Architect files.

1. Project Identity

Project Name: Python Weather CLI

One-Sentence Pitch: A fast, terminal-based tool to fetch weather data for a given city.

Target Audience: Developers who want weather data directly in their terminal.

2. Technical Stack

Frontend Framework: N/A (CLI Tool)

Styling / UI Library: N/A

Backend / API: Python 3, using the requests library and a public weather API.

Database: None.

Authentication: None.

Hosting / DevOps: Local execution.

3. Core Features (The MVP)

Accept a city name as a command-line argument using Python's native argparse.

Fetch current weather data via HTTP request.

Print the temperature and weather condition clearly to the terminal.

Handle errors gracefully (e.g., city not found, no internet connection).

4. Strict Project Constraints

Coding Standard 1: Strict Python PEP 8 formatting. Use type hinting.

Performance Rule: No heavy frameworks (like Click or Typer). Stick to the standard library where possible.

Security Rule: Do not hardcode API keys; load them from a .env file.

Formatting Rule: Use standard Python docstrings for all functions.

5. Required AI Team (The Roster)

[x] @Architect (Required for initial file structure)

[x] @Senior_Dev (Required for writing the core python code)

[ ] @Security_Lead

[x] @QA_Specialist (Required for testing CLI arguments and API failures)

[x] @Project_Manager (Required for maintaining state)

6. Current Status & Initial Task

Status: Brand new workspace, completely empty.

First Desired Action Post-Setup: Have the @Architect design the simple folder structure and script architecture.
