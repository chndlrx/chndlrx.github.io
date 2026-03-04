---
title: "OffSec Web Expert (OSWE) Review"
date: 2026-03-04 00:00:00 -0500
categories: [hacking]
tags: [certification]
image:
  path: /assets/img/posts/oswe-review/oswe.png
  alt: OffSec (Offensive Security) OSWE WEB-300 Certification Exam Write-up
---
## Introduction
What's up everyone. I recently earned my [OSWE (OffSec Web Expert) Certification](https://www.offsec.com/courses/web-300/) and wanted to share my experience with the WEB-300 course and the 48-hour exam. Before I get into it, I think it's helpful to share a bit about where I was coming in so you can gauge how this might apply to you.

### My Background Going In
I came into OSWE as a working Penetration Tester with certifications including OSCP, BSCP, and GWAPT. I spend most of my professional time assessing web applications, so I was already comfortable with common vulnerability classes and had very strong experience with black box testing. I also lead the [OWASP Knoxville](https://owasp.org/www-chapter-knoxville/) chapter, where we regularly discuss application security topics. That said, I had no background in software development, so there were times where it felt pretty difficult performing static and dynamic source code analysis. Several vulnerabilities will require finding hidden functionality by tracing execution paths, identifying subtle logic flaws, and chaining multiple vulnerabilities into a full exploit.

## Course Overview
WEB-300 (Advanced Web Attacks and Exploitation) is OffSec's course for their OSWE certification. It's designed for experienced security professionals who want to develop deep white box web application testing skills. The course walks you through real-world case studies, each centered around a vulnerable application where you analyze source code, identify flaws, and develop working exploits.

The course explores a broad range of security vulnerabilities, including injection attacks, deserialization flaws, CSRF, SSRF, insecure cryptography, session hijacking, WebSocket exploitation, and other common web application weaknesses. Students are expected to possess a solid foundational understanding of these topics prior to participation, as they will be required to apply this knowledge in advanced, multifaceted scenarios. These scenarios often involve navigating around filters, safeguards, and various defensive mechanisms. For more specific details on course material, view the [OffSec (Offensive Security) OSWE AWAE (Advanced Web Application Exploitation) WEB-300 Course Syllabus](https://www.offsec.com/documentation/awae-syllabus.pdf).


### What Makes It Different
Unlike a lot of security courses that lean on automated tools, WEB-300 is almost entirely manual. You're reading code, tracing logic, and building custom proof-of-concept exploits by hand. There's no running a scanner and hoping for the best. The course forces you to think like a developer and an attacker at the same time. Additionally, learning never stops at a basic proof-of-concept (PoC). All labs leverage discovered vulnerabilities for maximum impact, whether that be bypassing authentication, getting administrative access, or achieving RCE. This course brings the classic OffSec **#tryharder** mentality.

## Course Insight

### Getting Started
The first couple modules hit hard. There's a steep initial learning curve, especially if you haven't done much source code review before. The early case studies throw a lot of technical detail at you quickly. Be prepared to drink from the fire hose.  
![Drinking From Fire Hose](/assets/img/posts/oswe-review/fire-hose.svg)  
Once I got past that initial ramp-up, the material became much more manageable. The course does a good job at showcasing different methodologies in each lab. This is because there isn't a best methodology to follow in the white box testing world. Once you start recognizing patterns in how vulnerabilities appear in code, the process of tracing sources and sinks becomes more natural.

### Real Vulnerable Applications
One aspect I loved about the course is that real open-source applications are used throughout the case studies. You're not exploiting some deliberately vulnerable app that was built to be broken. You're analyzing actual software with actual CVEs. This makes the learning feel immediately applicable to real-world engagements. You get to see how these vulnerabilities were discovered in practice, trace the flawed logic through legitimate codebases, and understand how subtle implementation mistakes become fully exploitable under the right conditions. It bridges the gap between course work and client work in a way that most training doesn't. These applications also open doors to awesome supplementary research you can perform to better understand the discovered vulnerabilities, and even more that are not covered in the course. Finding other vulnerabilities in the provided applications will tremendously help improve your white box skills.


### Exploit Scripting
Another recommendation is writing your exploit scripts from scratch rather than copying from the course material. The exam requires fully automated exploit scripts with zero manual interaction, and you want that muscle memory built up well before exam day. Additionally, several of the labs do not require you to develop exploit scripts. It would be in your best interest to get the reps during training to ensure your exam scripts are less stressful to write.

## The OSWE Exam
![Boxing Ring - OffSec OSWE Certification Exam](/assets/img/posts/oswe-review/boxing-ring.svg)  
The OSWE exam is a 47-hour and 45-minute practical assessment, followed by an additional 24 hours to submit a professional penetration test report. It is remotely proctored for the entire duration.

### Scoring Breakdown
- **35 points** for each successful authentication bypass (two applications).
- **15 points** for each successful RCE (two applications).
- **85 points** required to pass.
- All exploit scripts must be fully automated with **zero user interaction**.
- A detailed, professional-grade report must be submitted documenting everything.

The automation requirement really separates OSWE from a lot of other practical exams. It's not enough to demonstrate exploitation manually — your scripts need to reproduce the full attack chain from start to finish, hands-off.

For official and up-to-date exam requirements, check the [OSWE Exam Guide](https://help.offsec.com/hc/en-us/articles/360046869951-WEB-300-Advanced-Web-Attacks-and-Exploitation-OSWE-Exam-Guide).

## Exam Experience

### Overview
My exam started at 11:00 AM and I obtained all 100 points with fully functional exploitation scripts in 38 hours. Both applications had a smaller codebase than what I was used to from the course material labs which made pinpointing vulnerabilities much more manageable.

Upon finding vulnerabilities, there was often an attempt at sanitizing dangerous user input, but it fell short. In my opinion, exploiting the vulnerabilities was moderately difficult. Finding the correct bypass was generally not too difficult. Scripting the exploit chains is what took the most time and what I found to be the most difficult. Once I had the scripts complete, I reverted both applications multiple times to ensure that both scripts run through the authentication bypass and RCE successfully without any errors or user interaction.

### Exam Approach
While taking the exam, this was my general approach:

1. **Black box enumeration first**: Interact with the application before diving into source code. Self-register an account if possible, and walk the application until all low-privilege functionality has been discovered.
2. **Threat modeling**: Identify potential attack surface, input fields, and interesting functionality. Think about abuse case scenarios.
3. **Targeted code review**: Dig into the source code focusing on functions already identified. This kept the review focused instead of aimlessly reading thousands of lines of code.
4. **Validate on the debug instance**: Test assumptions against the debug version of the application before going after the target. Use debugging and database logging to better understand how user input impacts targeted functions.
5. **Research filter bypass techniques**: Found a vulnerability but cannot exploit it? It may just be a flimsy wall trying to stop you. Research the mechanism that is stopping you and identify if it can be bypassed.
6. **Repeat**: Got through the authentication mechanism? Time to find a way to get RCE. Use the admin account to look for new features, perform threat modeling, and targeted code review. This approach may not always work, but it is a great place to start.

### Evidence
![Camera - Screenshots for Reporting](/assets/img/posts/oswe-review/camera.svg)  
Throughout the exam I took **tons** of screenshots. This was to ensure that I had enough evidence to submit in the report, without allocating time to reporting during the exam window. This worked out really well. Before ending my exam, I also double checked to ensure I had all the evidence needed to move on to reporting.

### Breaks and Mental State

I took a lot of breaks to recuperate. This helped keep the exam relaxed and I even thought of good ideas to try while I was away. Throughout the exam I was fairly relaxed and honestly I was really enjoying everything and having fun with the hacking. I was hoping to get 8 hours of sleep each night, but I was super locked in and had a hard time shutting my brain off. This led to me getting less sleep than I hoped for, but I guess that's just the cost of doing business.

## The Result
After I submitted my report to OffSec, I got the email that I passed only 24 hours later. I was extremely impressed with how fast the exam was graded and how quick I got results back.
![Celebrate - Pass the Certification Exam!](/assets/img/posts/oswe-review/celebrate.svg)  

## Tips for Future OSWE Candidates
Based on my experience, here's what I'd recommend:

1. **Build your code review methodology early.** Don't just read code randomly. Identify sources and sinks, trace execution paths, and build a repeatable process. Your methodology will change on different applications and that is ok. Just be sure to spend time getting comfortable in code review.

2. **Automate from day one.** Every lab, every exercise — write a fully automated exploit script. Don't leave this for exam prep. By exam day, it should be second nature.

3. **Get your boilerplate code ready.** Have templates for common exploit patterns, HTTP request handling, session handling, reverse shell listeners, file uploads, and file hosting. You don't want to be writing boilerplate under pressure.

4. **Take breaks.** Seriously. Step away from the screen when you're stuck. Some of my biggest breakthroughs came right after a short walk or a reset.

5. **Read the code carefully.** If something isn't working, the answer is almost always in the source code. Read it again. Then read it one more time.

6. **Document as you go.** Don't save all your screenshots and notes for the end. You'll forget things, and you don't want to be scrambling during the report window.

7. **Supplement with external resources.** PortSwigger Web Security Academy, GitHub prep repos, and Hack The Box machines are all great for filling gaps.

## Final Thoughts
This was an awesome certification from OffSec. It was both more challenging and rewarding than I expected. This is also the first exam that I have had genuine fun with while taking. I would recommend this course to senior security professionals with a strong foundation in web applications. This course would also be great for software engineers since they are the ones often responsible for writing secure code in the first place.

Thanks for reading. If you have questions about OSWE or want to connect, feel free to reach out on [LinkedIn](https://www.linkedin.com/in/johnsonchandler/) or [X](https://x.com/chndlrx).
