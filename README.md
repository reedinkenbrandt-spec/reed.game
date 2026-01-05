import turtle
import random

# Setup the screen
screen = turtle.Screen()
screen.setup(width=1000, height=1000)
screen.bgcolor("tan")
screen.tracer(0)  # Disable automatic screen updates for smoother animation

# Create the player turtle
my_turtle = turtle.Turtle()
my_turtle.color("light green")
my_turtle.shape("turtle")
my_turtle.penup()
my_turtle.speed(5)

# Generate and place obstacles
obstacles = []
num_obstacles = 10

for _ in range(num_obstacles):
    obstacle = turtle.Turtle()
    obstacle.shape("square")
    obstacle.color("green")
    obstacle.penup()
    x = random.randint(-450, 450)
    y = random.randint(-450, 450)
    obstacle.goto(x, y)
    obstacles.append(obstacle)

# Define movement functions
def move_up():
    my_turtle.forward(20)

def move_down():
    my_turtle.backward(20)

def turn_left():
    my_turtle.left(90)
    my_turtle.forward(10)  # Move slightly after turning for smoother feel

def turn_right():
    my_turtle.right(90)
    my_turtle.forward(10)  # Move slightly after turning for smoother feel

def dash_dash():
    my_turtle.forward(45)
    my_turtle.speed(9)

# Register key bindings
screen.onkey(move_up, "Up")
screen.onkey(move_down, "Down")
screen.onkey(turn_left, "Left")
screen.onkey(turn_right, "Right")
screen.onkey(move_up, "w")  # Use lowercase for keyboard keys
screen.onkey(move_down, "s") # Use lowercase for keyboard keys
screen.onkey(turn_left, "a") # Use lowercase for keyboard keys
screen.onkey(turn_right, "d") # Use lowercase for keyboard keys
screen.onkey(dash_dash, "space")  # "space" for the spacebar

# Create the target
target_turtle = turtle.Turtle()
target_turtle.shape("circle")
target_turtle.color("gray")
target_turtle.penup()
target_turtle.goto(250, 120)

# Collision detection and game loop
def check_collision():
    global random_x, random_y

    if my_turtle.distance(target_turtle) < 20:
        random_x = random.randint(-400, 400)
        random_y = random.randint(-400, 400)
        target_turtle.goto(random_x, random_y)
        target_turtle.showturtle()
        print("Collision detected! Target disappeared and reappeared.")

    for obstacle in obstacles:
        if my_turtle.distance(obstacle) < 20:
            print("You hit an obstacle! Game Over!")
            screen.bye() # Close the Turtle Graphics window

    screen.update()  # Manually update the screen after all drawing operations
    screen.ontimer(check_collision, 10) # Schedule the collision check to run again

# Start the game loop and listen for events
screen.listen()  # Start listening for key presses
check_collision() # Begin the collision detection loop
turtle.done()  # Keep the window open until manually closed
