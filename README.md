# CS305_SoftwareSecurity
Artemis Financial Secure Software Development Portfolio
Repository Artifact
Selected Portfolio Artifact: `CS305_Project_Two_Report_Final.docx` (Artemis Financial Practices for Secure Software Report)

# Technical Reflection & Project Summary
### 1. Client Summary and Software Requirements
Artemis Financial is a specialized financial consulting firm that develops highly customized individual financial plans spanning savings, retirement, investments, and insurance. To modernize their enterprise operations while protecting sensitive client information, the company required the implementation of current, advanced software security controls. Specifically, they needed a robust data verification mechanism (a cryptographic checksum step) embedded into their web interface to protect data transfers from modification, alongside a full migration from unencrypted HTTP communications to secure transport protocols.

### 2. Finding Vulnerabilities & The Critical Value of Secure Coding
When identifying software vulnerabilities, I analyzed the specific conditions under which high-severity flaws could actually execute. For example, I successfully recognized that generic scanner flags for `CVE-2022-22965` (Spring4Shell) were false positives because our application bundles as an executable JAR file, rather than an external Tomcat WAR deployment. Coding securely is absolutely vital because code is rarely written from scratch; modern applications inherit massive attack surfaces through third-party libraries. If unvetted, these dependencies can become tools for malicious actors to infiltrate adjacent databases, networks, and systems. Implementing defensive coding protocols adds profound value to a company's well-being by shielding them from catastrophic regulatory fines (such as HIPAA or financial audit failures), protecting proprietary organizational assets, and preserving consumer trust.

### 3. Insights and Challenges in Vulnerability Assessments
The most helpful part of the assessment was using automated Software Composition Analysis (SCA) via the OWASP Dependency-Check tool. It provided a rapid, top-down look into our deep dependency tree. The most challenging aspect was managing "alert fatigue." It requires methodical, high-level code auditing and cross-referencing with the National Vulnerability Database (NVD) to dissect complex vulnerability parameters and determine whether a finding represents an actionable threat or a false positive.

### 4. Layering Security Controls and Future Mitigation Strategy
I increased layers of security by implementing a strict defensive posture at distinct architectural boundaries:

   * Transport Layer: Configured the application properties file to disable insecure HTTP paths and enforce HTTPS communication over port 8443 using a custom Java Keystore (`keystore.jks`).
   * Data Integrity Layer: Instantiated a JCA MessageDigest engine utilizing the SHA-256 cipher algorithm to generate unforgeable hex-encoded checksums for data validation.
   * Supply Chain Layer: Formulated an audited `suppression.xml` matrix rule configuration to isolate and filter out false-positive scanner alerts without ignoring new risks.
In the future, I will use automated continuous integration pipelines with tools like OWASP Dependency-Check alongside static application security testing engines. I will decide on mitigations by calculating risk metrics and prioritizing high-reachability and high-severity issues first.

### 5. Verifying Functionality and Checking for New Flaws
To ensure the application remained fully functional and secure after refactoring, I conducted a combination of manual code reviews, endpoint testing, and automated builds. I verified functionality by executing the Spring Boot server and performing runtime tests through a local secure web browser at `https://localhost:8443/hash`, ensuring the correct JSON data structure and matching hex string output were successfully processed without syntax faults.

To check if my code changes introduced new vulnerabilities, I ran a secondary static testing sequence using:
```
./mvnw dependency-check:check
```
This verified that the refactored code and newly added library imports complied fully with secure protocols without degrading our existing security posture.

### 6. Transferable Tools, Resources, and Coding Practices
Several utilities used in this project that will be highly beneficial for me in future software engineering roles:

* Java Cryptography Architecture (JCA): Leveraging classes like MessageDigest for robust data integrity validations.
* Java keytool CLI: Managing cryptographic assets, keystores, and certificate handshakes.
* Maven Dependency Management: Restructuring build descriptors (`pom.xml`) and crafting tailored exclusion configurations (`suppression.xml`) to manage software bills of materials cleanly.
* Secure Coding Hygiene: Applying proper input validation and utilizing native data-binding mechanisms instead of risky expression parsers.

### 7. Showcasing Work to Future Employers
When interviewing with technical hiring managers or security teams, I can show this assignment as concrete proof of my ability to build secure software pipelines. Specifically, I can showcase:

   1. Production-Grade Architecture: My ability to convert a vulnerable legacy application into a secure RESTful API running over encrypted HTTPS/TLS channels.
   2.  DevSecOps Automation: Mastery of automated dependency analysis tools and the capability to author formal, audited XML configurations that reduce team alert fatigue while maintaining strong security guardrails.
   3.  Technical Technical Writing: A comprehensive professional report illustrating that I can communicate deep cryptographic parameters, historical cipher landscapes, and business-risk mitigations clearly to both technical and corporate stakeholders.

