- 👋 Hi, I’m @TRA
- 👀 I’m student at Royal univerysity Phnom penh Cambodia
- 🌱 I’m currently learning computer sincene
- 💞️ I’m looking to collaborate on my coding building
- 📫 How to reach me Thank

<!---
PEE-TRA/PEE-TRA is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

# Import necessary Libraries
import pyttsx3
import speech_recognition as sr
import winsound
import time

talk = pyttsx3.init() #initialize pyttsx3


#possible lists of possible words or sentences with different punctuation
call_list = ['totla', 'Totla', 'tot la', 'Tot la', 'Patla', 'patla']
r_u_there = ['Are you there', 'are you there', 'Are You There', 'Are you their',
             'are you their', 'You there', 'You there', 'You their', 'you their']
hi_List = ['hi', 'Hi', 'Hello', 'hello', 'Hey', 'hey', 'yo', 'Yo,' 'salam', 'Salam',
             'hi totla', 'Hi totla', 'totla', 'Totla']
bye_List = ['Bye', 'bye', 'Goodbye', 'goodbye', 'Good bye' 'good bye', 'byebye',
             'by by', 'By by', 'Tata', 'tata', 'So long', 'so long', 'okay bye', 'ok bye', 'Ok bye', 'Okay bye']
qst1_list = ["Who are you", 'who are you', 'whats your name', 'your name',
             'Your name', 'What are you', 'what are you']
res_neg_list = ['Bad Robot', 'bad robot', 'Bad robot','bad boy', "Bad boy", 'you are rude',
             'You are rude', 'Bad robot' 'bad robot', 'Bad Robot']
slang_list = ['Bal', 'bal', 'Crap', 'crap', 'chutiya', 'Chutiya', 'chootia', 'Chootia']
Love_list = ['i love you', 'I love you', 'Love you', 'love you']
hate_list = ['i hate you', 'I hate you', 'Hate you', 'hate you']

def Listen():
    """
    Takes users voice as input and converts it to text.
    """
    speech = sr.Recognizer()
    #say beep before listening
    
    #take input from microphone
    with sr.Microphone() as source:
        winsound.Beep(frequency = 2500, duration = 100) #beep to inform that it's listening
        print("Say>>")
        voice = speech.listen(source) 
        text = speech.recognize_google(voice)
        print(text) #print what it heard just to debug

    return text  #return what was heard

    
def Decide(listen):
    """
    Takes decision based on what user says.
    """
    print(f" Command = {listen}.") #just to debug

    #see what user said is in which list or not
    if listen in hi_List:
        Respond("Hi there, Good to see you.")

    elif listen in bye_List:
        Respond("I liked talking with you, okay take care.")

    elif listen in Love_list:
        Respond("Yuk, I have a robot girl friend, No seat available")
    
    elif listen in hate_list:
        Respond("Hate you too.")
     
    elif listen in qst1_list:
        Respond("""I am Totla bot. The dumb talking robot written in python.
                    My creator Ashraf minhaj is trying to make me smart""")
    
    elif listen in res_neg_list:
        Respond("I am very sorry I was just joking.")

    elif listen in slang_list:
        Respond("You are a bad guy")
    
    elif listen in r_u_there:
        Respond("For, you, Always sir")

    else:
        Respond("Sorry I don't understand Please say again.")

        

def Respond(t):
    print(f"Talking the: {t}") #to debug and see if everythings going okay

    talk.say(t)
    talk.setProperty('rate', 90) #90 words per minute
    talk.runAndWait()

while True: #forever loop 
     
    """
    The robot needs a WakeUp command so that it
    can start listening to.
    """
    try:
        speech = sr.Recognizer()
    
        #take input from microphone
        with sr.Microphone() as source:
            print("call>>")
            voice = speech.listen(source) 
            called = speech.recognize_google(voice)
            print(called) #print what it heard just to debug

            if called in call_list:
                comm = Listen() #listen to what user says

                Decide(comm)  #take decision and respond
    
    except: #No wake up word found
    pass #Do nothing avoiding the error
