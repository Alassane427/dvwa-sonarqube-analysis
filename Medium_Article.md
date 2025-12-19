# How I Used SonarQube to Analyze DVWA: A Beginner-Friendly Walkthrough
<img width="1000" height="667" alt="image" src="https://github.com/user-attachments/assets/75b44364-ee42-4ab1-a070-111561221ed3" />

When I started this project, I wanted real experience with a tool that professionals actually use to find security flaws in applications. Instead of just reading about vulnerabilities, I wanted to see them - what they look like inside code, how they're detected, and how the scanning process works.

To do that, I used two well known tools:  
**DVWA (Damn Vulnerable Web Application)** - an intentionally insecure web app made for learning  
**SonarQube** - a static analysis platform used by companies to identify bugs, vulnerabilities, and code quality issues

**My goal was simple:**  
Run SonarQube against DVWA, analyze the results, and learn how real-world security scanning works.

This walkthrough explains exactly how I set things up, what SonarQube found, the mistakes I made along the way, and what I learned from troubleshooting everything myself.

---

## Setting Up DVWA and SonarQube Using Docker

Setting up both tools with Docker was the fastest and cleanest way to get everything running. Using containers kept the tools isolated and easy to start or stop at any time. Even though this setup sounds simple, this was the part where I learned the most about managing security tools.

---

## Starting DVWA

DVWA is built specifically for cybersecurity practice. After pulling the DVWA Docker image, the container launched immediately, and I could access the vulnerable application through my browser.
<img width="960" height="1020" alt="image" src="https://github.com/user-attachments/assets/d336c2a4-20c3-482d-a1a4-dabc4cda325e" />

DVWA gave me a controlled environment full of intentional vulnerabilities perfect for learning.

---

## Starting SonarQube in Docker

SonarQube was more demanding. The Docker image took a long time to download, and at first, I thought something was wrong. Eventually, the container finished installing, and I accessed the SonarQube dashboard in my browser.
<img width="1000" height="531" alt="image" src="https://github.com/user-attachments/assets/7d550228-e201-49ba-911b-c126185c843c" />

Seeing SonarQube load in the browser felt like a big milestone because this is a tool used in real DevSecOps pipelines.

---

## Running the SonarScanner

Once DVWA and SonarQube were running, it was time to scan the DVWA code using SonarScanner, a command-line tool that sends code to SonarQube for analysis. This step taught me a lot about how SonarQube is structured and how scanners communicate with analysis servers.

---

## Creating a SonarQube Project

My first scanner attempts failed because SonarQube requires a project before any scans can be uploaded. After figuring this out, I:

- Logged into the SonarQube dashboard  
- Clicked **"Create Project"**  
- Named my project (e.g., `dvwa-analysis`)  
- Generated an authentication token  

The token is what allows the scanner to authenticate securely.
<img width="1000" height="663" alt="image" src="https://github.com/user-attachments/assets/dd00b804-33ae-4308-8886-82ebc127a2e1" />

---

## Running the Scan

With everything set up, I ran the scanner command again. This time, it began indexing and analyzing the DVWA code:

- recognizing files  
- applying security rules  
- uploading results to the dashboard  
<img width="1000" height="695" alt="image" src="https://github.com/user-attachments/assets/82ab77f4-d1f2-4d24-9be6-fae4f061f0cf" />

Seeing the scan succeed helped me understand how the pieces fit together.

---

## What SonarQube Found in DVWA

After the scan completed, the SonarQube dashboard displayed a list of issues.

One issue stood out right away:

### **JavaScript Variable Used Without Declaration**

SonarQube flagged the variable **day**, which was used without `let`, `const`, or `var`.

### Why this matters:

- JavaScript automatically creates an unintended global variable  
- Global variables can be overwritten by other scripts  
- They can cause unpredictable behavior  
- They make debugging much harder  
- In larger apps, this leads to real security and stability problems  

This helped me understand how simple coding habits can create deeper issues.
<img width="1000" height="513" alt="image" src="https://github.com/user-attachments/assets/a55449ce-6d5f-4f8e-a73e-b2d4902db8a8" />

SonarQube also categorized additional findings into:

- **Security Hotspots**  
- **Code Smells**  
- **Bugs**

This taught me the differences between maintainability issues and actual security vulnerabilities.

---

## Challenges I Faced (And What They Taught Me)

This project wasn't perfect, and I ran into multiple challenges. Each one ended up teaching me something valuable about how real-world tools behave.

---

### 1. Extremely Slow SonarQube Download

The Docker image took so long to download that I thought something was wrong.

**What I learned:**  
Large enterprise tools require patience, and slow downloads don't always mean errors.

---

### 2. Scanner Failed Repeatedly

My first scans kept failing because I hadn't created a project in SonarQube yet.

**What I learned:**  
Tools often rely on specific workflows, and understanding the setup order is important.
<img width="1000" height="695" alt="image" src="https://github.com/user-attachments/assets/25d13c67-ad58-431b-95bd-6c2b927878c5" />

---

### 3. Confusion About Authentication Tokens

I had never used tokens before, so figuring out how they authenticate the scanner took some research.

**What I learned:**  
Even simple authentication systems require attention to detail. Tokens are widely used in real development pipelines.
<img width="1000" height="662" alt="image" src="https://github.com/user-attachments/assets/1a4cfb4c-4c94-44b6-81b8-3c168f6e18f3" />

---

## What I Learned

This project gave me a clearer understanding of how cybersecurity and software development overlap.

- **Static analysis is extremely powerful.**  
  SonarQube detects vulnerabilities and coding issues that are easy to overlook.

- **Small coding mistakes can lead to real issues.**  
  The undeclared variable showed how something tiny can create bigger problems later.

- **Troubleshooting is part of the learning process.**  
  Tools don't always work on the first try. Fixing errors taught me how these systems behave.

- **Professional tools require proper setup.**  
  SonarQube is not a lightweight tool, but once configured, it provides valuable analysis.

---

## Conclusion

This project gave me hands-on experience using a real static analysis tool to examine insecure code. Scanning DVWA with SonarQube helped me understand how vulnerabilities are detected, how issues are categorized, and how developers use automated tools to improve security.

Most importantly, it showed me that learning cybersecurity is a process of experimenting, breaking things, fixing them, and understanding how everything connects.

This experience made me more confident working with professional tools and deepened my understanding of secure coding practices.

---

## Resources

DVWA GitHub: https://github.com/digininja/DVWA  
SonarQube: https://www.sonarsource.com/products/sonarqube/  
SonarQube Documentation: https://docs.sonarqube.org  
SonarScanner Guide:  
https://docs.sonarqube.org/latest/analyzing-source-code/scanners/sonarscanner/  
Docker: https://www.docker.com
