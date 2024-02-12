# Rock-Paper-Scissor-Game
from tkinter import * #Tkinter module imports all functions and classes which are used for creating graphical user interfaces in python 
from PIL import Image,ImageTk #Imports necessary modules from the Python Imaging Library (PIL) to work with images

# PIL is the Python Imaging Library which provides the python interpreter with image editing capabilities. The Image module provides a class with the same name 
# which is used to represent a PIL image. The module also provides a number of factory functions, including functions to load images from files, and to create new images.

from random import randint #Imports the randint function from the random module to generate random integers.

#main window
root = Tk() #Creates the main window object using Tkinter.
root.title("Rock Paper Scissor") #Sets the title of the window.
root.configure(background="#9b59b6") #Configures the background color of the window.

#picture ( Loads and converts images into Tkinter-compatible format using PIL.)
rock_img = ImageTk.PhotoImage(Image.open("Rock.jpg"))
paper_img = ImageTk.PhotoImage(Image.open("paper.png"))
scissor_img = ImageTk.PhotoImage(Image.open("scissor.png"))

#insert picture
user_label = Label(root,image=scissor_img,bg="#9b59b6")
comp_label = Label(root,image=scissor_img,bg="#9b59b6")
comp_label.grid(row=1,column=0)
user_label.grid(row=1,column=4) #Creates labels to display user and computer choices and places them in the grid layout.



#scores
playerScore = Label(root,text=0,font=100,bg="#9b59b6",fg="white")
computerScore = Label(root,text=0,font=100,bg="#9b59b6",fg="white")
computerScore.grid(row=1,column=1)
playerScore.grid(row=1,column=3) #Creates labels to display player and computer scores.

#indicators
user_indicator = Label(root,font=50,text="USER",bg="#9b59b6",fg="white")
comp_indicator = Label(root,font=50,text="COMPUTER",bg="#9b59b6",fg="white")
user_indicator.grid(row=0,column=3)
comp_indicator.grid(row=0,column=1) #Creates labels for user and computer indicators.

#messages
msg = Label(root,font=50,bg="#9b59b6",fg="white",text="You Loose")
msg.grid(row=3,column=2) #Creates a label for displaying game result messages.

#update message
def updateMessage(x):
    msg['text'] = x #Updates the text of the message label.
    
Certainly! Let's look at the relevant lines of code:

python
Copy code
msg = Label(root, font=50, bg="#9b59b6", fg="white", text="You Loose")
msg.grid(row=3, column=2)

#update message
def updateMessage(x):
    msg['text'] = x
# Here, a Tkinter Label widget named msg is created with some initial settings. It has a default text of "You Loose". The widget is then placed in the grid 
# layout of the main window (root) at row 3 and column 2 using the grid method.

# The updateMessage function takes a parameter x and updates the text of the msg label with the value of x. This function is designed to dynamically 
# change the text of the label based on different game outcomes. For example, it might display "You Win", "You Loose", or "It's a tie !!!" depending on 
# the result of the game.

#update user score
def updateUserScore(): #updateUserScore is a function that increments the player's score.
    score = int(playerScore["text"]) #It retrieves the current score from the playerScore label using int(playerScore["text"]).
    score += 1 #Increments the score by 1.
    playerScore["text"]= str(score) #Converts the updated score back to a string (str(score)) and sets it as the new text for the playerScore label.

    

def updateCompScore():
    score = int(computerScore["text"])
    score += 1
    computerScore["text"]= str(score)

#check winner
def checkWin(player,computer):
    if player == computer:
        updateMessage("its a tie !!!")
    elif player == "rock":
        if computer == "paper":
            updateMessage("YOU LOOSE")
            updateCompScore()
        else:
            updateMessage("YOU WIN")
            updateUserScore()
    elif player == "paper":
        if computer == "scissor":
            updateMessage("YOU LOOSE")
            updateCompScore()
        else:
            updateMessage("YOU WIN")
            updateUserScore()
    elif player == "scissor":
        if computer == "rock":
            updateMessage("YOU LOOSE")
            updateCompScore()
        else:
            updateMessage("YOU WIN")
            updateUserScore()
    else :
        pass


#update choices
choices =["rock","paper","scissor"]
def updateChoice(x):
#for computer
    compChoice = choices[randint(0,2)]
    if compChoice=="rock":
        comp_label.configure(image=rock_img)
    elif compChoice =="paper":
        comp_label.configure(image=paper_img)
    else:
        comp_label.configure(image=scissor_img)

#for user
    if x=="rock":
        user_label.configure(image=rock_img)
    elif x =="paper":
        user_label.configure(image=paper_img)
    else:
        user_label.configure(image=scissor_img)
    checkWin(x,compChoice)


#button visit
rock=Button(root,width=20,height=2,text="ROCK",bg="#FF3E4D",fg="white",command = lambda:updateChoice("rock")).grid(row=2,column=1)
paper=Button(root,width=20,height=2,text="PAPER",bg="#FAD02E",fg="white",command = lambda:updateChoice("paper")).grid(row=2,column=2)
scissor=Button(root,width=20,height=2,text="SCISSOR",bg="#0ABDE3",fg="white",command = lambda:updateChoice("scissor")).grid(row=2,column=3)

#updateChoice("paper"), command=lambda: updateChoice("scissor"): Specifies the function to be executed when the button is clicked. In this case, 
#it uses lambda functions to call updateChoice with the corresponding choice ("rock", "paper", or "scissor").


root.mainloop() # Enters the Tkinter main event loop, which continuously listens for user input and updates the GUI accordingly.
