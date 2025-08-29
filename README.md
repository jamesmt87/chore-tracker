# Chore Tracker

A Firebase-backed daily chore tracking web app built for two users: **Annabel** and **Amelia**. This tracker allows for:

- Daily tracking of paid and required chores
- Earnings accumulation (total and lifetime)
- Manual earnings adjustments
- Auto-reset of chore checkboxes at the start of each new day

---

## 🔧 Technologies Used

- **HTML/CSS**: for layout and styling
- **JavaScript (ES Modules)**: for DOM manipulation and Firebase integration
- **Firebase Firestore**: to store chore data and sync state in real-time

---

## 📁 Firebase Firestore Structure

Each user (`annabel`, `amelia`) has a document in the `users` collection with the following fields:

```json
{
  "total": 0,
  "lifetime": 0,
  "paidChores": ["Chore 1", "Chore 2"],
  "requiredChores": ["Chore A", "Chore B"],
  "lastReset": "2025-08-28"
}
```

### Field Descriptions:
- **total**: Money earned today from paid chores.
- **lifetime**: All-time total earnings (manual edits allowed).
- **paidChores**: List of chores that add to `total` when checked.
- **requiredChores**: List of chores not tied to earnings.
- **lastReset**: ISO date string of last checkbox reset.

---

## ⏱ Daily Reset Mechanism

When the app loads, it checks if `lastReset` is different from today's date. If so:
- It resets all checkboxes (visually and internally)
- Updates the `lastReset` field in Firestore

This ensures the chore list is fresh each day without wiping out earnings.

---

## 🧠 Features

- Two user panels shown side-by-side
- Visual separation of **Paid** and **Required** chores
- Manual `+` and `-` controls to adjust earnings
- “Paid” button adds today’s total to lifetime and resets total
- Secret Shift+L combo shows lifetime editing input

---

## 📌 Notes

- This version relies on `checkedMap` (local) for visual checkbox states. Daily reset logic ensures it's cleared each new day.
- Firestore `onSnapshot` keeps the UI in sync in real-time when updates are made.