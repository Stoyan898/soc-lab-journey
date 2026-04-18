# Commands Used

## SPL Detection Query
```spl
index=* (EventCode=4625 OR EventCode=4672)
| eval user=Account_Name
| stats count(eval(EventCode=4625)) as failed_logins 
        count(eval(EventCode=4672)) as privilege_events 
        min(_time) as first_seen 
        max(_time) as last_seen 
        by user, host
| eval time_diff = last_seen - first_seen
| where failed_logins >= 3 AND privilege_events >= 1 AND time_diff <= 86400


Click **Commit**

---

### 3. Clean your README

Go back to `README.md`

👉 REMOVE the command section  
👉 REPLACE with this:

```markdown id="3r7v3j"
## 🔧 Commands Used

See full queries here: [commands-used.md](commands-used.md)
