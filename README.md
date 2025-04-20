# *Dork Like a Demon: Shodan Edition for Hackers and Bug Bounty Hunters*  💀

## ⚠️ Disclaimer:
> This article is **strictly for educational purposes**. The examples and dorks shared are meant to raise awareness about exposed systems and services on the internet. **Do not misuse** this information for unauthorized access or unethical activity. Always practice **responsible disclosure** and adhere to your local cyber laws.

![Image](https://github.com/user-attachments/assets/305fc80b-185b-48e8-b4b2-ec31a32b99d1) <br/>

---

## 🧠 Introduction: Why Shodan Dorks Deserve the Spotlight

While most of the hacking community is busy exploiting **Google Dorks** or scrubbing through **GitHub Dorks**, there's an underrated weapon in the arsenal of elite recon masters — **Shodan Dorks**.

Shodan isn’t just a search engine. It’s the *dark mirror of the internet* — indexing everything from exposed webcams to entire ICS/SCADA systems running unpatched firmware. If it’s internet-connected, Shodan probably knows it... and so can you.

Let’s break down Shodan dorking into **three mastery tiers**, and I’ll guide you through each with examples, syntax breakdowns, and advanced techniques.

![Image](https://github.com/user-attachments/assets/265dfde8-d985-4feb-ad05-015c5b7f8438) <br/>

---

## 🟢 1. Easy Dorks for Beginners

### 📸 Exposed Webcams

- **What it does:** Finds IP cams running `webcamXP` software  
- **Syntax:** `http.title:"<PAGE_TITLE>"`  
- **Breakdown:**
  - `http.title:"<PAGE_TITLE>"` → Searches HTML title tags of indexed web pages.
    - `<PAGE_TITLE>` is the string Shodan should match.
    - Example: `"webcamXP"` to find exposed webcam interfaces.  
- **Example Dork Code:**  
  ```shodan
  http.title:"webcamXP"
  ```

---

### 🧑‍💻 Open FTP Servers

- **What it does:** Finds FTP servers that allow anonymous login  
- **Syntax:** `port:<PORT> <KEYWORD>`  
- **Breakdown:**
  - `port:<PORT>` → Specifies the service port to search on.
    - `<PORT>` is a placeholder for port number.
    - Example: `21` is default for FTP.
  - `<KEYWORD>` → Searches for any keyword in the banner or metadata.
    - Example: `anonymous` for anonymous login access.  
- **Example Dork Code:**  
  ```shodan
  port:21 anonymous
  ```

---

### 🪟 Outdated Windows Machines

- **What it does:** Finds devices running Windows 7  
- **Syntax:** `os:"<OPERATING_SYSTEM>"`  
- **Breakdown:**
  - `os:"<OPERATING_SYSTEM>"` → Searches by operating system fingerprint.
    - `<OPERATING_SYSTEM>` is the system name or version.
    - Example: `"Windows 7"` finds machines still running Win7.  
- **Example Dork Code:**  
  ```shodan
  os:"Windows 7"
  ```

---

## 🟡 2. Intermediate Dorks for Rising Hackers

### 🌐 Misconfigured MongoDB Databases

- **What it does:** Finds exposed MongoDB instances without authentication  
- **Syntax:** `product:"<PRODUCT_NAME>" port:<PORT>`  
- **Breakdown:**
  - `product:"<PRODUCT_NAME>"` → Matches the product name in banners.
    - `<PRODUCT_NAME>` is the service name.
    - Example: `"MongoDB"` identifies MongoDB servers.
  - `port:<PORT>` → Default MongoDB port.
    - Example: `27017`  
- **Example Dork Code:**  
  ```shodan
  product:"MongoDB" port:27017
  ```

---

### 🔐 Exposed Login Panels

- **What it does:** Identifies admin login portals  
- **Syntax:** `http.title:"<LOGIN_TITLE>"`  
- **Breakdown:**
  - `http.title:"<LOGIN_TITLE>"` → Matches text from HTML title tags.
    - `<LOGIN_TITLE>` is the text shown on login pages.
    - Example: `"Admin Login"`  
- **Example Dork Code:**  
  ```shodan
  http.title:"Admin Login"
  ```

---

### 🧭 Specific Geolocation Targets

- **What it does:** Finds services exposed in a specific country  
- **Syntax:** `port:<PORT> country:"<COUNTRY_CODE>"`  
- **Breakdown:**
  - `port:<PORT>` → Port number for the desired service.
    - Example: `22` for SSH.
  - `country:"<COUNTRY_CODE>"` → Filters results by country.
    - `<COUNTRY_CODE>` is a 2-letter ISO code.
    - Example: `"IN"` for India.  
- **Example Dork Code:**  
  ```shodan
  port:22 country:"IN"
  ```

---

## 🔴 3. Complex/Compound Dorks for Advanced Dorking

### 🧨 Apache Servers with Expired SSL in the US

- **What it does:** Finds Apache web servers with expired SSL certs in the US  
- **Syntax:** `product:"<PRODUCT_NAME>" ssl:"<SSL_STATUS>" country:"<COUNTRY_CODE>"`  
- **Breakdown:**
  - `product:"<PRODUCT_NAME>"` → Specifies the web server software.
    - Example: `"Apache httpd"`
  - `ssl:"<SSL_STATUS>"` → SSL certificate status.
    - Example: `"expired"`
  - `country:"<COUNTRY_CODE>"` → Location filter.
    - Example: `"US"` for United States.  
- **Example Dork Code:**  
  ```shodan
  product:"Apache httpd" ssl:"expired" country:"US"
  ```

---

### 🧪 Devices Vulnerable to CVEs (e.g., Confluence CVE-2021-26084)

- **What it does:** Finds potentially vulnerable Confluence servers  
- **Syntax:** `http.html:"<PAGE_IDENTIFIER>" port:<PORT>`  
- **Breakdown:**
  - `http.html:"<PAGE_IDENTIFIER>"` → Looks for specific strings in HTML.
    - Example: `"Atlassian Confluence"`
  - `port:<PORT>` → Default Confluence port.
    - Example: `8090`  
- **Example Dork Code:**  
  ```shodan
  http.html:"Atlassian Confluence" port:8090
  ```

---

### 🎛️ ICS/SCADA Devices

- **What it does:** Detects Modbus protocol on industrial systems  
- **Syntax:** `port:<PORT> name:"<BANNER_NAME>"`  
- **Breakdown:**
  - `port:<PORT>` → Modbus operates on port 502.
    - Example: `502`
  - `name:"<BANNER_NAME>"` → Protocol/service name in the banner.
    - Example: `"modbus"`  
- **Example Dork Code:**  
  ```shodan
  port:502 name:"modbus"
  ```

---

## 📦 BONUS: Dork Chains for Pro-Level Filters

### 🔗 Cisco Routers with Expired SSL in Germany

- **Syntax:** `product:"<PRODUCT>" ssl:"<SSL_STATUS>" country:"<COUNTRY_CODE>"`  
- **Breakdown:**
  - Example:  
    - `product:"Cisco"`  
    - `ssl:"expired"`  
    - `country:"DE"`  
- **Example Dork Code:**  
  ```shodan
  product:"Cisco" ssl:"expired" country:"DE"
  ```

---

### 🔗 Elasticsearch Leaking Data in India

- **Syntax:** `port:<PORT> product:"<PRODUCT_NAME>" country:"<COUNTRY_CODE>"`  
- **Breakdown:**
  - Example:
    - `port:9200`
    - `product:"ElasticSearch"`
    - `country:"IN"`  
- **Example Dork Code:**  
  ```shodan
  port:9200 product:"ElasticSearch" country:"IN"
  ```

---

## 🧠 Conclusion: Respect the Power of the Internet’s Dark Mirror

Shodan dorking isn’t just a skill — it’s a **superpower**. It reveals a layer of the internet that’s usually invisible. Whether you're doing OSINT, red teaming, or bug bounty recon, mastering Shodan Dorks will take your game to the next level.

But with great visibility comes great responsibility.

---

## ⚠️ Final Disclaimer:
> This article is for **educational** and **ethical purposes only**. Do not exploit, damage, or interfere with any exposed system you find using Shodan. Always adhere to **legal boundaries**, follow **responsible disclosure practices**, and use this knowledge to **protect**, not to harm.

---
