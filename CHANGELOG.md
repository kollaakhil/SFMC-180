# Changelog

All notable changes to SFMC 180 will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.0.0] - 2025-01-01

### Added
- Initial release of SFMC 180
- **Dual Lookup**: Search by email address OR subscriber key
- **Subscriber Profile**: Status, join date, locale, domain display
- **Engagement Metrics**: Sent, Opens, Clicks, Bounces, Lists counts
- **Engagement Score**: Calculated score based on subscriber activity
- **Bounce Intelligence**: Detailed bounce category, job ID, email name
- **Unsubscribe Tracking**: Reason and timestamp display
- **Activity Timeline**: Last 10 sends with open/click indicators
- **Journey Context**: Journey name and version on timeline items
- **Job Analytics Modal**: Deep dive into send job details
- **Duplicate Handling**: Selection UI for multiple subscribers with same email
- **Performance Optimization**: Bounded queries to prevent SFMC timeouts
- **Modern UI**: Clean, responsive design with Google-inspired aesthetics
- **Status Indicators**: Visual emoji icons based on subscriber status

### Technical Details
- Uses `LookupOrderedRows` with explicit row limits (100-500)
- Queries 10 Data Views for comprehensive subscriber data
- Enterprise-level subscriber lookup via `ENT._Subscribers`
- Responsive CSS with mobile support

---

## Future Roadmap

### Planned Features
- [ ] Export subscriber data to CSV
- [ ] Bulk subscriber lookup
- [ ] Custom date range for timeline
- [ ] Additional engagement metrics
- [ ] Dark mode theme option
- [ ] List membership details view
- [ ] Send preview capability

### Under Consideration
- Authentication/login requirement
- API endpoint version
- Integration with Data Cloud
- Multi-language support

---

## Contributing

Want to contribute? See the main [README.md](README.md) for guidelines.
