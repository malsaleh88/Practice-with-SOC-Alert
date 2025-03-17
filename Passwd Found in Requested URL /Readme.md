
# LFI Attack Investigation - ReadMe

## Alert Information
- **Severity:** High  
- **Date Closed:** Mar 17, 2025, 03:24 PM  
- **Rule Name:** SOC170 - Passwd Found in Requested URL - Possible LFI Attack  
- **Event ID:** 120  
- **Type:** Web Attack  
![1](https://github.com/user-attachments/assets/77de1635-411e-4c71-ba16-4964989323eb)

## Event Details
- **Event ID:** 120  
- **Event Time:** Mar 01, 2022, 10:10 AM  
- **Rule:** SOC170 - Passwd Found in Requested URL - Possible LFI Attack  
- **Level:** Security Analyst  
- **Hostname:** WebServer1006  
- **Destination IP Address:** 172.16.17.13  
- **Source IP Address:** 106.55.45.162  
- **HTTP Request Method:** GET  
- **Requested URL:** `https://172.16.17.13/?file=../../../../etc/passwd`  
- **User-Agent:** Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; .NET CLR 1.1.4322)  
- **Alert Trigger Reason:** URL Contains "passwd"  
![2](https://github.com/user-attachments/assets/5d1e90cf-1185-4e64-9316-eb75f2026f14)
![18](https://github.com/user-attachments/assets/f25a487d-800f-441b-9783-cc03c1cd6e23)

![3](https://github.com/user-attachments/assets/639f2fa1-dea2-43fc-a929-c11e7d4aeb46)


![4](https://github.com/user-attachments/assets/03f651b1-a6dd-4b44-bde2-ea253b35e33e)

## Playbook Execution
Once the alert was triggered, we created a **case** and proceeded with the **playbook** to guide us through the investigation.
![5](https://github.com/user-attachments/assets/f7481339-f79e-4a0b-9be1-4ca068f9f167)

### **Step 1: Why Was the Alert Triggered?**
- The request contained `../../../../etc/passwd`, indicating a **Local File Inclusion (LFI) attack**.
- The attacker attempted to access **sensitive system files**.
![6](https://github.com/user-attachments/assets/6aee8844-0268-4f09-9ef9-0126c2037d6f)

### **Step 2: Collect Information**
- **Ownership of Source IP:** Tencent Cloud (AS45090, China)  
- **Reputation Check:** IP scored **-15** in VirusTotal (community flagged suspicious).  
- **Target System:** Windows Server 2019 (not Linux, making the attack ineffective).  
![7](https://github.com/user-attachments/assets/0a1a3dd3-9409-49c1-a92e-fcc3c34d6b23)
![8](https://github.com/user-attachments/assets/19163253-01ea-4813-a931-0d4f1f56c9f2)

### **Step 3: Identify the Type of Attack**
- **Attack Type:** Local File Inclusion (LFI)  
- **Reason:** The attacker attempted to exploit a web vulnerability to read system files using path traversal.

### **Step 4: Is the Traffic Malicious?**
- ✅ **Yes, the traffic is malicious.**
- Even though the attacker targeted a Linux file on a Windows server, this was a **clear attack attempt**.
![9](https://github.com/user-attachments/assets/728896ba-a080-40a5-aad9-e25434ed8bd7)

### **Step 5: What is the Attack Type?**
- **Type:** Local File Inclusion (LFI)
- The attacker attempted to include system files in the web request.
![10](https://github.com/user-attachments/assets/02e12436-87e1-4099-9b87-a103198d4148)

### **Step 6: Is This a Planned Test?**
- ❌ **No, this was not a planned test.**
![11](https://github.com/user-attachments/assets/06411f34-53ba-4830-95e0-38397fc4507c)

### **Step 7: Direction of Traffic**
- **Traffic Flow:** Internet → Company Network  
![12](https://github.com/user-attachments/assets/9b1d34cf-a67e-4ea5-870a-8db2e577a1dc)

### **Step 8: VirusTotal Check for Attacker's IP**
- **Reputation Score:** **-15** (flagged as suspicious but not blocked by security vendors).
![13](https://github.com/user-attachments/assets/5e41da52-703a-45f6-9982-676e49df663d)

### **Step 9: Was the Attack Successful?**
- **❌ No, the attack was NOT successful.**
- The attacker requested a **Linux file**, but the target server runs **Windows**, making the attack ineffective.

### **Step 10: Adding Artifacts**
![15](https://github.com/user-attachments/assets/894b1d8a-42ef-4540-b122-fabc740697fb)


### **Step 11: Is Tier 2 Escalation Required?**
- ❌ **No, escalation is not required** because the attack was **not successful**.
![16](https://github.com/user-attachments/assets/63574500-dc40-4277-9f78-f30eaf64723e)

### **Step 12: Analyst Notes**
-This was a real LFI attack attempt from IP 106.55.45.162. The attack was allowed but failed because the target was a Windows server, not Linux. No signs of compromise were found. Monitoring will continue for further attempts.


### **Step 13: Closing the Alert**
- **Verdict:** ✅ **True Positive** (Real attack attempt, but unsuccessful).
- **Notes added and alert closed.**
![19](https://github.com/user-attachments/assets/0cabe283-cae0-44e2-9f54-4f40bdfc6f9c)
![20](https://github.com/user-attachments/assets/f2101d7e-847b-4cef-95f8-3e0c6b2b64ef)

---

### ✅ **Final Recommendations**
1. **Monitor for repeated attacks** from IP `106.55.45.162`.
2. **Block the attacker's IP** if further suspicious activity is detected.
3. **Implement security measures** (e.g., WAF rules) to prevent LFI attacks.
4. **Ensure proper input validation** on web applications to mitigate LFI risks.

🚀 **This completes the investigation.**
