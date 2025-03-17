
# LFI Attack Investigation - ReadMe

## Alert Information
- **Severity:** High  
- **Date Closed:** Mar 17, 2025, 03:24 PM  
- **Rule Name:** SOC170 - Passwd Found in Requested URL - Possible LFI Attack  
- **Event ID:** 120  
- **Type:** Web Attack  

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

## Playbook Execution
Once the alert was triggered, we created a **case** and proceeded with the **playbook** to guide us through the investigation.

### **Step 1: Why Was the Alert Triggered?**
- The request contained `../../../../etc/passwd`, indicating a **Local File Inclusion (LFI) attack**.
- The attacker attempted to access **sensitive system files**.

### **Step 2: Collect Information**
- **Ownership of Source IP:** Tencent Cloud (AS45090, China)  
- **Reputation Check:** IP scored **-15** in VirusTotal (community flagged suspicious).  
- **Target System:** Windows Server 2019 (not Linux, making the attack ineffective).  

### **Step 3: Identify the Type of Attack**
- **Attack Type:** Local File Inclusion (LFI)  
- **Reason:** The attacker attempted to exploit a web vulnerability to read system files using path traversal.

### **Step 4: Is the Traffic Malicious?**
- ✅ **Yes, the traffic is malicious.**
- Even though the attacker targeted a Linux file on a Windows server, this was a **clear attack attempt**.

### **Step 5: What is the Attack Type?**
- **Type:** Local File Inclusion (LFI)
- The attacker attempted to include system files in the web request.

### **Step 6: Is This a Planned Test?**
- ❌ **No, this was not a planned test.**

### **Step 7: Direction of Traffic**
- **Traffic Flow:** Internet → Company Network  

### **Step 8: VirusTotal Check for Attacker's IP**
- **Reputation Score:** **-15** (flagged as suspicious but not blocked by security vendors).

### **Step 9: Was the Attack Successful?**
- **❌ No, the attack was NOT successful.**
- The attacker requested a **Linux file**, but the target server runs **Windows**, making the attack ineffective.

### **Step 10: Adding Artifacts**


### **Step 11: Is Tier 2 Escalation Required?**
- ❌ **No, escalation is not required** because the attack was **not successful**.

### **Step 12: Analyst Notes**
-This was a real LFI attack attempt from IP 106.55.45.162. The attack was allowed but failed because the target was a Windows server, not Linux. No signs of compromise were found. Monitoring will continue for further attempts.


### **Step 13: Closing the Alert**
- **Verdict:** ✅ **True Positive** (Real attack attempt, but unsuccessful).
- **Notes added and alert closed.**

---

### ✅ **Final Recommendations**
1. **Monitor for repeated attacks** from IP `106.55.45.162`.
2. **Block the attacker's IP** if further suspicious activity is detected.
3. **Implement security measures** (e.g., WAF rules) to prevent LFI attacks.
4. **Ensure proper input validation** on web applications to mitigate LFI risks.

🚀 **This completes the investigation.**
