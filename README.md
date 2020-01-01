# PongGame
Pong is one of the earliest arcade video games. It is a table tennis sports game featuring simple two-dimensional graphics. The game was originally manufactured by Atari, which released it in 1972.

Part 1: Getting started
The program will be developed using the turtle module. It’s a great little module for graphics and can be a great starting point for developing games using python. Pygame is another module that is very good for game dev but for starting off we will be using turtle. Turtle is built in to python so we do not have to install it unlike Pygame.

First thing we need to do I create our screen turtle object Note: that screen is capitalised. We than give our window a title. We will also set the background our window to black. Next, we want to change the size of our screen to be 600 x 800.

Now the next line wn.tracer(0) actually prevents the window from updating meaning we have to manually update it. We do this in order to speed up out games.

The main game loop is going to be where all the main activity of our game will be taking place. We create a while loop and when it’s true (which it always is meaning it’s guaranteed to run) do the following actions. We start this by telling the window to update. Now would be a good time to run the program and what you should have is a simple black screen 800 x 600 as specified. The coordinates at the centre is 0,0 +300 is the top and -300 is the bottom +400 and -400 is right and left respectively it’s important to remember this numbers for later.

import turtle

wn = turtle.Screen() #screen object
wn.title("Pong by Stephen Blaney")
wn.bgcolor("black")
wn.setup(width=800, height=600)

# Main game loop

while True:
    wn.update()
Part1

Part 2: Creating our paddles and ball
Moving on we need to create our pong paddles along with the ball. We do this by creating a Turtle object that will represent these items along with their respective attributes. The following is how we create our turtle objects.

Paddle_a = turtle.Turtle()

NOTE: Watch the capitalisation. Capital T as that is the class name.

We set the speed of our object to 0 which is the possible speed available otherwise this game would run very slow. The colour and shape of the paddle is set to white and square respectively, like the original game. We then lift our turtle pen; we do this cause by definition turtle objects draw the objects as they are moving across the screen. paddle_a.penup(). Now we want our turtle to draw our paddle at a certain part of the screen being the left, we set the turtle_a to( -350, 0).

Now you may have notice when we run the program, we have a square on the left, but the original game has more of a rectangular shape. Here we need to use the turtle.shapesize() method in order to stretch the width. The original square is 20 x 20 so we multiply by 5 to give 100 and that will be our final rectangle shape.

Now we have our first paddle done we essentially do the same thing again except make a few changes I’d recommend copy the code and make the necessary changes which I will go through now. The only change is that we need to set the goto to plus 350 as we are setting this object to the right and of course change the name of our turtle object.

Creating our ball is very similar to our paddles copy the paddle code block and rename it ball. We want to get rid of the stretch as we want the ball to be its original size and we need to set its position to the centre of the screen which of course is 0,0

# Paddle A
paddle_a = turtle.Turtle()
paddle_a.speed(0)  # fastest possible speed
paddle_a.shape("square")
paddle_a.color("white")
paddle_a.shapesize(stretch_wid=5, stretch_len=1)
paddle_a.penup()
paddle_a.goto(-350, 0)

# Paddle B
paddle_b = turtle.Turtle()
paddle_b.speed(0)  # fastest possible speed
paddle_b.shape("square")
paddle_b.color("white")
paddle_b.shapesize(stretch_wid=5, stretch_len=1)
paddle_b.penup()
paddle_b.goto(350, 0)

# Ball
ball = turtle.Turtle()
ball.speed(0)  # fastest possible speed
ball.shape("square")
ball.color("white")
ball.penup()
ball.goto(0, 0)
Part2

Step 3: Moving the Paddles.
We will be creating our first function of our program here, we will need this to control our paddles up and down. First things first we need to define our function def paddle_a_up(): Now, we need to get the current Y Coordinate of paddle_a y = paddle_a.ycor() . Ycor is from the turtle module and what it does is returns the y coordinates and we are assigning it to a variable called y. Note: Functions/ Methods in python must have four whitespaces after the function is defined otherwise you will get an indentation error. In order for this to move we need to get the current y coordinate and add by 20 pixels. This does not create the movement however, we need to set the paddle as the current version of the y coordinate (y + 20)

Now we have our function defined except it’s not being use, for our program to use our function we need to bind it to something we call keyboard binning’s. This is essentially having one of our keyboard keys activate or function to move our paddle.

Wn.listen this line listen for keyboard input and onKeypress() says when the w key is pressed call the paddle_a_up method which in turn runs the code within it and there moves the paddle 20 pixels up.

Now we have our left paddle going up, so what we can do is copy that method and use it for the paddle going down except this time we set new y cord as -20 and we also need to create a key binding for that as well. Now we have the full controls working for the left paddle. Repeat for the right paddle.

# Moving our paddles

def paddle_a_up():
     y = paddle_a.ycor()
     y += 20
     paddle_a.sety(y)

def paddle_a_down():
    y = paddle_a.ycor()
    y -= 20
    paddle_a.sety(y)

def paddle_b_up():
    y = paddle_b.ycor()
    y += 20
    paddle_b.sety(y)

def paddle_b_down():
    y = paddle_b.ycor()
    y -= 20
    paddle_b.sety(y)

# Keyboard Bindings
wn.listen()
wn.onkeypress(paddle_a_up, "w")
wn.onkeypress(paddle_a_down, "s")

wn.onkeypress(paddle_b_up, "Up")
wn.onkeypress(paddle_b_down, "Down")
Part 4: Moving the ball
Probably the main feature and most difficult part of our program. We need the ball to bounce off our two paddles as well as the top and bottom parts of our screen. We’ll start by dividing our balls movement into x and y using ball.dx = 2 and ball.dy which stands for delta or change. So, every time our ball moves it will move by 2 pixels. So, it’s going in a diagonal motion at his point and we put this kind code in our main game loop.

Now we have our ball moving to the upper right, next we need to do some boarder checking. We need to check the ball when it hits our wall and remember that our wall is 600 pixels and our ball is 10 so we subtract the difference and get 290 so when the position of y is greater than 290 we set the direction of the ball to go the opposite direction using ball.dy *= - 1

It’s the same process for the bottom screen.

Now it’s time to do the walls on the x axis which is very similar to the y walls except this time when the ball surpasses the paddle, we want to set the position of the ball to the centre (0, 0).

# Ball  movement parameters
ball.dx = 2
ball.dy = -2


while True:
    wn.update()

    # To actually move the ball
    ball.setx(ball.xcor() + ball.dx)
    ball.sety(ball.ycor() + ball.dy)

    # Border checking

    if ball.ycor() > 290:
        ball.sety(290)
        ball.dy *= -1

    if ball.ycor() < -290:
        ball.sety(-290)
        ball.dy *= -1

    if ball.xcor() > 390:
        ball.goto(0, 0)
        ball.dx *= -1

    if ball.xcor() < -390:
        ball.goto(0, 0)
        ball.dx *= -1
Part4

Part 5: Getting the ball to collide with the ball
Now we have to get the ball to bounce off of the paddles. Now if you recall our paddles are 20 pixels wide by 100 pixels long. So, we need to get our ball to bounce when it hit y coordinates that are between the top and bottom of the right side of our paddles. This involves a bit of maths to determine. If the xcor are between 340 and 350 (the top and bottom of a paddle) and the current ycor and y paddle positions plus 40 and the ycor and y paddle positions between -40. This is the pixels along the longer edge of our paddle. After this we set the position of x and reverse the direction.

Repeat code for the left paddle while changing our pixel coordinates for x.

Note: all this code goes within the main loop.

 # Paddle and ball collision
    if (ball.xcor() > 340 and ball.xcor() < 350) and (ball.ycor() < paddle_b.ycor() + 40 and ball.ycor() > paddle_b.ycor() -40):
        ball.setx(340)
        ball.dx *= -1

    if (ball.xcor() < -340 and ball.xcor() > -350) and (ball.ycor() < paddle_a.ycor() + 40 and ball.ycor() > paddle_a.ycor() - 40):
        ball.setx(-340)
        ball.dx *= -1
Part 6: Scoring
The way we are going to do this is that we’ll be drawing the score on to the upper centre of the screen we will be doing this using turtle. So, what we are going to do, is we are going to create a pen which is a simple turtle object like our ball and paddles. pen = turtle.Turtle(). We set our animation speed of our object and a colour. We then lift our pen, so we don’t have a line leading up to the upper part of our screen as turtles default position is always (0,0) then we hide after it’s done because we don’t want to see it after it’s done it’s job. We finally tell our pen to head to the x and y cors that we want it to draw this cause being our score. You may have to play around with the numbers. Then all we have to do next us to use the write method to get our required text, it’s font and alignment.

pen.write(“Player A: 0 Player B: 0”, align = “center”, font=(“Courier”, 24,”normal”))

Now we need to create two variables that will contain our score which will be set to 0 to start. We than need to go to the part of our code that tells us what happens when the ball reaches beyond the paddles. We simply increment our score by 1 when the ball surpasses the paddle and then update our screen. Note: It’s important to use pen.clear() to ensure the you are not drawing over the previous score. Run it to test and you have a well running game. Congratulations

score_a = 0
score_b = 0

 if ball.xcor() > 390:
        ball.goto(0, 0)
        ball.dx *= -1
        score_a += 100
        pen.clear()
        pen.write("Player A: {} Player B: {} ".format(score_a, score_b), align="center", font=("Courier", 24, "normal"))

    if ball.xcor() < -390:
        ball.goto(0, 0)
        ball.dx *= -1
        score_b += 100
        pen.clear()
        pen.write("Player A: {} Player B: {} ".format(score_a, score_b), align="center", font=("Courier", 24, "normal"))
        
Part 7: Sound.
To start you’ll need to download the bounce.wav sound file which is available in this repository. Now this is the solution if you are working on a windows operating system you need to import. winsound and place this line of code in to places the place where the ball hit the paddle. It’s important to have the bounce.wav file in the same directory as your pong.py file

Winsound.Palysound(“Bounce”, winsound.SND_ASYNC)

And that’s It’s the program is done the classic Atari Pong Enjoy!!!!
