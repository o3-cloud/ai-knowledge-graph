---
summary: R&D+Product - AI Adoption Feedback Session discussing team experiences with Claude and Gemini for development tasks, including code analysis, testing, and prototyping
event_type: meeting
sources:
    - https://docs.zoom.us/doc/jp8Jc3M6QvuCQbBPasOEtA
    - https://us06web.zoom.us/user/meeting/summary?ampDeviceId=8103557d-921c-4088-b759-a7c181f0a73c&ampSessionId=1766078514650
tags:
    - AI
    - adoption
    - feedback
    - Claude
    - Gemini
    - development
    - testing
    - prototyping
---

# R&D+Product - AI Adoption Feedback Session

## Quick Recap

The team discussed various experiences and challenges with AI tools like Claude and Gemini for development tasks, including code analysis, testing, and prototyping, while highlighting both their benefits and limitations. Team members shared their specific use cases and experiences with different AI tools across different technical areas, including database maintenance, testing frameworks, and code generation, with discussions around the need for human oversight and verification. The conversation ended with reflections on AI's role as a supportive tool rather than a replacement for human judgment, and plans for an upcoming unconference to further explore AI applications.

## Key Discussion Areas

### Query Performance and Team Updates
Tyler shared his experience of improving query performance by running explain on the server after an upgrade, which resulted in a significant improvement in Federator query performance. Joshua and Tyler discussed the differences in database maintenance practices between SQL Server and their current system. The team welcomed Mateusz, a new team member from Code Concept in Poland, and discussed his introduction to the team and the challenges of certain projects like Iguana and Analytics work.

### AI Tools: Experiences and Challenges
The team discussed their experiences with AI tools, particularly Claude, focusing on code analysis, unit testing, and automation. Tomasz shared his positive experience with code review and unit testing, noting the Polish language's effectiveness for AI prompts. Szymon highlighted AI's role in discovering new technologies and its ability to streamline learning processes, though he noted a lack of creativity as a challenge.

### AI for Product Specification
Nick shared his experience using AI for product specifications, finding it helpful for organizing complex scenarios and creating prototypes, but noted challenges with unexpected UI changes. Joshua mentioned difficulties in generating realistic data with AI, especially for text fields, and Henry suggested using range limits to improve accuracy.

### AI Prototyping Challenges
The team discussed the limitations and challenges of using AI models for coding and prototyping, particularly focusing on context retention and the difficulty of managing long conversations. Strategies discussed include keeping discussions brief, resetting the session to clear context, and using external libraries to structure conversations.

### Testing and Validation
Joshua shared his experience with using an AI tool for testing, noting that it struggled with integration tests and was overly enthusiastic about making changes, emphasizing the need for user oversight. Harpreet highlighted the use of Gemini for testing edge cases and finding bugs. Santhosh discussed using Gemini for test planning and design, creating Excel outputs for Jira.

### Development Practice Insights
The team agreed that AI should be used as a support tool, not a replacement for human judgment. Common themes included the need for verification of AI suggestions, limitations with complex tasks like CSS and regex, and the importance of slower, more deliberate prompting for better results.

## Next Steps

- **Manny**: Take notes from the meeting and identify themes from AI feedback
- **Sarah**: Help Owen schedule and coordinate the UN-conference in January
- **Owen**: Lead the UN-conference in January focused on AI collaboration and learning
- **Sarah**: Recruit volunteers to help arrange and moderate sessions for the UN-conference
- **Matt**: Look at setting up shared configuration like clod.md in repos and how to share projects in Claude
- **Henry**: Start specifying libraries when creating prototypes with AI to match what the team can actually implement
- **Sami**: Investigate Visual Studio 2022 update for Claude integration or explore moving to VS Code for C-sharp development
- **Mateusz**: Help Sami with Claude integration in Visual Studio if needed by January
