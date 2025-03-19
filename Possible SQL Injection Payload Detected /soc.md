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



![map](https://github.com/user-attachments/assets/c7207cb0-f493-464a-8be4-4bb9171b61dc)

![map2](https://github.com/user-attachments/assets/ae3ed61c-c642-4ae0-8314-2fd1d39f4e0f)





