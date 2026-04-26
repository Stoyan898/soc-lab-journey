
🛡️ Phishing Detection – Email Log Analysis (Splunk)
🎯 Objective

Detect phishing activity using email logs in Splunk by identifying:

Suspicious sender domains
Malicious URLs
Dangerous attachments
Social engineering patterns
🧪 Dataset

A simulated email dataset (email_logs.csv) was ingested into Splunk.

Fields:

timestamp
sender
recipient
subject
url
attachment
⚙️ Data Ingestion
Uploaded CSV file into Splunk
Configured source type: CSV
Enabled field extraction using header row
Indexed under: email_logs
🔍 Detection Use Cases
🔹 Suspicious Sender Domains

Detect typosquatting and spoofed domains:

index=email_logs
| search sender="*micr0soft*" OR sender="*paypa1*"
| table sender subject url
🔹 Suspicious URLs

Detect phishing links and internal IP usage:

index=email_logs
| where like(url, "%login%") OR like(url, "%192.168%")
| table sender url subject
🔹 Malicious Attachments

Detect potentially dangerous file types:

index=email_logs
| search attachment="*.exe"
| table sender subject attachment
🔹 Social Engineering Detection

Detect urgency-based phishing:

index=email_logs
| search subject="*Urgent*" OR subject="*Verify*" OR subject="*Transfer*"
| table sender subject recipient
🔹 Correlation Detection

Combine multiple indicators:

index=email_logs
| eval suspicious=if(
    like(sender,"%micr0soft%") OR 
    like(url,"%login%") OR 
    like(attachment,"%.exe%"),
    "YES","NO"
)
| table sender subject url attachment suspicious
🚨 Alert Configuration
Name: Phishing Detection – Suspicious Email Activity
Type: Scheduled
Cron: */5 * * * *
Time Range: Last 5 minutes
Trigger: Number of results > 0
🧠 Key Findings
Detected typosquatting domains (micr0soft.com, paypa1.com)
Identified malicious login URLs
Flagged executable attachments
Recognized social engineering patterns
Built a correlation-based detection rule
🧩 MITRE ATT&CK Mapping
Technique	ID	Description
Phishing	T1566	General phishing attacks
Spearphishing Link	T1566.002	Malicious links in emails
Spearphishing Attachment	T1566.001	Malicious attachments
Application Layer Protocol	T1071	Use of web traffic (malicious URLs)
🧠 Skills Gained
Log ingestion and parsing in Splunk
SPL query writing
Detection engineering
Threat hunting basics
SOC alert creation
✅ Outcome

Successfully built a phishing detection pipeline using:

Simulated logs
SPL queries
Alerting
