# SFMC 180

![SFMC 180 Homepage](docs/screenshots/homepage.png)

**A powerful subscriber diagnostics tool for Salesforce Marketing Cloud**

SFMC 180 gives you a complete 360° view (well, 180° at a time 😉) of any subscriber in your Marketing Cloud instance. Instantly look up engagement metrics, bounce history, journey context, and recent activity — all from a single CloudPage.

---

## ✨ Features

- **Dual Lookup** — Search by email address OR subscriber key
- **Subscriber Profile** — Status, join date, locale, and domain analysis
- **Engagement Metrics** — Sends, opens, clicks, bounces with calculated rates
- **Engagement Score** — Proprietary scoring based on subscriber activity
- **Bounce Intelligence** — Detailed bounce category, job info, and email name
- **Unsubscribe Tracking** — Reason and timestamp for unsubscribes
- **Activity Timeline** — Last 10 sends with open/click tracking per job
- **Journey Context** — See which Journey and activity triggered each send
- **Job Analytics Modal** — Deep dive into any send job's details
- **Duplicate Handling** — Gracefully handles multiple subscribers with same email
- **Performance Optimized** — Bounded queries to prevent SFMC timeout errors

---

## 🚀 Quick Start

1. Copy the code from `cloudpage/sfmc180.html`
2. Create a new CloudPage in SFMC
3. Paste the code and publish
4. Start searching subscribers!

For detailed setup instructions, see [INSTALLATION.md](INSTALLATION.md)

---

## 📖 Documentation

| Document | Description |
|----------|-------------|
| [INSTALLATION.md](INSTALLATION.md) | Step-by-step setup guide |
| [USER_GUIDE.md](docs/USER_GUIDE.md) | How to use SFMC 180 |
| [TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md) | Common issues and fixes |

---

## 🔧 Requirements

- Salesforce Marketing Cloud account
- Access to CloudPages
- Appropriate permissions to query Data Views:
  - `ENT._Subscribers`
  - `_Sent`
  - `_Open`
  - `_Click`
  - `_Bounce`
  - `_Unsubscribe`
  - `_ListSubscribers`
  - `_Job`
  - `_Journey`
  - `_JourneyActivity`

---

## 📊 Data Views Used

| Data View | Purpose |
|-----------|---------|
| `ENT._Subscribers` | Core subscriber lookup |
| `_Sent` | Send history and counts |
| `_Open` | Open tracking |
| `_Click` | Click tracking |
| `_Bounce` | Bounce details |
| `_Unsubscribe` | Unsubscribe info |
| `_ListSubscribers` | List membership count |
| `_Job` | Email/job details |
| `_Journey` | Journey names and status |
| `_JourneyActivity` | Journey activity mapping |

---

## ⚡ Performance Notes

SFMC 180 is built with platform constraints in mind:

- **30-second timeout protection** — All Data View queries use `LookupOrderedRows` with explicit row limits (100-500 rows) instead of unbounded `LookupRows`
- **Optimized query count** — Caches results to minimize redundant lookups
- **Bounded timeline** — Shows last 10 sends to balance detail with performance

---

## 🤝 Contributing

Contributions are welcome! Feel free to:

- Report bugs
- Suggest features
- Submit pull requests

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👤 Author

**Akhil Kolla**

---

## 🤖 Powered by AI

This project was developed with AI assistance.

---

## ⭐ Support

If you find SFMC 180 useful, consider giving it a star on GitHub!
