# **How I Used SonarQube to Analyze DVWA: A Beginner-Friendly Walkthrough**

When I started this project, I wanted real experience with a tool that professionals actually use to find security flaws in applications. Instead of just reading about vulnerabilities, I wanted to see them — what they look like inside code, how they're detected, and how the scanning process works.

To do that, I used two well-known tools:

- **DVWA (Damn Vulnerable Web Application)** — an intentionally insecure web app made for learning  
- **SonarQube** — a static analysis platform used to identify bugs, vulnerabilities, and code quality issues  

**Project Goal:**  
Scan DVWA using SonarQube, analyze the results, and understand how real-world security scanning works.

This walkthrough explains step-by-step how I set everything up, what SonarQube found, the mistakes I made, and what I learned.

---

## **Setting Up DVWA and SonarQube Using Docker**

Setting up both tools with Docker was the fastest and cleanest way to get everything running. Using containers kept the tools isolated and easy to start or stop at any time.

---

## **Starting DVWA**

DVWA is built specifically for cybersecurity practice. After pulling the DVWA Docker image, the container launched immediately, and I could access the vulnerable application through my browser.

It provides a controlled environment full of intentional vulnerabilities perfect for learning.

```
[Insert Screenshot: DVWA container running in Docker Desktop]
[Insert Screenshot: DVWA homepage]
```

---

## **Starting SonarQube in Docker**

SonarQube required more resources. The Docker image took a long time to download, and at first, I thought something was wrong. Eventually, the container finished installing, and I accessed the SonarQube dashboard in my browser.

Seeing SonarQube load felt like a major milestone.

```
[Insert Screenshot: SonarQube container running]
[Insert Screenshot: SonarQube dashboard homepage]
```

---

## **Running the SonarScanner**

Once DVWA and SonarQube were both running, the next step was scanning the DVWA code using **SonarScanner**, which sends source code to SonarQube for analysis.

This helped me understand how SonarQube organizes projects, tokens, and scan uploads.

---

## **Creating a SonarQube Project**

My first scanning attempts failed because SonarQube requires a project before accepting any scan uploads.

To fix this, I:

1. Logged into SonarQube  
2. Clicked **“Create Project”**  
3. Named the project (example: `dvwa-analysis`)  
4. Generated an authentication token  

```
[Insert Screenshot: Create Project screen]
[Insert Screenshot: Token creation screen]
```

The token allows the scanner to authenticate securely.

---

## **Running the Scan**

Once everything was configured properly, I ran SonarScanner again. This time it successfully:

- Indexed the DVWA files  
- Applied security rules  
- Uploaded results to the dashboard  

```
[Insert Screenshot: Successful terminal scan output]
```

---

## **What SonarQube Found in DVWA**

After the scan completed, SonarQube displayed multiple issues.

### **Highlighted Issue: JavaScript Variable Used Without Declaration**

SonarQube flagged a variable (`day`) used without defining it with `let`, `const`, or `var`.

### **Why This Matters**

- It becomes an unintended global variable  
- Other scripts can overwrite it  
- It can cause unpredictable behavior  
- Debugging becomes more difficult  
- In larger apps, this becomes a real security and stability issue  

SonarQube also categorized issues into:

- **Security Hotspots**  
- **Code Smells**  
- **Bugs**

```
[Insert Screenshot: SonarQube issue details]
[Insert Screenshot: Issues dashboard]
```

---

## **Challenges I Faced (And What They Taught Me)**

This project wasn’t perfect. These challenges taught me how real tools behave.

---

### **1. Extremely Slow SonarQube Download**

The image was large, and Docker pulled it slowly.

**What I learned:**  
Large enterprise tools require patience. Slow downloads don't always mean errors.

---

### **2. Scanner Failed Repeatedly**

I kept running scans before creating the SonarQube project.

**What I learned:**  
Tools like SonarQube follow specific workflows and expect certain steps in order.

---

### **3. Confusion About Authentication Tokens**

I had never used tokens before and needed to learn how they authenticate scanners.

**What I learned:**  
Even simple authentication systems require attention to detail. Tokens are widely used in real development pipelines.


---

## **What I Learned**

This project helped me understand how software development and cybersecurity overlap.

- **Static analysis is powerful.**  
  SonarQube detects vulnerabilities and coding issues that are easy to overlook.

- **Small mistakes can create big issues.**  
  The undeclared variable `day` showed how tiny errors become larger problems.

- **Troubleshooting is part of the process.**  
  Most tools don’t work perfectly the first time.

- **Professional tools require proper setup.**  
  SonarQube becomes extremely valuable once configured correctly.

---

## **Conclusion**

This project gave me hands-on experience with a real static analysis tool. Scanning DVWA with SonarQube helped me understand how vulnerabilities are detected, how issues are categorized, and how automated tools help developers improve code security and quality.

It strengthened my problem-solving skills and increased my confidence working with professional tools.

---

## **Resources**

- DVWA GitHub: https://github.com/digininja/DVWA  
- SonarQube: https://www.sonarsource.com/products/sonarqube/  
- SonarQube Documentation: https://docs.sonarqube.org  
- SonarScanner Guide: https://docs.sonarqube.org/latest/analyzing-source-code/scanners/sonarscanner/  
- Docker: https://www.docker.com  

