# Requirements Document

## Introduction

MoodPet is a simple React web application for mental health tracking. It provides a single-page interface where users can log their current mood, complete daily wellness tasks, and earn points for healthy habits. As users accumulate points by completing tasks, they unlock access to different pets. The app uses a clean, pastel-colored UI to create a calm and encouraging experience.

## Glossary

- **App**: The MoodPet React single-page application
- **User**: A person using the MoodPet web app in their browser
- **Mood**: One of four emotional states the user can select: Happy, Neutral, Sad, or Stressed
- **Task**: A daily wellness activity with a checkbox that the user can mark as complete
- **Points**: A numeric score that increases when the user completes tasks and drives pet progression
- **Check-in**: The act of selecting a mood button to record the current emotional state
- **Pet**: A virtual companion displayed in the app; different pets are unlocked at different point thresholds
- **Active_Pet**: The pet currently displayed, determined by the user's highest unlocked pet tier

## Requirements

### Requirement 1: App Layout and Title

**User Story:** As a user, I want to see a clearly titled, centered page, so that I know I am using MoodPet and can navigate it easily.

#### Acceptance Criteria

1. THE App SHALL display the title "MoodPet" prominently at the top of the page
2. THE App SHALL center all content horizontally on the page
3. THE App SHALL apply a soft pastel color scheme throughout the interface
4. THE App SHALL use rounded corners on all interactive buttons

---

### Requirement 2: Mood Check-In

**User Story:** As a user, I want to select my current mood from a set of options, so that I can log how I am feeling today.

#### Acceptance Criteria

1. THE App SHALL display exactly four mood buttons: Happy, Neutral, Sad, and Stressed
2. WHEN a user clicks a mood button, THE App SHALL visually indicate which mood is currently selected
3. THE App SHALL display the mood check-in section below the title

---

### Requirement 3: Daily Tasks

**User Story:** As a user, I want to see a list of daily wellness tasks with checkboxes, so that I can track my healthy habits.

#### Acceptance Criteria

1. THE App SHALL display exactly three daily tasks: "Drink water", "Go outside for 5 minutes", and "Text a friend"
2. WHEN a task is displayed, THE App SHALL render a checkbox alongside each task label
3. THE App SHALL display the daily tasks section below the mood check-in section

---

### Requirement 4: Points System

**User Story:** As a user, I want to earn points when I complete daily tasks, so that I feel rewarded for practicing healthy habits.

#### Acceptance Criteria

1. THE App SHALL initialize the points counter at 0 when the app first loads
2. WHEN a user checks an unchecked task, THE App SHALL add 10 points to the current points total
3. WHEN a user unchecks a previously checked task, THE App SHALL subtract 10 points from the current points total
4. THE App SHALL display the current points total in a dedicated section
5. IF a task is already checked and the user clicks it again, THE App SHALL NOT add additional points beyond the single 10-point increment for that task

---

### Requirement 5: Pet Progression

**User Story:** As a user, I want to unlock new pets as I earn more points, so that I feel motivated to keep completing daily tasks.

#### Acceptance Criteria

1. THE App SHALL display a pet companion in a dedicated section of the page
2. THE App SHALL define at least three pet tiers, each unlocked at a specific point threshold
3. WHEN the user's points reach a new pet tier threshold, THE App SHALL update the Active_Pet to the newly unlocked pet
4. THE App SHALL display the name or visual representation of the Active_Pet
5. THE App SHALL display progress toward the next pet unlock, showing how many more points are needed
6. WHEN the user has unlocked the highest pet tier, THE App SHALL indicate that all pets have been unlocked

---

### Requirement 6: State Persistence Within Session

**User Story:** As a user, I want my mood selection, task completions, and pet progress to remain visible during my session, so that I can see my progress without losing it.

#### Acceptance Criteria

1. WHILE the app is running, THE App SHALL retain the selected mood state until the user selects a different mood
2. WHILE the app is running, THE App SHALL retain the checked state of each task until the user explicitly unchecks it
3. WHILE the app is running, THE App SHALL retain the current points total and Active_Pet as tasks are checked and unchecked
