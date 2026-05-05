# webhook-test

3.	Click Create bot
 Step 2: Create Bot
1.	Choose:
o	 Create a blank bot
2.	Enter:..
o	Bot name: HotelBookingBot
3.	IAM role → Create new role
4.	Remaining defaultnext
5.	Language: English
6.	Voice (optional)
7.	Click Done
________________________________________
 Step 3: Create Intent
1.	Go to Intents
2.	Name: BookHotel
3.	Click Create
________________________________________
 Step 4: Add Sample Utterances
Add user sentences (how user talks):
I want to book a hotel
Book a room
Reserve hotel
I need a room
 These are Utterances
________________________________________
Step 5: Create Slots (User Inputs)
Slots collect user information.
 Add Slot
1.	Click Add slot
2.	Fill:
o	Slot name: age
o	Slot type: AMAZON.Number
o	Prompt: Which city do you want?
Mark as Required
Add IF Conditions (Conditional Logic)
 Used to control flow based on slot values
Example Condition:
If {age} < 18
Steps:
1.	Go to Intent → Slots -> under Advance options
2.	Scroll to Slot capture: success response ->Conditional branching
3.	Click Add condition
Example:
Condition:
 If {age} < 18
Response:
Your not eligible for hoot booking?
________________________________________
 Step 6: Create Slots (User Inputs)
Slots collect user information.
 Add Slot
3.	Click Add slot
4.	Fill:
o	Slot name: location
o	Slot type: AMAZON.City
o	Prompt: Which city do you want?
5.	Mark as Required

Repeat for other slots.
1.	Click Add slot 
2.	Fill details: 
o	Slot name: checkin 
o	Slot type: AMAZON.Date 
o	Prompt:
 "What is your check-in date?" 
3.	 Mark as Required 
(Optional but recommended) 
o	Add Retry prompt:
 "Please provide a valid date (e.g., 2026-03-25)" 
4.	Click Save 
________________________________________
Slot 7: Number of Nights (nights)
 Steps:
1.	Click Add slot again 
2.	Fill details: 
o	Slot name: nights 
o	Slot type: AMAZON.Number 
o	Prompt:
 "How many nights will you stay?" 
3.	Mark as Required 
4.	Click Save 
________________________________________

 Step 7: Create Custom Slot Type

Save intent

Click on Back to intents
If you want custom values:
1.	Go to Slot Types
2.	Click Add slot type ->add blank slot type
3.	Name: RoomType
Add values:
Single
Double
Suite
Save slot type
Now use this in slot: go back to intent
•	Slot name: RoomType
•	Slot type: RoomType
________________________________________
 Step 9: Add Response Cards (Card Groups)
 Used for buttons (quick replies)
Steps:
1.	Go to slot prompts -> more prompt options
2.	Click Add -> add card groups
Example:
Card Title: Select Room Type
click on add Buttons:
•	Single → "Single"
•	Double → "Double"
•	Suite → "Suite"
________________________________________
 Step 10: Configure Responses
Initial Response:
Welcome to Hotel Booking! What is your name?
Confirmation:
Do you want to confirm booking in {location} for {nights} nights?
________________________________________
 Step 11: Build & Test
1.	Click Build
2.	Use Test chatbot panel
3.	Try:
Book a hotel
________________________________________
Sample output
User: Book a hotel
Bot: What is your age?
User: 25
Bot: Which city do you want?
User: Hyderabad
Bot: Check-in date?
User: Tomorrow
Bot: Number of nights?
User: 2
Bot: Select room type
User: Double
Bot: Do you want to confirm booking in Hyderabad for 2 nights?
User: Yes
Bot: Booking confirmed.



///9 wk 
Copy the ssh key of instance and paste in the powershell 
Run sudo yum update –y  command in the powershell 
Run sudo yum install httpd  –y  command in the powershell 
Run  systemctl start httpd 
systemctl enable httpd 
echo  "This is Server 1" > /var/www/html/index.html

//for instance 2
Configure Security Group: 
• Allow SSH (22) from anywhere 
• Allow HTTP (80) from anywhere (0.0.0.0/0) 

Name : loadbalancer-sg -> give description 
click on add rule of inbound rule -> Allow HTTP (80) from anywhere 
Leave the outbound rules as default  
Click on create security group 
Go to EC2 → Load Balancers → Click on Create Load Balancer
lick on create of Application Load Balancer .Name: my-loadbalancer ->  Scheme: Internet-facing 
IP address type: IPv4 
 
Select the  deafault VPC where your EC2 instances exist 
Select all subnets (one for each instance if possible  
Choose the loadbalancer-sg security group created earlier.Click on create target group 
 
Name: my-targetgroup -> Target type: Instance 
Protocol: HTTP -> Port: 80 
Select ipv4 -> select the default vpc -> click on next .Select all the instances -> Click Include as pending → Click on next 
Review all settings → Click Create target group 
Go to Load Balancers → Select the loadbalancer → Description → copy the DNS name 
Paste it in a browser → You should see either WebServer-1 or WebServer-2 page. 
Refresh multiple times → Load balancer distributes traffic between the two instances 
Auto Scaling Group with Load Balancer 
 
Go to EC2 Console → Instances -> Select the EC2 instance  
Click Actions → Image and Templates → Create Image 
 
Provide Image Name: e.g., my-webserver-AMI 
Optional: Add description 
Click Create Image 
Go to EC2 → instances->Launch Templates → Create Launch Template 
 
Launch Template Name: my –template 
Add description 
Select  My AMIs -> select owned by  me 
AMI: Select the AMI created in Step 1 (webserver-1-AMI) 
 
Instance Type: t2.micro 
Key Pair: Select your existing key pair 
Set Health Check Grace Period: 3 seconds 
Click Next 
 
Desired Capacity: 2 (initial instances)  
Minimum Capacity: 1 -> Maximum Capacity: 4 
Click Next
Leave notifications and tags as default -> click next 
 
Review all settings 
Click Create Auto Scaling Group 
Go to Load Balancers → Select your Load Balancer 
Check Auto Scaling Group → Instances 
• You may see up to 4 instances if scaling triggers 
 
Test auto recovery: 
Select the instance -> Terminate the instance
 
2 instances will be created automatically by the auto scaling 
Select the load balancer -> copy the DNS name 
 
Paste the DNS in the incognito mode 
 You should see your web page from one of the instances -> Refresh multiple times → traffic alternates 
between instances 
 
//
echo '<!DOCTYPE html>
<html>
<head><title>Demo App</title></head>
<body>
<h2>AWS Elastic Beanstalk App</h2>

<form>
Name: <input type="text"><br><br>
Email: <input type="email"><br><br>

Skills:<br>
<input type="checkbox"> Java<br>
<input type="checkbox"> Python<br><br>

Gender:<br>
<input type="radio" name="g"> Male
<input type="radio" name="g"> Female<br><br>

<button>Submit</button>
</form>

</body>
</html>' > index.html
