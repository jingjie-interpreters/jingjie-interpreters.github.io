# Requirements Specification

## Functional Requirements

### FR1 — Twitch Live Stream Embed
- **FR1.1**: A 16:9 video container shall be centered on the page, responsive in width.
- **FR1.2**: When the Twitch channel is live, the container shall display the real-time stream via Twitch Embed API.
- **FR1.3**: When the Twitch channel is offline, the container shall display a user-provided looping GIF (`assets/offline.gif`).
- **FR1.4**: Switching between live and offline states shall occur automatically via `Twitch.Player.ONLINE` / `Twitch.Player.OFFLINE` events.
- **FR1.5**: The `parent` parameter for the Twitch embed shall be dynamically obtained from `window.location.hostname`.

### FR2 — Text Input & Firebase Submission
- **FR2.1**: A text input field shall appear directly below the stream container. Placeholder text: "Enter text to interact..."
- **FR2.2**: A "Send" button shall appear adjacent to the input field.
- **FR2.3**: On send, the input shall be validated client-side:
  - If empty: display red text "Content cannot be empty."
  - If >150 English characters: display red text "A single submission cannot exceed 150 characters."
- **FR2.4**: During submission, the button shall be disabled to prevent duplicate requests.
- **FR2.5**: Valid text shall be written to Firebase Realtime Database at path `messages/` with structure:
  ```json
  {
    "text": "<user input>",
    "timestamp": <unix milliseconds>,
    "status": "pending"
  }
  ```
- **FR2.6**: On successful write: clear the input field and re-enable the button.
- **FR2.7**: On failed write: display red text "Submission failed, please retry." and re-enable the button.

### FR3 — Project Information Display
- **FR3.1**: Below the input area, display a cover image (`assets/cover.jpg`).
- **FR3.2**: Display an artist bio paragraph (placeholder, English).
- **FR3.3**: Display a project statement paragraph (placeholder, English).
- **FR3.4**: An expandable section titled "Web Logistics Flow" shall reveal `assets/logistics.png` when expanded.
- **FR3.5**: An expandable section titled "Technical Signal Flow" shall reveal `assets/technical.png` when expanded.

### FR4 — UI Design
- **FR4.1**: Background color shall be `#303030`.
- **FR4.2**: Typography shall use monospace font stack.
- **FR4.3**: A subtle noise texture overlay shall be applied via CSS.
- **FR4.4**: All visible text shall be in grammatically correct English.
- **FR4.5**: The design shall be responsive and mobile-friendly.

## Non-Functional Requirements
- **NFR1**: Single static HTML file — no build tools or frameworks.
- **NFR2**: All external dependencies loaded via CDN (Twitch SDK, Firebase SDK).
- **NFR3**: Deployable directly to GitHub Pages without configuration changes.
- **NFR4**: Firebase API key exposure is acceptable (frontend SDK design).
