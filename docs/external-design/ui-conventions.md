# UI Conventions: iHanoi Alert Module

> DBIZ2 Lesson 8 · One page. Every Screen Spec in `screens/` uses the component names and message patterns below. Items marked "assumption" are not in any source file and need the client's or team's confirmation.

## 1. Language and tone

- Interface language: Vietnamese is the default and English is available (assumption; iHanoi serves Hanoi citizens). The Screen Specs and mockups are written in English for the course; Vietnamese labels are a translation step before DBIZ3.
- Address the user as: "bạn" in Vietnamese, "you" in English; no formal titles on any screen, including staff screens.
- Button labels are verbs that say what happens: "Send report", "Declare missing", "Update status", "Show audit trail", not "OK" or "Submit".
- Messages are short and name the object: "Report sent", not "Success".

## 2. Formats

| Item | Format | Example |
|---|---|---|
| Date | dd/mm/yyyy | 16/10/2026 |
| Time | 24-hour, hh:mm | 09:00 |
| Date and time together | date, then time | 16/10/2026 09:40 |
| Currency | The module shows no money amounts. If one is ever needed: thousands separated by a dot, then ₫ | 120.000 ₫ |
| Phone | Display with the national prefix and spaces | 0912 345 678 |
| Names | Family name first, then given name (Vietnamese order) | Nguyễn Văn An |
| Alert ID | `A-` and four digits | A-1002 |
| Case ID (missing person / pet / asset) | `M-` and three digits | M-101 |
| Coordinates | latitude, longitude, four decimals (assumption) | 21.0136, 105.8014 |
| Confidence score | two decimals, 0.00 to 1.00 | 0.85 |
| Duration (SLA) | hours with one decimal | 3.0 h |
| Status | exactly one of Submitted, Routed, In Progress, Resolved; "Handed to Police" is shown as In Progress until decided. Vietnamese labels: Đã gửi, Đã chuyển, Đang xử lý, Đã giải quyết | Routed |

ID formats come from the test data of the activity diagrams (AD-UC-06 and AD-UC-15 use other sample IDs); the team must fix one pattern.

## 3. Components (use these names in every Screen Spec)

| Component | When to use | Notes |
|---|---|---|
| Header | Top of every screen: title and back arrow | One per screen; the back arrow returns to the screen the user came from |
| Primary button | The one main action of a screen | One per screen (for example "Send report") |
| Secondary button | Alternative actions | Outlined; never next to a second primary button |
| Text input | One-line free text or an ID | Label above, error message below, a star marks required fields |
| Text area | Descriptions | Same as text input, several lines |
| Segmented selector | Choose exactly one of two to four short options | "Person / Pet / Asset"; "Resolved / Handed to Police" |
| Photo picker | Add photos or videos | Shows thumbnails with a remove action |
| Map | Show or set a location | Draggable pin when it is an input; read only otherwise |
| List item | One record in a list | Two lines: ID and short text, then date, time or status |
| Status chip | Show a status | Text plus an icon, never colour alone |
| Status steps | Show where a report is in its life | Four steps; the current step is marked with an icon and text |
| Banner | Non-blocking information or an error inside a screen | Sits where the content would be |
| Modal | Confirm or cancel a single action | Never for navigation; examples: "Discard report?", "Confirm status change" |
| Toast | Short confirmation after success | Disappears by itself after a few seconds |
| Skeleton | Loading state of a list or a detail screen | Grey bars in the shape of the content; no spinner on the whole screen. Buttons that do not depend on the data stay usable |
| Spinner button | Loading state after the user taps the primary button | The button shows a spinner and a verb in progress ("Sending…", "Updating…") and is disabled; form fields are locked |
| Retry action | Inside an error banner when the request can be repeated | Text button "Retry" at the right end of the banner |
| Blocked message | Access denied or "not available" in place of the whole content | Icon plus one sentence from section 4, and a way back (back arrow or Back button) |

## 4. Messages

| Situation | Pattern | Example |
|---|---|---|
| Validation error | what is wrong + how to fix | "Describe what happened so the right agency can act." under the description field |
| System error | what happened + what the user can do now | "Could not send. Your report is kept on this screen. Try again." |
| Access denied | what is not allowed, no detail about why | "You are not allowed to change this case." |
| Not available | one message for "does not exist" and "not yours" | "This report is not available." |
| Empty state | why it is empty + the next action | "You have not sent any reports yet." with the button "Report an incident" |
| Duplicate | what exists + its ID | "A similar report already exists: A-1001." |
| Success | what was done | "Report sent. Alert ID A-1002. Status: Submitted." |

## 5. Accessibility minimums

- Body text contrast at least 4.5:1 (WCAG 2.2, success criterion 1.4.3).
- Information is never carried by colour alone (WCAG 2.2, 1.4.1): statuses, "OVER SLA" and errors use text and an icon.
- Tap targets at least 24 by 24 CSS pixels (WCAG 2.2, 2.5.8).
- Smallest supported screen width: 360px. The module is designed mobile first; staff screens use the same layout (assumption: a wider web layout for HPC dashboards is a later decision).

## 6. State mockups

- Every screen has one state sheet, `screens/img/ENG/<Screen ID>-en.png` (English) and `screens/img/VIE/<Screen ID>-vi.png` (Vietnamese). Editable sources: `screens/figma/en/` and `screens/figma/vi/` (SVG, drag into Figma; one frame per screen, text and shapes stay editable).
- Frames follow section 4 of the Screen Spec: Default, Empty, Loading, Error and Success first, then the other states of the spec (system error, duplicate, modal, access denied). A state marked "Not applicable" keeps its frame with the reason ("Không áp dụng"), so reviewers see it was considered.
- When a spec names two kinds of error (validation and system, or access denied and system), each gets its own frame.
- Visual style: blue gradient header with a city skyline and a topic icon, large screen title, white rounded card, pill chips for statuses, navy pill buttons (outline for secondary), grey skeleton bars while loading, dashed tiles for photos, a map block with a location chip. The status bar shows 9:41, signal, wifi and battery. There are no element numbers and no tab bar.
- Every sheet exists in two languages with the same frames, order and sample data: English (the language of the Screen Specs, `screens/img/ENG/`, `screens/figma/en/`) and Vietnamese, the default interface language of section 1 (`screens/img/VIE/`, `screens/figma/vi/`; address "bạn"). Sample data uses the formats of section 2. Values that the specs leave open are shown as sample data in the mockups only: SLA thresholds 2 h (routing) and 24 h (resolution) on S-F04-01 (spec question 1), and the station name on S-F03-02. Statuses use exactly the four values of section 2.
- A primary button whose validation rule is not yet met is drawn disabled in the Default state.
- S-F01-01 follows the reference design for the form components: description with a counter, three dashed media tiles, a map with a "Use my location" chip, an additional-details dropdown, and the send button and Cancel link below the card. The citizen does not choose an incident type or a priority: the system classifies the report, an authority reviewer verifies it when needed, and the citizen is notified afterwards (S-F01-01 spec, rule SR-006). S-F01-04 to S-F01-06 use the same components (icon chips for the case type or outcome, dashed photo tile, send button outside the card).
