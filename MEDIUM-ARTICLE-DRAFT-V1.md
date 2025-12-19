

---

## 1. Title

# How I Used SonarQube to Analyze DVWA and Find Real Coding Issues (Beginner-Friendly Guide)

---

## 2. Introduction / Abstract 

If you’ve ever wondered how developers catch bugs and vulnerabilities before they become serious problems, you’re not alone. When I first started learning cybersecurity, I used to think code review was something only senior developers or huge companies did. But after running my first code scan using SonarQube, I realized that even beginners can use powerful tools to find real issues hidden inside code.

For this article, I decided to analyze the source code of DVWA (Damn Vulnerable Web Application) an intentionally insecure training application used in cybersecurity classes. By connecting DVWA’s codebase to SonarQube using SonarScanner, I was able to scan hundreds of lines of code and see exactly what kinds of mistakes developers make without realizing it.

In this Medium article, I’ll walk you through the entire process: setting up Docker, installing SonarQube, running a scan, and reviewing the results. I’ll also explain one very simple but important issue I found inside DVWA’s JavaScript code, an issue many real developers make when they’re not paying attention.

Whether you’re a cybersecurity student like me or someone curious about code analysis, this article will show you how easy and useful it is to review code with modern tools.

---

## 3. Purpose and Background 

When I chose SonarQube for my CSN190 project, my goal wasn’t to become an expert in software development—I wanted to understand how code scanning tools actually detect problems. Code review is one of the most important skills in cybersecurity because insecure code is one of the biggest reasons security breaches happen.

**SonarQube** is a static analysis platform created by SonarSource. It scans code for:
- Bugs
- Vulnerabilities
- Code smells
- Security hotspots
- Duplicated code
- Maintainability issues

It works with many programming languages and is used by professional developers, DevOps teams, and cybersecurity analysts to maintain clean, secure code.

I chose DVWA as my test application because it contains many intentional flaws meant for training. This made it a perfect project for analyzing what mistakes look like in the real world.

What I hoped to learn:
- How SonarQube reads and evaluates code
- What common mistakes look like in real files
- How the scanner reports issues
- How developers can improve their code using these insights

Before this project, I honestly thought this would be a complicated setup. But Docker made it surprisingly easy to run SonarQube locally, and SonarScanner handled most of the work. 
What surprised me most was that SonarQube didn’t just find hacks it found everyday coding mistakes that beginners like me make too. The issue I focus on later in this article is a simple JavaScript mistake involving variable declaration. Even though it’s small, it demonstrates why clear and clean coding practices matter.

---


## 4. Installation and Setup Tutorial 

### **Prerequisites**
To follow along, you need:
- Windows, macOS, or Linux
- Docker Desktop installed and running
- VS Code 
- Git installed

### Step 1: Clone the DVWA Repository
Open VS Code and run:
```
git clone https://github.com/digininja/DVWA.git
```

[Screenshot: DVWA folder visible in VS Code Explorer sidebar — showing index.php, config, js, and other DVWA files]

### Step 2: Install and Start SonarQube Using Docker
In your terminal:
```
docker run -d --name sonarqube -p 9000:9000 sonarqube
```

<img width="1049" height="235" alt="Sonnar_image_pulling" src="https://github.com/user-attachments/assets/5bf617e7-9a57-4d34-a6e4-22b50756e7ca" />


Visit SonarQube at:
```
http://localhost:9000
```
Login:
```
username: admin
password: admin
```

### Step 3: Install SonarScanner
Download from the official website and add the bin folder to your system PATH.

Check installation:
```
sonar-scanner --version
```

<img width="1440" height="1020" alt="Sonnar_version" src="https://github.com/user-attachments/assets/17b638cb-7a66-46dc-a92f-3c864ffb3883" />


### Step 4: Create a Project in SonarQube
Before scanning, SonarQube requires a project to be created.

1. Open SonarQube in your browser:
```
http://localhost:9000
```
2. Click **Projects** → **Create Project**.
3. Choose **Create a local project**.
4. Enter:
   - **Project Key:** dvwa
   - **Project Name:** dvwa
5. Click **Create Project**.
6. When asked how you want to analyze the project, click **Locally**.
7. Click **Other (for Go, PHP, …)**.
8. Copy the *exact* SonarScanner command SonarQube generates for you.

[Screenshot: SonarQube showing project setup]

### Step 5: Run the Scan on DVWA
Make sure your terminal is inside the DVWA folder:
```
cd DVWA
```

Paste the command SonarQube generated. It will look similar to this:
```
sonar-scanner -D"sonar.projectKey=dvwa" -D"sonar.sources=." -D"sonar.host.url=http://localhost:9000" -D"sonar.token=YOUR_TOKEN_HERE"
```

This command:
- connects DVWA to your SonarQube instance
- uploads all source files
- triggers the analysis process

<img width="1468" height="1020" alt="Screenshot 2025-12-03 213118" src="https://github.com/user-attachments/assets/e0d8fdab-5900-417d-86f6-cc2f3be671e9" />


After the scan finishes, go back to SonarQube and open your project.


With the setup complete, the next natural step is to actually use the tool and see what SonarQube finds inside DVWA.

## 5. Using the Software – Practical Example 

Instead of focusing on everything SonarQube found, I picked one issue that was simple and perfect for learning: a JavaScript variable declared incorrectly.

### The Issue I Found
File scanned:
```
dvwa/js/dvwaPage.js
```

SonarQube flagged this line:
```
day = new Date();
```

### Why SonarQube Flagged It
SonarQube labeled this as a **Maintainability Issue** because the variable `day` is created **without** using:
- `let`
- `const`
- or `var`

Without these keywords, JavaScript treats the variable as a **global variable**, which can:
- cause hidden bugs
- override variables accidentally
- make the code harder to understand

### How to Fix It
A simple fix:
```
let day = new Date();
```

or, if it never changes:
```
const day = new Date();
```

### What This Means for Beginners
This issue shows that not all vulnerabilities are about hackers. Some are about **sloppy code** that causes unexpected behavior. Clean code = fewer bugs = fewer security risks.

[Screenshot: SonarQube issue panel highlighting the JavaScript variable declaration problem — showing severity level, rule description, and suggested fix]

---

To put my findings into context, I reviewed industry resources that explain why these issues matter.

## 6. Research Insights 
Understanding *why* SonarQube flagged my issue required looking beyond the scan results and connecting them to real-world secure coding practices. To do that, I reviewed two reliable sources: **SonarSource’s official static analysis guidance** and the **OWASP Secure Coding Practices Checklist**. Both gave me a clearer understanding of why a missing variable declaration, even though small, truly matters.

### Source 1: SonarSource – Why Small Coding Mistakes Matter
The SonarSource documentation explains one of the core ideas behind static analysis: **clean, intentional code leads to more secure applications**. Even when a mistake doesn’t look like a “vulnerability,” it can still introduce unpredictable behavior, and unpredictability is the enemy of security.

One concept that stood out is how implicitly created global variables—like the `day` variable in my DVWA example—can leak into other parts of a program. This can cause unintended overrides, conflicts, or logic errors. SonarSource stresses that these maintainability issues often turn into real vulnerabilities later when developers build new features on top of messy code.

**Key takeaway:** Even small mistakes compound over time. Static analysis helps catch them early.

###Source 2: OWASP Secure Coding Practices – Variable Scope and Predictability
The OWASP Secure Coding Practices guide highlights a similar idea: **global variables are risky**. According to OWASP, secure coding is not only about preventing attacks, but also about avoiding design patterns that make code harder to maintain, reuse, or secure.

OWASP explains that uncontrolled global state increases the chance of bugs and unexpected interactions—exactly the kind of issue SonarQube detected in DVWA. Even though forgetting a `let` or `const` isn’t a direct security exploit, OWASP shows how such mistakes weaken the overall reliability of the application.

**Key takeaway:** Predictable code is secure code. Avoiding accidental globals is a basic part of secure practice.

### How These Sources Deepened My Understanding
Before researching, I thought the missing variable declaration SonarQube flagged was just a tiny style issue. After reading SonarSource and OWASP, I understood that tools like SonarQube are teaching developers to think long-term. The goal isn’t only to stop hackers—it’s to write code that behaves exactly as intended.

This connection between theory and practice made the scan results more meaningful. Instead of seeing SonarQube as a “mistake detector,” I began to see it as a teaching tool that helps beginners like me learn professional coding habits.

---

## 7. Challenges and Problem-Solving 
No technical project goes perfectly the first time, and this one definitely tested my patience, problem‑solving skills, and confidence. Looking back, the challenges were actually the most valuable part of the experience because they taught me how real developers troubleshoot in the moment.

The first major challenge was the **SonarQube Docker download**. The image is huge, and watching it crawl from a few megabytes to several hundred felt endless. At one point, I genuinely thought something was broken. I felt impatient and frustrated, especially because I didn’t want to waste time. Eventually I learned that the slow download was normal and that sometimes the solution is simply giving tools time to finish. This taught me the importance of patience and understanding how large systems behave.

The second challenge came when **SonarScanner kept failing** with a message saying the project did not exist. At first, I was confused and thought I installed it incorrectly. I felt stuck because the error wasn’t very clear. After re‑reading the steps and experimenting, I realized that SonarQube requires a project to be created *before* scanning. Once I created the project, selected **“Locally”**, chose **“Other (for Go, PHP…)”**, and copied the exact generated command, everything finally worked. This moment taught me how important it is to follow the workflow in the right order.

Another challenge involved **authentication tokens**. SonarScanner refused to run until I supplied the correct token linked to my project. I felt confused at first, but after carefully checking the documentation and trying again, I understood how tokens authenticate scans.

By the end, each challenge made me more confident. I learned that frustration is part of the learning process, and solving problems one step at a time is what truly builds skill in cybersecurity.

---

## 8. Conclusion and Future Applications. Conclusion and Future Applications. Conclusion and Future Applications

This project helped me understand how powerful code review tools are. SonarQube showed me that even simple mistakes can have big effects. I learned how to set up tools, run scans, and understand reports.

In the future, I want to explore:
- scanning Python projects
- using SonarCloud
- trying other secure coding tools

---

## 9. Resources and Links
Below are the core resources that supported this project. Instead of overwhelming the reader with too many citations, this list focuses on the essential tools and documentation someone would actually need to repeat the steps.

### Project Resources
- **DVWA (Damn Vulnerable Web Application)** – Official GitHub repository used for scanning and testing.
  https://github.com/digininja/DVWA

- **SonarQube Community Edition** – Local code analysis platform used to review DVWA.
  https://www.sonarqube.org

- **SonarScanner CLI** – Tool used to upload the DVWA source code to SonarQube for analysis.
  https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/scanners/sonarscanner/

### Learning & Reference Materials
- **Basic SonarQube Setup Guide (Official Docs)** – Helped with initial configuration and understanding how local analysis works.
  https://docs.sonarsource.com

- **OWASP Secure Coding Practices Checklist** – Reinforced why global variables and poor coding habits matter.
  https://owasp.org/www-project-secure-coding-practices/

### Tools Used in This Project
- **Docker Desktop** – Used to run SonarQube locally.
- **Visual Studio Code** – Used as the main development/editor environment.
- **Windows Terminal / PowerShell** – Used to run scanner commands and work inside the DVWA folder.

These resources allow any beginner to follow the same steps without confusion or unnecessary complexity.

---

# **END OF DRAFT**
