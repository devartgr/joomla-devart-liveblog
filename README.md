# DevArt Liveblog for Joomla

Live blogging inside Joomla articles for editorial, sports, news and
high-traffic sites — with CDN-friendly live updates, an editor console and
one-click conversion to a regular article.

![Joomla](https://img.shields.io/badge/Joomla-6.x-blue)
![PHP](https://img.shields.io/badge/PHP-8.3%2B-green)
![Release](https://img.shields.io/badge/Version-1.1.0-orange)
![License](https://img.shields.io/badge/License-GPLv3-red)

---

## Overview

DevArt Liveblog is a Joomla 6 native package for live coverage inside articles.

Editors publish updates from an administrator Live Console. Readers see a
server-rendered snapshot in the article and receive new posts through a shared,
cacheable JSON feed — designed for Cloudflare Full Page Cache and high
concurrency.

When coverage ends, convert the live blog into a self-contained archive timeline
inside the linked article so the page remains valid after the component is no
longer needed.

---

## Features

### Live Console

- Publish, edit, unpublish, pin and delete updates without page reloads
- Concurrent editor sync
- Go live / pause / end workflow
- Load earlier posts for long sports and news events
- Dedicated image upload and browse under `/images` (CSRF + item ACL)

### Article embedding

- Shortcode `{devartliveblog id=N}` via content plugin
- SSR-friendly HTML for SEO and no-JS fallback
- editors-xtd button inserts the shortcode from the article editor

### CDN-friendly live feed

- Default static feed mode writes `media/com_devartliveblog/feeds/<id>[-lang].txt`
- Optional Cloudflare purge of the feed URL after each version bump
- PHP feed remains a fallback / restricted-access path
- Language-aware feeds and ETags for multilingual sites

### End & Convert

- End first, then convert
- Replaces the shortcode with self-contained archive HTML (plain semantic markup)

### Administrator experience

- Dashboard hub with stats and workflow guidance
- Live blogs list with status badges and console access
- Centered responsive admin headers
- Soft-deleted post retention option + scheduled purge task plugin
- 15 language packs

---

## Included Extensions

This package installs:

- `com_devartliveblog`
- `plg_content_devartliveblog`
- `plg_editors-xtd_devartliveblog`
- `plg_task_devartliveblog`

Plugins are enabled on install/update.

---

## Requirements

- Joomla 6.x
- PHP 8.3+

---

## Installation

1. Download the latest release ZIP (`pkg_devartliveblog_v1.1.0.zip`)
2. Open:

```text
System → Extensions → Install
```

3. Upload the package ZIP
4. Open:

```text
Components → DevArt Liveblog
```

5. Create a live blog, link an article, insert the shortcode, open the Live Console

---

## Joomla Native Updates

Supports Joomla native updates via GitHub.

Update location:

```text
System → Extensions → Update
```

Update server:

```text
https://raw.githubusercontent.com/devartgr/joomla-devart-liveblog/main/update.xml
```

Install or update using the full package ZIP only.

---

## Performance

Designed for production and high-traffic use.

- Shared static feed for all readers
- Edge-friendly cache headers (when using PHP feed fallback)
- Vanilla deferred frontend script with jitter/backoff
- Polling stops when status is ended or converted
- Cloudflare Full Page Cache friendly (static feed mode)

See `docs/cloudflare.md` for optional edge cache rules.

---

## Security Highlights

- Item-level ACL for console and media endpoints
- CSRF token on administrator JSON actions
- `no-store` responses for console/media
- Post HTML filtered with the acting user’s Joomla text filters
- Escaped reader-facing output from layouts
- JSON encode/decode paths use `JSON_THROW_ON_ERROR` where applicable

---

## Compatibility

Supported:

- Joomla 6.x
- PHP 8.3+
- Joomla native update system

Not supported:

- Joomla 3 / 4 / 5
- PHP 8.2 and earlier

---

## Current Version

**1.1.0** — first public release

---

## Changelog Highlights (1.1.0)

### Added

- Live Console, shortcode embed, static CDN feeds, End & Convert
- Media upload/browse, editors-xtd insert button, scheduled trash purge
- Admin dashboard / list headers, 15 locales, GitHub update metadata

### Fixed

- Go Live sync race, JED update-server / JAMSS embed noise
- Uninstall feed cleanup, JSON hardening, list language messages

See [`changelog.xml`](changelog.xml) for the public package history.

---

## Production Recommendations

- Prefer **static** feed mode on Cloudflare Free/Pro
- Enable Cloudflare purge of the feed URL when possible
- Keep poll interval at or above your edge TTL
- Create the Scheduled Task for trashed-post purge when soft-deletes accumulate

---

## Author

Kostas Stathopoulos  
DevArt

https://devart.gr

GitHub Repository:

https://github.com/devartgr/joomla-devart-liveblog

---

## License

GNU General Public License version 3 or later.
