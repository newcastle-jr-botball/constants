# CONSTANTS
This is a small basic script helping to explain constants to elementary students. 

Constants are like variables in that they are a place to store and access data within your program. The main difference between the two is that the value that a constant holds __does not change__ throughout the life of your program. The value is __constant__.

Why would we want to use a container for something that never changes? Why wouldn't we just use that value in the first place?

Well, let's use an example. One thing that you'll be doing in almost every program that you write for the Botball robot is to access the ports that the motors are plugged into. You'll remember that the robot has 4 ports into which a motor can be plugged: 0, 1, 2, and 3. Your programs currently look something like this:

    int main() {
        // move forward
        motor(0, 100);
        motor(3, 100);
        msleep(1000);
        
        // turn left
        motor(0, 100);
        motor(3, 25);
        msleep(500);
        
        // move forward
        motor(0, 100);
        motor(3, 100);
        msleep(1000);
        
        ao();
        return 0;
    }

You'll notice that we are accessing the ports for the motor multiple times within the program with `motor(0, 100)` etc. There are two potential problems with this: readability and maintenance.

READABILITY:  Readability is how easy is to read the code - whether you are the programmer, or someone else just looking at the code. If I didn't know that the right motor was plugged into port 0, then I would have to read through your code, trying to figure out line by line what happens. Eventually, I would be able to determine the motor, but not without having to take the time to read through your code carefully.

MAINTENANCE:  Maintenance in programming is how easy it is for us to go back to our program to make changes. If, for instance, we needed to change the port for the right motor from 0 to 1, then we would have to change every instance of the 0 referring to the port in our program to 1. That's fine for a 15 line program like above, but some of our programs will extend into hundreds if not thousands of lines of code. That would take quite a bit of time to change every instance - and if we make a mistake changing even one of the motor instances, then our program breaks. 

What we would like to do is create a variable that would hold the motor port for us that can then be referenced from within the program. However, the motor port will not change throughout the program. We don't accidentally want to change that variable, because our program would break. So, we create a __constant__ and our program will not compile if we attempt to change its value somewhere in the program - notifying us that something is wrong within the code. 

OK, so let's rewrite the program above to use constants.

    #define RIGHT_WHEEL 0   // right motor is plugged into M0 (motor port 0)
    #define LEFT_WHEEL 3    // left motor is plugged into M3 (motor port 3)
    int main() {
        // move forward
        motor(RIGHT_WHEEL, 100);
        motor(LEFT_WHEEL, 100);
        msleep(1000);
        
        // turn left
        motor(RIGHT_WHEEL, 100);
        motor(LEFT_WHEEL, 25);
        msleep(500);
        
        // move forward
        motor(RIGHT_WHEEL, 100);
        motor(LEFT_WHEEL, 100);
        msleep(1000);
        
        ao();
        return 0;
    }

OK, do you see what has changed? We __defined__ a constant by writing `#define RIGHT_WHEEL 0`. So, anywhere we want to reference the port that the right motor is plugged into, we can just use `RIGHT_WHEEL` like we're doing in the `motor` functions. This is much easier for someone to understand that just happens to read through our code. It is also easier for us to change the port that the motor is plugged into. If we want the right motor to be plugged into port 1, all we have to do is change one line:  just change `#define RIGHT_WHEEL 0` to `#define RIGHT_WHEEL 1` - and our program is instantly updated to work with that change.

We can do this with anything within our program that we want to be constant. For example:

    #define SPEED_SLOW 25
    #define SPEED_NORMAL 50
    #define SPEED_FAST 100  

Can you write some code that would use the constants from above to move your robot in a square?

*Note:*

The code used in these tutorials is intended to run on the KIPR Link controller and written in 
the KISS Platform. You can find information about the KIPR Link and KISS Platform at 
http://www.kipr.org/hardware-software. The KISS Platform includes a simulator, so you can run 
the code on your computer without a robot. Our Botball team currently participates in the Junior 
Botball Challenge sponsored by KIPR. You can view more information for the challenge at 
http://www.juniorbotballchallenge.org.
