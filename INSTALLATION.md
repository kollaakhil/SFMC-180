# Installation Guide

This guide walks you through setting up SFMC 180 in your Salesforce Marketing Cloud instance.

---

## Prerequisites

Before you begin, ensure you have:

- [ ] Access to Salesforce Marketing Cloud
- [ ] Permissions to create CloudPages
- [ ] Permissions to query system Data Views

---

## Step 1: Access Web Studio

1. Log in to Salesforce Marketing Cloud
2. Navigate to **Web Studio** from the main menu
3. Click on **CloudPages**

---

## Step 2: Create a New CloudPage Collection (if needed)

If you don't have an existing collection for internal tools:

1. Click **Create Collection**
2. Name it something like `Internal Tools` or `Admin Utilities`
3. Click **Save**

---

## Step 3: Create the CloudPage

1. Open your collection
2. Click **Create** → **Landing Page**
3. Name it `SFMC 180` or `Subscriber Diagnostics`
4. Click **Create**

---

## Step 4: Add the Code

1. In the CloudPage editor, switch to **Code View** (not the drag-and-drop editor)
2. Delete any default code/content
3. Open `cloudpage/sfmc180.html` from this repository
4. Copy the entire contents
5. Paste into the CloudPage code editor

---

## Step 5: Publish

1. Click **Publish** in the top right
2. Confirm the publish action
3. Copy the published URL

---

## Step 6: Test

1. Open the published CloudPage URL in a new browser tab
2. Enter a known subscriber email or subscriber key
3. Verify the results display correctly

---

## 🔗 Sharing Access with Your Team

Once published, you have several options to share SFMC 180 with your team:

### Option A: Direct Bookmark

Share the CloudPage URL directly with team members and have them bookmark it in their browser.

```
https://cloud.YOUR-STACK.exacttarget.com/cloudpage/YOUR-PAGE-ID
```

**Tip:** Add it to your browser's bookmarks bar for one-click access.

---

### Option B: Store URL in a Data Extension

Create a simple Data Extension to store internal tool URLs that your team can reference:

**Data Extension: `Admin_QuickLinks`**

| Field Name | Data Type | Length | Primary Key |
|------------|-----------|--------|-------------|
| LinkName | Text | 100 | Yes |
| LinkURL | Text | 500 | No |
| Description | Text | 255 | No |
| SortOrder | Number | - | No |

**Sample Data:**

| LinkName | LinkURL | Description | SortOrder |
|----------|---------|-------------|-----------|
| SFMC 180 | https://cloud... | Subscriber diagnostics tool | 1 |

This approach lets you:
- Maintain a central list of internal tools
- Easily update URLs if pages are republished
- Build a "quick links" dashboard CloudPage that reads from this DE

---

### Option C: Team Communication Channels

- Pin the URL in your team's Slack/Teams channel
- Add to your company wiki or internal documentation
- Include in onboarding materials for new team members

---

## 🔐 Security Considerations

### Restrict Access (Optional)

By default, the CloudPage is publicly accessible to anyone with the URL. For additional security, consider:

1. **IP Restriction** — Add AMPscript at the top to check IP ranges
2. **Authentication** — Require login via SFMC user authentication
3. **Obscure URL** — Don't share the URL publicly; treat it as internal-only

**Example IP Check (add at the very top of the code):**

```ampscript
%%[
VAR @clientIP
SET @clientIP = RequestParameter("HTTP_X_FORWARDED_FOR")

/* Add your allowed IP ranges */
IF IndexOf(@clientIP, "YOUR.COMPANY.IP") == 0 THEN
    /* Not from allowed IP - show error or redirect */
    Redirect("https://your-company.com")
ENDIF
]%%
```

---

## ✅ Installation Complete

You should now have SFMC 180 running in your Marketing Cloud instance!

For usage instructions, see [USER_GUIDE.md](docs/USER_GUIDE.md).

If you encounter issues, check [TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md).
