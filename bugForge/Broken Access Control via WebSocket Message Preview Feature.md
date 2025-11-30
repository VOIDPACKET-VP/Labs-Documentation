---
vulnerability: Web Sockets
platform: BugForge
difficulty: Medium
date: 2025-11-24
---
# Lab: Broken Access Control via WebSocket Message Preview Feature

- Date: 2025-11-24
- Platform: BugForge
- Difficulty: Medium
- Vulnerability: Broken Access Control via WebSocket Message Preview Feature

## Key Steps
1. **Reconnaissance**: Discovered REST API endpoints (`/api/messages`, `/api/users`) and WebSocket (Socket.IO) implementation
2. **Initial Testing**: Confirmed proper access control on main message endpoints - `GET /api/messages/{id}` returned proper authorization errors
3. **WebSocket Analysis**: Observed real-time message notifications and preview functionality
4. **Vulnerability Discovery**: Found that WebSocket `preview-message` event lacked access control checks
5. **Exploitation**: Requested message previews for unauthorized message IDs via WebSocket
6. **Flag Extraction**: Retrieved flag from admin's message preview (ID 1)

## Vulnerable Endpoint
- **WebSocket Event:**
```Socket.IO Connection → 42["preview-message", MESSAGE_ID]```
- **Response Channel:**
```42["message-preview", {"messageId": ID, "preview": "MESSAGE_CONTENT"}]```

## Exploitation Payload
```
// Via Browser Dev Tools Console
socket.emit('preview-message', 1);

// Via Raw WebSocket Message
42["preview-message",1]
```

## Payload Breakdown
- 42 = Socket.IO message packet type (event)
- ["preview-message", 1] = Event name and parameter (message ID to preview)
- The server processes this without verifying user authorization for the requested message
- Returns preview content for ANY message ID regardless of ownership

## Lesson Learned
- Inconsistent Security Models: REST API had proper access control, but WebSocket events were inadequately protected
- Preview Features Are Risky: "Convenience" features like message previews often have weaker security
- WebSocket Testing Gap: Traditional API testing methodologies don't cover real-time communication vulnerabilities
- Stateful Protocol Challenges: WebSockets require different testing approaches than stateless REST APIs

## Remediation
- **Implement Access Control on ALL Events**:
    // Server-side validation needed
    socket.on('preview-message', (messageId) => {
    if (!canUserAccessMessage(socket.userId, messageId)) {
        return socket.emit('error', 'Unauthorized');
    }
    // ... proceed with preview logic
    });
- **Consistent Authorization Layer**: Apply same access control rules to WebSocket events as REST endpoints
- **Input Validation**: Validate message ID ownership before processing preview requests
- **Security Testing**: Include WebSocket events in penetration testing scope and automated security scans