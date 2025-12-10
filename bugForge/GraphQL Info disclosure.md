---
vulnerability: Info Disclosure
platform: BugForge
difficulty: Easy
date: 2025-12-10
---

---

# Lab: Ottergram Admin Password Disclosure via GraphQL

## Vulnerability Overview

I found a serious security issue in the Ottergram chat application where the GraphQL API was leaking sensitive information. The problem had two parts: first, the GraphQL system was set up to show its entire structure to anyone who asked (like showing the blueprint of a building to strangers), and second, there was no check to stop people from accessing other users' private data just by changing a number in their request.

## Vulnerable Endpoint

**POST** `/graphql` (The main GraphQL API endpoint)

**How I found it**: While using Burp Suite to watch the traffic, I noticed the app was sending special requests to `/graphql`. These requests looked different from normal API calls - they were asking for specific pieces of data by name. This told me the app was using GraphQL instead of a regular REST API.

## Attack Flow

1. **Finding the GraphQL Endpoint**: I saw in Burp that the app was talking to `/graphql` whenever someone viewed their profile stats.
    
2. **Asking for the Blueprint**: I sent a special GraphQL question that asked "Show me everything you can do." This is called introspection. The server happily replied with a full list, including a `User` type that had a `password` field!
    
3. **Finding Available Actions**: Next, I asked "What specific questions can I ask you?" The server told me I could use two queries: `analytics` (which the app already used) and `user` (which wasn't visible in the normal app).
    
4. **Trying the Hidden Query**: I asked for user information with ID 2 (guessing that might be an admin). The server gave me everything: username, email, password, and role - without asking if I had permission!
    
5. **Getting the Flag**: The password field contained the flag I was looking for.

## Exploitation Payload

**Step 1: Getting the System Blueprint**
		{
		  "query": "query { __schema { types { name fields { name } } } }"
		}
_This asks the GraphQL system: "Show me all the different types of data you have and what information each type contains."_

**Step 2: Finding Available Queries**
		{
		  "query": "{ __schema { queryType { fields { name description } } } }"
		}
_This asks: "What specific questions am I allowed to ask you?" It revealed the hidden `user` query._

**Step 3: Getting Admin Credentials**
		{
		  "query": "query { user(id: 2) { username email password role } }"
		}
_This asks: "Give me the username, email, password, and role for the user with ID number 2."_

## What Happened Behind the Scenes

1. **The GraphQL system was too talkative**: Normally, GraphQL introspection (the "show me your blueprint" feature) should be turned off in production. But here it was left on, so anyone could learn about the `User` type and its `password` field.
    
2. **No permission check**: When I asked for user ID 2's information, the server didn't ask: "Are you allowed to see this?" It just gave me the data because I asked for it nicely.
    
3. **Passwords in plain sight**: The password was stored right in the database field instead of being hidden or encrypted in the API response.

## What I Got Back

When I ran the final query, I received:
	`{
	  `"data": {
	    `"user": {
	      `"username": "admin",
	      `"email": "admin@ottergram.com",
	      "password": "bug{.........}",
	      `"role": "admin"
	    `}
	  `}
	`}

**The Flag**: `bug{........}` was sitting right there in the password field!

## What Went Wrong (In Simple Terms)

1. **Too much information sharing**: The GraphQL API was like an open book - it showed everything it could do to anyone who asked.
    
2. **No bouncer at the door**: There was no security guard checking if you should be allowed to see someone else's private information.
    
3. **Secrets in plain text**: The app was storing and showing passwords without hiding them, which is like writing your password on a sticky note for everyone to see.

## Lesson Learned

1. **Never enable GraphQL introspection in production environments** - Introspection should be disabled or restricted to authenticated administrative users only.
    
2. **Implement proper authorization at the resolver level** - GraphQL queries must validate that the requesting user has permission to access the requested data, not just that the query syntax is valid.
    
3. **Avoid exposing sensitive fields in GraphQL schemas** - Fields like `password` should never be queryable through GraphQL, even with proper authorization.
    
4. **Use allow-lists for queries in production** - Implement query complexity analysis and allow only specific, vetted queries.
    
5. **Implement query depth limiting** - Prevent excessively nested queries that could lead to denial of service or data exfiltration.
