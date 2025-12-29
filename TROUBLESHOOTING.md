# Troubleshooting Guide

This guide helps you resolve common issues with SFMC 180.

---

## Common Issues

### 1. Page Timeout Error (500 Error)

**Symptom:** The page shows an error or times out when searching for a subscriber.

**Cause:** SFMC CloudPages have a 30-second execution limit. Unbounded queries on large Data Views can exceed this.

**Solutions:**

✅ **Already implemented:** SFMC 180 uses `LookupOrderedRows` with row limits (100-500 rows) to prevent timeouts.

If you still experience timeouts:

1. **Check subscriber volume** — Subscribers with thousands of sends may still be slow
2. **Reduce timeline limit** — Edit the code to show fewer than 10 timeline items:
   ```ampscript
   SET @recentSentJobs = LookupOrderedRows("_Sent", 5, "EventDate DESC", "SubscriberKey", @subKey)
   ```
3. **Check SFMC status** — Platform issues can cause slowdowns

---

### 2. "Not Found" for Known Subscriber

**Symptom:** You search for a subscriber you know exists, but get "Not Found."

**Causes & Solutions:**

| Cause | Solution |
|-------|----------|
| Wrong search type | If searching by email, ensure it contains `@`. For subscriber key, don't include `@` |
| Typo in search | Double-check spelling and copy/paste from source |
| Wrong Business Unit | `ENT._Subscribers` searches all BUs. If subscriber is in a different parent BU, they may not appear |
| Recently added | Data Views can have slight delays. Wait a few minutes and retry |
| Deleted subscriber | Subscriber may have been deleted from All Subscribers |

---

### 3. Metrics Show Zero

**Symptom:** Subscriber found, but all metrics (Sent, Opens, etc.) show 0.

**Causes & Solutions:**

| Cause | Solution |
|-------|----------|
| New subscriber | No sends yet — this is expected |
| Tracking disabled | Opens/clicks won't register if tracking is off |
| Data View retention | SFMC Data Views have retention limits (typically 6 months). Older data is purged |
| Wrong subscriber key | If email matches but subscriber key is different, metrics may not align |

---

### 4. Journey Information Not Showing

**Symptom:** Timeline items don't show Journey pills even though sends came from Journeys.

**Causes & Solutions:**

1. **Non-Journey sends** — Email Studio sends don't have Journey context
2. **Triggered sends** — Some triggered sends may not have `TriggererSendDefinitionObjectID` populated
3. **Journey deleted** — If the Journey was deleted, `_Journey` lookup will fail
4. **API sends** — Transactional API sends won't have Journey context

---

### 5. Page Shows Blank/White Screen

**Symptom:** CloudPage loads but shows nothing.

**Causes & Solutions:**

1. **AMPscript error** — Check for syntax errors in the code
2. **Unpublished changes** — Make sure you clicked "Publish" after making edits
3. **Browser cache** — Hard refresh with `Ctrl/Cmd + Shift + R`
4. **View source** — Right-click → View Page Source to see any error messages

**Debug tip:** Add this at the top of your AMPscript to see errors:
```ampscript
%%[ OutputLine(Concat("Debug: searchInput = ", @searchInput)) ]%%
```

---

### 6. Duplicate List Not Showing

**Symptom:** You know multiple subscribers have the same email, but you're taken directly to one.

**Cause:** The duplicate handling only triggers when:
- Searching by email (contains `@`)
- More than one subscriber found
- No `selectedKey` parameter in URL

**Solution:** Clear the URL and search again by email only.

---

### 7. Modal Not Closing

**Symptom:** Job Analytics modal won't close.

**Solutions:**

1. Click the "Close" button at the bottom
2. The close button links back to the search results — ensure URL parameters are intact
3. If stuck, manually remove `&viewJobId=XXX` from the URL

---

### 8. Styling/CSS Issues

**Symptom:** Page looks broken, unstyled, or elements overlap.

**Causes & Solutions:**

1. **Browser compatibility** — Use modern browsers (Chrome, Firefox, Edge, Safari)
2. **SFMC wrapper styles** — Some SFMC instances inject wrapper CSS. Check for conflicts
3. **Code corruption** — Re-copy the original code from the repository
4. **Mobile view** — The page is responsive but optimized for desktop

---

### 9. Permission Denied Errors

**Symptom:** Error messages about Data View access.

**Cause:** Your SFMC user doesn't have permission to query certain Data Views.

**Solution:** Contact your SFMC admin to grant access to:
- `ENT._Subscribers`
- `_Sent`, `_Open`, `_Click`, `_Bounce`, `_Unsubscribe`
- `_ListSubscribers`
- `_Job`, `_Journey`, `_JourneyActivity`

---

### 10. Slow Performance

**Symptom:** Page takes 10+ seconds to load results.

**Optimization tips:**

1. **Reduce row limits** — Lower the `LookupOrderedRows` limits in the code
2. **Limit timeline** — Reduce from 10 to 5 items
3. **Remove Journey lookups** — If you don't need Journey context, comment out those sections
4. **Check platform** — SFMC performance varies by stack and time of day

---

## Error Messages

| Error | Meaning | Solution |
|-------|---------|----------|
| `500 Internal Server Error` | Page timeout or AMPscript error | Check for unbounded queries or syntax errors |
| `Function not found` | AMPscript function name typo | Verify function names (case-sensitive) |
| `Invalid column` | Data View column doesn't exist | Check column names match SFMC documentation |
| `Null value` | Trying to format/use a null field | Add `IF NOT EMPTY()` checks |

---

## Getting More Help

### SFMC Resources
- [Salesforce Help](https://help.salesforce.com/s/products/marketing-cloud)
- [SFMC Stack Exchange](https://salesforce.stackexchange.com/questions/tagged/marketing-cloud)
- [Trailblazer Community](https://trailhead.salesforce.com/trailblazer-community)

### Report Issues
If you find a bug in SFMC 180, please open an issue on GitHub with:
1. Steps to reproduce
2. Expected behavior
3. Actual behavior
4. Screenshots (if applicable)
5. Any error messages

---

## Debug Mode

To enable debug output, add this code after the variable initialization section:

```ampscript
%%[
/* DEBUG OUTPUT - Remove in production */
Output(Concat("<pre>"))
Output(Concat("searchInput: ", @searchInput, "<br>"))
Output(Concat("isEmailSearch: ", @isEmailSearch, "<br>"))
Output(Concat("subRowCount: ", @subRowCount, "<br>"))
Output(Concat("subKey: ", @subKey, "<br>"))
Output(Concat("subStatus: ", @subStatus, "<br>"))
Output(Concat("</pre>"))
]%%
```

This will display variable values at the top of the page to help diagnose issues.
