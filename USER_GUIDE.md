# User Guide

Welcome to SFMC 180! This guide explains how to use the subscriber diagnostics tool.

---

## Getting Started

### Accessing SFMC 180

Open your published CloudPage URL in a web browser. You'll see the home screen with a search box.

---

## Searching for Subscribers

### Search by Email Address

Enter a complete email address in the search box:

```
john.doe@example.com
```

The tool detects the `@` symbol and searches the `EmailAddress` field.

---

### Search by Subscriber Key

Enter a subscriber key (no `@` symbol):

```
CUST-12345-ABCD
```

The tool detects the absence of `@` and searches the `SubscriberKey` field.

---

## Understanding the Results

### Subscriber Profile Card

The top card displays:

| Field | Description |
|-------|-------------|
| **Status** | Current subscriber status (Active, Held, Bounced, Unsubscribed) |
| **Subscriber Key** | The unique identifier for this subscriber |
| **Email** | The subscriber's email address |
| **Domain** | Email domain (e.g., @gmail.com) |
| **Joined** | Date the subscriber was added to SFMC |
| **Locale** | Language/region preference (if set) |

**Status Icons:**
- 😊 Green smiley = Active
- 😢 Red sad face = Bounced
- 😐 Gray neutral = Held or Unsubscribed

---

### Engagement Metrics

Six metric cards show subscriber engagement:

| Metric | Description |
|--------|-------------|
| **Sent** | Total emails sent to this subscriber |
| **Opens** | Number of tracked opens |
| **Clicks** | Number of tracked clicks |
| **Bounces** | Number of bounced emails |
| **Eng. Score** | Calculated engagement score (0-100) |
| **Lists** | Number of lists the subscriber belongs to |

**Rate Calculations:**
- Open Rate = Opens ÷ Sent × 100
- Click Rate = Clicks ÷ Sent × 100
- Bounce Rate = Bounces ÷ Sent × 100

**Engagement Score Formula:**
```
Score = (Opens + (Clicks × 2)) ÷ Sent × 10
```
Capped at 100. Higher scores indicate more engaged subscribers.

---

### Detailed Info Panel

The left panel shows additional details:

- **Subscriber ID** — SFMC's internal numeric ID
- **Last Sent** — Date/time of the most recent send

**Bounce Alert** (if applicable):
- Bounce category (Hard, Soft, Block, etc.)
- Bounce date
- Job ID that caused the bounce
- Email name that bounced

**Unsubscribe Info** (if applicable):
- Unsubscribe reason
- Unsubscribe date

---

### Activity Timeline

The right panel shows the **last 10 email sends** to this subscriber:

**Color Coding:**
- 🔵 Blue border = Sent only (no open or click)
- 🟢 Green border = Opened
- 🟣 Purple border = Clicked

**Each timeline item shows:**
- Email name
- Journey name (if from a Journey, shown as purple pill)
- Send date

**Expand for details:**
Click any timeline item to see:
- Job ID (clickable for more info)
- Subject line
- Sent date/time
- Time to open
- Open time
- Click time

---

## Job Analytics Modal

Click a **Job ID** in the timeline to open the Job Analytics modal:

| Field | Description |
|-------|-------------|
| **Subject Line** | Email subject |
| **Email Name** | Internal email name |
| **Job Status** | Completed, In Progress, etc. |
| **Scheduled** | Scheduled time or "Triggered/API" |
| **Send Type** | Normal, Test, etc. |
| **Tracking** | Active or Disabled |

**Journey Context** (if applicable):
- Journey Name
- Version number
- Journey Status
- Activity Name
- Last Published date

---

## Handling Duplicates

If multiple subscribers share the same email address, SFMC 180 displays a selection screen:

1. You'll see a list of all matching subscriber keys
2. Each shows the subscriber key, status, and join date
3. Click on a row to view that specific subscriber's details
4. Use the "Back to List" button to return to the selection

---

## Tips & Best Practices

### Quick Lookups
- Bookmark the CloudPage for instant access
- Keep it open in a browser tab while working in SFMC

### Troubleshooting Subscribers
1. Check status first — is the subscriber active?
2. Look at bounce info — why did they bounce?
3. Review timeline — are they engaging with sends?
4. Check engagement score — are they worth re-engaging?

### Journey Debugging
- Use the timeline to see which Journey sends reached the subscriber
- Click Job IDs to verify correct Journey and activity names

---

## Keyboard Shortcuts

Currently, SFMC 180 doesn't have keyboard shortcuts. Use standard browser shortcuts:
- `Ctrl/Cmd + F` — Find on page
- `Ctrl/Cmd + R` — Refresh
- `Tab` — Navigate between fields

---

## Limitations

- **Timeline limit**: Shows last 10 sends only
- **Metric caps**: Metrics capped at 500 records for performance
- **Real-time**: Data is real-time from Data Views
- **Enterprise scope**: Uses `ENT._Subscribers` (all business units)

---

## Need Help?

Check [TROUBLESHOOTING.md](TROUBLESHOOTING.md) for common issues and solutions.
