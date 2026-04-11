# PrenatalCare Pro — Mother's Safe Hospital

---

## Tech Stack
- **React 18** (JSX, hooks — useState, useEffect, useRef)
- **In-memory state** with deep-copy pattern (`JSON.parse(JSON.stringify(...))`)
- All data stored in React state; architecture mirrors the Firestore-backed production system described in the IA

---

## How to Run

### Option A — Direct (no install needed)
Open `src/App.jsx` in any **StackBlitz**, **CodeSandbox**, or **Replit** React project and replace the default `App.jsx`.

### Option B — Local Development
Requires **Node.js ≥ 16**

```bash
# 1. Install dependencies
npm install

# 2. Start development server
npm start

# 3. App opens at http://localhost:3000
```

---

## Demo Credentials

### Doctor Portal
| Name | Username | Password |
|------|----------|----------|
| Dr. Likitha Reddy | `doctor1` | `doctor123` |
| Dr. Meera Patel | `doctor2` | `doctor456` |

### Patient Portal
| Name | Username | Password |
|------|----------|----------|
| Priya Sharma | `patient1` | `pat123` |
| Sita Rao | `sita1` | `sita123` |

> Tap the **"Demo — tap to fill"** section on the login screen to auto-fill credentials.

---

## Features (All 14 Success Criteria Met)

1. **Dual-role login** — Doctor & Patient portals with credential validation; invalid login shows red error banner
2. **Patient registration** — Doctor adds patients with full prenatal details; appears immediately in list
3. **Vital signs + BP classification** — Log visits with BP, weight, HR, Fetal HR; colour-coded: Green (Normal <130), Orange (High BP 130–139), Red (Critical ≥140)
4. **Vital history + BP badge** — All visits listed in Vitals tab; live BP badge on patient tile
5. **Medication management** — Doctor edits via modal; patient views read-only
6. **Diet plan management** — Doctor edits via modal; patient views read-only
7. **Appointment workflow** — Patient books → pending; Doctor accepts/denies with date/time/reason
8. **Real-time messaging** — Shared state chat; scrolls to latest message automatically
9. **Patient Portal read-only** — No write functions exposed to patient-facing components
10. **Pregnancy week progress** — Visual progress bar: (week/40)×100%, capped at 100
11. **Search + BP filter** — Live `Array.filter()` dual-condition: name search AND BP category
12. **Input validation** — Required fields checked before save; descriptive red toast on error
13. **Session persistence** — State persists across tab navigation within session
14. **Offline capability** — In-memory state always available; mirrors IndexedDB persistence architecture

---

## Key Architecture Notes (matching IA Criterion C)

- **`updateDoc(fn)`** — Deep-copies state before mutation; ensures React detects changes
- **`bpStatus(sys)`** — Pure function: systolic → `{label, color, bg}`; used in 4 places
- **`addVital(pid, v)`** — Appends vital AND writes back `bpCategory` to patient document
- **`patientSend(text)`** — Uses `setData` directly with `currentPat.docKey` (not `updateDoc`) since patient ≠ `currentDoc`
- **`EditListModal`** — Local state for list edits; only calls parent `onSave` on explicit Save button
- **`showToast(msg, color)`** — Auto-dismisses after 2500ms via `setTimeout`

---

## Project Structure

```
prenatal-care-pro/
├── public/
│   └── index.html
├── src/
│   ├── index.js        ← React entry point
│   └── App.jsx         ← Complete application (single-file architecture, as per IA)
├── package.json
└── README.md
```
