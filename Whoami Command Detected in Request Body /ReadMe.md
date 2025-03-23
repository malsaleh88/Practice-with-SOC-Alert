# 🛡 Incident Report: Remote Command Execution on WebServer1004

## 📌 Attacker Information

- **Attacker IP:** `61.177.172.87`
- **Location:** China (CHINANET Jiangsu Network)
- **User-Agent Used:** `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1)`
- **Traffic Direction:** Internet ➡️ Internal Network

---

## 🖥️ Target Host Information

- **Hostname:** `WebServer1004`
- **Internal IP:** `172.16.17.16`
- **Service Targeted:** Web application at `/video/` endpoint
- **HTTP Method Used:** `POST`

---

## 🚨 Type of Attack

The attack is classified as a **Remote Command Execution (RCE)**. The attacker sent POST requests to the web server with system commands embedded in a parameter (`?c=`), trying to execute them directly on the server.

### ⚠️ Example Commands Sent:

- `?c=whoami`
- `?c=ls`
- `?c=uname`
- `?c=cat /etc/passwd`
- `?c=cat /etc/shadow`
![1](https://github.com/user-attachments/assets/2365db8a-82eb-4c1e-95ce-69255916fb3a)
![2](https://github.com/user-attachments/assets/29884974-c65e-4da5-824b-9855e95f19a3)
![3](https://github.com/user-attachments/assets/d4f4b673-aaf2-48e4-9738-b307c5de9aeb)
![4](https://github.com/user-attachments/assets/b26ac199-e061-4663-ac42-4a05698edb29)

---

## ✅ Why the Attack Was Successful

- The server responded with **HTTP 200 OK** to every malicious request.
- The **response size increased** with each command, suggesting real output was returned (e.g., file contents).
- The application **did not sanitize input**, allowing commands to be executed directly.
- No security controls (like WAF or input validation) blocked the requests.
- Sensitive files like `/etc/shadow` were accessed, indicating high-level access.

---

## 🧯 Containment Actions

- **Immediate containment was performed** by isolating `WebServer1004` from the network.
- All traffic from the attacker's IP (`61.177.172.87`) was blocked at the firewall.
- The vulnerable `/video/` endpoint has been taken offline for investigation.
- Forensic investigation and log collection are ongoing.
- The vulnerability is being analyzed and patches will be applied before rejoining the server to the network.
![5](https://github.com/user-attachments/assets/ad340032-5c99-43aa-81ba-a47b067b5d61)

---

## 📂 Status: Contained
The threat has been successfully contained. No further signs of attacker activity have been observed as of the latest review.


