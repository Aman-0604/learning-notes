---
title: Answers Framework
nav_order: 3
parent: Posts
---

# Interview Answers Framework

Jotting down some important frameworks to answer interview questions.

## For Introduction:

Most students think "Tell me about yourself" is about their life story. It's not.

What 95% of candidates do wrong: They repeat their resume word-for-word.
> "***Hi, I'm ABC. I did BTech from XYZ college. I know Java, Python, C++. I made a blockchain project.***"

Interviewer's reaction: "***I already read your resume. What's new here?***"

What actually works: The **PARL Framework** I developed:
- Personal Background (relevant only)
- Academic Achievements (specific, not generic)
- Relevant Skills & Projects (with real impact)
- Long-term Vision (aligned with company goals)

**Example of a winning introduction:** 
> "***I'm passionate about solving complex problems, which drew me to computer science. At XYZ Institute, I ranked top 5% and specialized in ML algorithms. Using MERN stack, I built a resource-sharing platform with 500+ active users, implementing JWT authentication and real-time notifications. I'm excited about cloud architecture and see this role as perfect for contributing to your microservices work.***"

## For HR Round: 

Answer every question in STAR Framework, i.e first layout the situation then the tasks you performed, then the actions you took and finally the result you got. Try to provide real life examples.

**Sample Interview Question: Can you describe a situation where you faced a significant challenge during the development of DeCyber(project name) and how you resolved it?**

**Situation**: During the development of DeCyber, we encountered a challenge related to real-time data interactions and synchronization between players. The multiplayer nature of the game required seamless communication and instant updates to ensure a smooth gaming experience.

**Task**: My task was to implement real-time data interactions using web sockets to ensure that all players could see the changes in the game state simultaneously.

**Action**: To tackle this challenge, I decided to integrate Socket.io, a widely-used library for real-time communication in web applications. I set up a Socket.io server on the Node.js backend and established a connection between the server and the clients. This allowed us to broadcast updates whenever a player captured a country or when a new code was generated.

**Result**: By using Socket.io, I successfully implemented real-time updates, ensuring that all players received immediate feedback on the game's progress. This enhanced the overall gaming experience and created a sense of engagement and competition among players.

> In the last you can also share your learnings. (Optional)

## For Coding Round:

Steps:
1. Read question loud
2. Explain 1 example loud
3. Can you tell me what to return if this edge case occurs? (or any other question)
4. Brute force (explain T.C and S.C)
5. More optimal (explain T.C and S.C)
6. Most optimal (explain T.C and S.C)
7. Code only the most optimal solution

## For System Design Round: 

Steps:
1. Use case diagram - Jot down all the actors, and their activities. This helps in storing all the requirements at one place with clear roles of everyone. 
2. Class Diagram - Writing down all the data members and functions of each object. It also helps in establishing relationships among objects. 
3. Discussing the design pattern - for eg. if we need only 1 instance of 'system' then we will be using singleton desing pattern.
4. Coding - code the class diagram as it is

> Think 'system' as the backend and it's functions as exposed api's, and customer as the client side or the frontend for simplicity

> Machine Coding Round - you have to run the code, but in LLD Round - you have to just write the pseudo code

> To solve concurrency problem - use make functions boolean

> To solve race conditions - use locking machenism to synchronize (senior sde interview question)