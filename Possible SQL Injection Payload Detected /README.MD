# **SQL Injection Investigation Report**

## **Incident Details**
- **Event ID:** 115  
- **Event Time:** February 25, 2022, 11:34 AM  
- **Rule Triggered:** SOC165 - Possible SQL Injection Payload Detected  
- **Severity Level:** Security Analyst  

## **Attack Information**
- **Attacker's IP Address:** `167.99.169.17` (DigitalOcean Hosting)  
- **Target Hostname:** `WebServer1001`  
- **Target IP Address:** `172.16.17.18` (Internal Web Server)  
- **Attack Method:** `GET` Request  
- **Requested URL:**  
  ```
  https://172.16.17.18/search/?q=%22%20OR%201%20%3D%201%20--%20-
  ```  
- **User-Agent:**  
  ```
  Mozilla/5.0 (Windows NT 6.1; WOW64; rv:40.0) Gecko/20100101 Firefox/40.1
  ```  
- **Alert Trigger Reason:** SQL Injection Attempt (`OR 1=1` for Authentication Bypass)  
- **Device Action:** Allowed  



---

## **Target System Information**
- **Hostname:** WebServer1001  
- **Domain:** letsdefend.local  
- **Operating System:** Windows Server 2019 (64-bit)  
- **Primary User:** `webadmin`  
- **Last Login:** February 10, 2022, 11:12 PM (No new login detected)  

---

## **Attacker's Information**
- **IP Address:** `167.99.169.17`  
- **ASN:** `AS14061 - DigitalOcean, LLC`  
- **Hosting Provider:** DigitalOcean  
- **Geolocation:** Santa Clara, California, United States  
- **Abuse Contact:** [abuse@digitalocean.com](mailto:abuse@digitalocean.com)  

### **Threat Intelligence Reports**
- **VirusTotal Reputation:**
  - **4/94 Security Vendors Marked as Malicious**
  - **Flags:**
    - ArcSight Threat Intelligence: **Malware**
    - BitDefender: **Phishing**
    - CyRadar: **Malicious**
    - G-Data: **Phishing**
  - **Community Score:** `-16` (Negative Reputation)

---

## **Investigation Findings**
- The attack **was a real SQL Injection attempt** using `OR 1=1`, which is commonly used for authentication bypass.
- **No unauthorized login or database modification was detected**.
- The **last successful login was on February 10, 2022**, which is before the attack on February 25, 2022.
- **The attack was NOT successful.**
- The attacker's IP has been **blocked** and **reported to DigitalOcean**.
- Web security measures such as **input validation, prepared statements, and Web Application Firewall (WAF) enhancements** are being reviewed to prevent future attacks.

---

## **Conclusion**
✅ **Alert Classification:** **True Positive** (The attack was real but unsuccessful)  
🚀 **Recommended Actions:**
- **Block attacker’s IP (`167.99.169.17`)** in the firewall.
- **Review SQL query logs** to ensure no unauthorized access occurred.
- **Enhance security** by implementing **prepared statements** and **WAF rules**.
- **Report abuse** to DigitalOcean via [DigitalOcean Abuse Report](https://www.digitalocean.com/company/contact/#abuse).

---

## **Notes**
This alert is confirmed as **True Positive**, meaning an actual attack attempt was detected. However, **no unauthorized access was found**. Further security improvements are recommended to prevent similar SQL Injection attempts in the future.


