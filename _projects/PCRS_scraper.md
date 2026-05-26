---
layout: page
title: PCRS Scraper
description: Multithreaded scraper for UofT course materials with a desktop GUI and session management
img: assets/img/PCRS_scraper.png
importance: 5
category: projects
related_publications: false
---

PCRS is the course platform used at the University of Toronto for CS courses. It holds lecture videos, code examples, and practice problems, but has no export or offline access feature. This tool scrapes a course and outputs a single interleaved markdown file that matches the original page layout, with videos, code, and questions in the same order they appear on PCRS.

<div style="text-align: center; margin: 1.5rem 0;">
  <img src="/assets/img/PCRS_scraper.png" alt="PCRS Scraper desktop GUI showing progress log" style="max-width: 680px; width: 100%;">
</div>

The tricky part of PCRS authentication is that it sits behind UofT's Shibboleth SSO, so there is no simple username/password login to automate. The scraper authenticates using a session cookie exported from your browser. The GUI has a Quick Import button that accepts a raw JSON cookie export from any browser extension, automatically finds the Shibboleth session token, and saves it to a `.env` file so you only have to do it once per session.

Scraping runs in a thread pool so multiple pages are fetched in parallel, which makes a noticeable difference on longer courses. A separate button generates a compiled study guide from all the scraped content. The week selector lets you target a specific week rather than pulling everything down at once.

[View on GitHub](https://github.com/daniel-halpern/PCRS-scraper)
