---
vulnerability: BAC
platform: BugForge
difficulty: Easy
date: 2025-11-14
---
# Lab: Broken Access Control via Unrestricted Stats Modification

**Date:**2025-11-14
**Platform:**BugForge.io
**Difficulty:**Easy
**Vulnerability:**Broken Access Control

## Key Steps
1.Discovered the /api/stats endpoint through reconnaissance
2.Identified it accepted both GET and PUT methods
3.Successfully modified statistics data without proper authorization checks
4.The endpoint allowed updating any user's stats despite lacking permissions

## Payload
Content-Type: application/json
{
  "total_sessions": 999,
  "best_wpm": 999,
  "avg_wpm": 999
}

## Lesson Learned
Never trust client-side controls for authorization. Even simple endpoints like statistics updates must verify the authenticated user has permission to modify the requested data. Server-side authorization checks should validate both authentication AND permissions for every state-modifying operation.