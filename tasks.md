# Implementation Plan: MoodPet

## Overview

Build a single-page React app with functional components and hooks. All state lives in the root `App` component. Child components are purely presentational. Styled with a single CSS file using pastel colors and rounded elements.

## Tasks

- [x] 1. Scaffold the React project and set up the file structure
  - Initialize a new React app (e.g., `npm create vite@latest mood-pet -- --template react`)
  - Install `fast-check` for property-based testing: `npm install --save-dev fast-check`
  - Create the following files: `src/App.jsx`, `src/App.css`, `src/components/Header.jsx`, `src/components/MoodCheckin.jsx`, `src/components/DailyTasks.jsx`, `src/components/PointsDisplay.jsx`, `src/components/PetDisplay.jsx`
  - Define the `PETS` constant and initial `TASKS` array in `src/data.js`
  - _Requirements: 1.1, 3.1, 5.2_

- [ ] 2. Implement core state and logic in App
  - [x] 2.1 Implement App component with state and handlers
    - Add `useState` for `selectedMood`, `tasks`, and `points`
    - Implement `handleMoodSelect(mood)` — sets selectedMood
    - Implement `handleTaskToggle(id)` — toggles task checked state and adjusts points (+10 / -10)
    - Derive `activePet` and `pointsToNext` from `points` using the `PETS` array
    - _Requirements: 2.2, 4.2, 4.3, 4.5, 5.3, 5.5, 5.6, 6.1, 6.2, 6.3_

  - [ ]* 2.2 Write property test: points invariant
    - **Property 4: Points equal 10 × number of checked tasks**
    - Use fast-check to generate random sequences of toggle operations, assert `points === 10 * checkedCount` after each step
    - **Validates: Requirements 4.2, 4.3, 4.5**

  - [ ]* 2.3 Write property test: active pet correctness
    - **Property 5: Active pet matches highest unlocked tier**
    - Use fast-check to generate random point values (0–100), assert `activePet.threshold <= points` and no higher-threshold pet qualifies
    - **Validates: Requirements 5.3**

  - [ ]* 2.4 Write property test: points-to-next correctness
    - **Property 6 & 7: Points-to-next is correct or null at max tier**
    - Use fast-check to generate random point values, assert `pointsToNext === nextPet.threshold - points` or `null` when at max
    - **Validates: Requirements 5.5, 5.6**

- [ ] 3. Implement presentational components
  - [x] 3.1 Implement Header component
    - Render the "MoodPet" title
    - _Requirements: 1.1_

  - [x] 3.2 Implement MoodCheckin component
    - Render four mood buttons: Happy, Neutral, Sad, Stressed
    - Highlight the selected mood (e.g., via a CSS class or inline style)
    - Accept `selectedMood` and `onMoodSelect` props
    - _Requirements: 2.1, 2.2_

  - [ ]* 3.3 Write property test: mood selection replaces previous
    - **Property: Selecting a mood deselects any prior mood**
    - Use fast-check to generate two different mood values, select the first then the second, assert only the second is selected
    - **Validates: Requirements 6.1**

  - [x] 3.4 Implement DailyTasks component
    - Render a checkbox and label for each task in the `tasks` prop
    - Call `onTaskToggle(id)` when a checkbox is clicked
    - _Requirements: 3.1, 3.2_

  - [ ]* 3.5 Write property test: checkbox renders for each task
    - **Property: Task checkbox renders for each task in the list**
    - Use fast-check to generate arrays of task objects, render DailyTasks, assert one checkbox per task
    - **Validates: Requirements 3.2**

  - [x] 3.6 Implement PointsDisplay component
    - Render the current points total
    - Accept `points` prop
    - _Requirements: 4.4_

  - [x] 3.7 Implement PetDisplay component
    - Render the active pet emoji and name
    - Render points-to-next message, or a completion message if `pointsToNext` is null
    - Accept `activePet` and `pointsToNext` props
    - _Requirements: 5.1, 5.4, 5.5, 5.6_

- [x] 4. Checkpoint — Ensure all tests pass
  - Ensure all tests pass, ask the user if questions arise.

- [ ] 5. Apply styling
  - [x] 5.1 Write App.css with pastel color scheme and layout
    - Center all content horizontally (flexbox column on body/App)
    - Define pastel background and accent colors
    - Apply `border-radius` to all buttons
    - Style mood buttons with selected/unselected states
    - Style task list items and checkboxes
    - Style pet display section
    - _Requirements: 1.2, 1.3, 1.4_

- [ ] 6. Wire everything together in App
  - [x] 6.1 Render all components in App with correct props
    - Render Header, MoodCheckin, DailyTasks, PointsDisplay, PetDisplay in order
    - Pass all state and handlers as props
    - _Requirements: 1.1, 2.3, 3.3_

  - [ ]* 6.2 Write unit tests for initial render
    - Assert title "MoodPet" is present
    - Assert points start at 0
    - Assert all 3 task labels are present
    - Assert pet section is present
    - _Requirements: 1.1, 4.1, 3.1, 5.1_

- [x] 7. Final checkpoint — Ensure all tests pass
  - Ensure all tests pass, ask the user if questions arise.

## Notes

- Tasks marked with `*` are optional and can be skipped for a faster MVP
- Each task references specific requirements for traceability
- Property tests use fast-check with a minimum of 100 iterations each
- Tag format for property tests: `Feature: mood-pet, Property {N}: {property_text}`
