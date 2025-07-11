# 📊 Elasticsearch & Kibana RBAC Project (IEC 62443-Inspired)

This project demonstrates a realistic, secure Elastic Stack deployment on WSL2 with **Role-Based Access Control (RBAC)** inspired by the **IEC 62443 standard** for industrial environments.  
It covers creating least-privilege user accounts, verifying with CLI and UI, and logging exactly what each role can — and *can’t* — do.

---

## 📌 Table of Contents

1. ✅ Overview  
2. 🔑 Superuser Login & Admin Checks  
3. 🛡️ RBAC Roles & Privileges  
   - Logstash Writer Role
   - Monitor Role
   - SOC Analyst Role
4. 👥 User Accounts  
   - Logstash Writer User
   - Monitor User
   - SOC Analyst User
5. 🔍 Tests & Validation
   - CLI Tests
   - UI Access Tests
   - Discover Queries
6. 📸 Screenshots by Section

---

## ✅ 1. Overview

- Deployed **Elasticsearch**, **Kibana**, and **Logstash** on **WSL2**  
- Enabled HTTPS and built-in user authentication
- Created custom roles:
  - `levi_logstash_writer_role` → pipeline writes only
  - `levi_monitor_role` → read-only cluster monitoring
  - `levi_analyst_role` → SOC-style access to dashboards & Discover
- Enforced **least privilege** with real CLI and UI tests

---

## 🔑 2. Superuser Login & Admin Checks

### Login as `elastic` Superuser

![elastic_login.png](images/elastic_login.png)  
_Elastic Stack login screen using the built-in `elastic` superuser._

### Admin Welcome Page

![admin_welcome.png](images/admin_welcome.png)  
_Successful login shows full-stack admin access._

### Admin RBAC View

![admin_rbac.png](images/admin_rbac.png)  
_Admin console showing all custom roles created._

### Discover as Admin

![discover_as_elastic.png](images/discover_as_elastic.png)  
_Verifying index data and Discover view as the superuser._

---

## 🛡️ 3. RBAC Roles & Privileges

### Logstash Writer Role

![logstash_writer_role.png](images/logstash_writer_role.png)  
_Custom `levi_logstash_writer_role` with write-only permissions for pipelines._

### Monitor Role

![monitor_role.png](images/monitor_role.png)  
_Custom `levi_monitor_role` for read-only cluster and index stats._

### SOC Analyst Role

![analyst_role.png](images/analyst_role.png)  
_Custom `levi_analyst_role` for SOC users to access dashboards._

![analyst_role_kibana.png](images/analyst_role_kibana.png)  
_Kibana feature-level privileges scoped for `levi_analyst_role`._

---

## 👥 4. User Accounts

### Logstash Writer User

![logstash_writer_user.png](images/logstash_writer_user.png)  
_User `levi_logstash_writer` mapped to the writer role for pipeline outputs only._

### Monitor User

![monitor_user.png](images/monitor_user.png)  
_User `levi_monitor` mapped to the monitor role._

### SOC Analyst User

![analyst_user.png](images/analyst_user.png)  
_User `levi_analyst` mapped to the SOC analyst role._

### Analyst Welcome Page

![analyst_welcome.png](images/analyst_welcome.png)  
_Analyst login shows appropriate access._

### Analyst Login Attempt

![analyst_login.png](images/analyst_login.png)  
_Login view for the analyst role._

### Analyst Correct Role Confirmation

![analyst_correct_role.png](images/analyst_correct_role.png)  
_Validates correct role assignment._

### Analyst RBAC Details

![analyst_rbac.png](images/analyst_rbac.png)  
_RBAC screen confirming granular privileges._

---

## 🔍 5. Tests & Validation

### 🟢 Logstash Writer CLI Test (Expected 403)

![levi_logstash_writer_attempt.png](images/levi_logstash_writer_attempt.png)  
_Test shows `levi_logstash_writer` gets **403 Forbidden** for read queries — pipeline-only as intended._

### 🔴 Logstash Writer UI Login Attempt

![levi_logstash_writer_login_attempt.png](images/levi_logstash_writer_login_attempt.png)  
_Attempt to log in to Kibana as `levi_logstash_writer` is blocked._

### 🚫 Logstash Writer No Permission Page

![levi_logstash_writer_no_permission.png](images/levi_logstash_writer_no_permission.png)  
_Permission denied page proves zero UI access for pipeline-only users._

---

### 🟢 Monitor CLI Test

![curl_levi_monitor_test.png](images/curl_levi_monitor_test.png)  
_CLI query returns healthy indices for `levi_monitor`._

### 🗂️ Monitor Role Details

![monitor_role.png](images/monitor_role.png)  
_Monitor role definition for context._

### 🗂️ Monitor User Details

![monitor_user.png](images/monitor_user.png)  
_Monitor user mapping confirmation._

---

### ✅ SOC Analyst Discover Test

![discover_as_analyst.png](images/discover_as_elastic.png)  
_Analyst using Discover to query allowed indices._

---

## 📸 6. Screenshots by Section

All screenshots live in `/images/` for easy reference.

---

## 🗒️ How to Run

```bash
sudo systemctl start elasticsearch kibana logstash
