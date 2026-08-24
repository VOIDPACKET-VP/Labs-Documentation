---
layout: layouts/entry-detail.njk
title: HTB — Cap
date: 2026-08-21
category: Web
platform: HackTheBox
difficulty: Easy
tags:
  - IDOR
  - Linux
  - PrivEsc
summary: One-line summary shown in the listing.
backLink: /writeups/
backLabel: Writeups
---
# About This Box
Cap is an easy difficulty Linux machine running an HTTP server that performs administrative functions including performing network captures. Improper controls result in Insecure Direct Object Reference (IDOR) giving access to another user's capture. The capture contains plaintext credentials and can be used to gain foothold. A Linux capability is then leveraged to escalate to root.


# Let's start
