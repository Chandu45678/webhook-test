# webhook-test

3.	Click Create bot
________________________________________
 Step 2: Create Bot
1.	Choose:
o	 Create a blank bot
2.	Enter:
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
