Setup Instructions

1. What to load
Please load all the flat files inside Project code file. 

2. How to start it up
1) Open the Kiosk domain.
2) Here we have two different conversational modes: a) Build user model by talking with them
													b) Give recommendation to user
3) If you want to play with a) option:
    Copy and paste below command into "Commands" tab.
    (achieve :receiver interaction-manager :content (playWithKioskFriend))
    Then ask questions related with location.
    Like, "Where is ken forbus's office?" to trigger the conversation.
    Then you can type "Yes" or "No" to response to the follow up question kiosk asks.
    If you type "Yes", it will ask your basic information, and store them inside KB.
    An example of basic information sentence is like, "I'm a junior student and in computer science major."
    If you type "No", it will end the conversation, without building user microtheory.
	
	===Example Dialog:===
	Hi cathy, how can I help you today? 
	where is ken forbus's office? 
	Ken Forbus' office is located at Mudd Room 3113. 
	cathy, Are you maybe interested in AI and Cognitive Science? 
	Yes. 
	Can you please tell me your grade and major? Thanks. 
	I'm a junior student and in computer science major. 
	Ok, store ur info: major: ComputerScience, grade: Junior-Student, anything else I can help? 
	No. 
	Alright, see you. 
	

4) If you want to play with b) option:
    First, please setup case library, here due to one session manager can only have one username, thus we created some dummy data.
    You can call the below command to set up case library.
    (achieve :receiver interaction-manager :content (kioskFriendCaselibrarySetup))
    To start the recommendation part, call:
    (achieve :receiver interaction-manager :content (playWithKioskFriend))
    (N.B. Currently we can only handle ask for research group recommendation.)
	
	Also clean up the current user microtheory if you played a) option before.
	(doForgetKBMt '(UserContextFn ?currentUser)) 
	
	So the interaction part will look like below if you want to play with it.
	Type "I want to find a research group." to trigger the recommendation part.
	
	When Kiosk asks follow up questions, you can use below two kinds of sentences to response. (Others might work, but we didn't test it / due to NF coverage)
	"I'm a senior student and in computer engineering major."
	"I'm a junior student and in computer science major."
	
	After that, it will give recommendations.	
	Right now, after kiosk give recommendations, we plan to stop here. So uses "No." to end the conversation.
	
	===Example Dialog:===
	Hi cathy, how can I help you today? 
	I want to find a research group. 
	cathy, can you tell me your major and what year are you? 
	I'm a senior student and in computer engineering major. 
	Ok, store ur info. And based on previous students' data, I would recommend NUComputingAlgorithmsAndApplications group. Anything else I can help? 
	No. 
	Alright, see you. 