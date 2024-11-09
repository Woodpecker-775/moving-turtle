# moving-turtle
-TASK-

Here's the code for making the turtle move in a rectangular path using ROS in the Turtlesim package.
Make sure you have already set up your ROS environment and Turtlesim as per the task instructions.

Create a new ROS package if not already done:

bash
Copy code
cd ~/catkin_ws/src
catkin_create_pkg turtle_rectangle rospy std_msgs geometry_msgs
cd ~/catkin_ws
catkin_make
Create a new Python script named turtle_rectangle.py inside your package:

bash
Copy code
cd ~/catkin_ws/src/turtle_rectangle/src
touch turtle_rectangle.py
chmod +x turtle_rectangle.py
Open turtle_rectangle.py and add the following code:

python
Copy code
#!/usr/bin/env python

import rospy
from geometry_msgs.msg import Twist
from turtlesim.srv import TeleportAbsolute
import time

def move_straight(distance, speed):
    velocity_message = Twist()
    velocity_message.linear.x = speed
    distance_traveled = 0
    rate = rospy.Rate(10)
    while not rospy.is_shutdown() and distance_traveled < distance:
        pub.publish(velocity_message)
        rate.sleep()
        distance_traveled += speed * 0.1

    # Stop moving after reaching distance
    velocity_message.linear.x = 0
    pub.publish(velocity_message)

def turn(angle, speed):
    velocity_message = Twist()
    velocity_message.angular.z = speed
    angle_turned = 0
    rate = rospy.Rate(10)
    while not rospy.is_shutdown() and angle_turned < angle:
        pub.publish(velocity_message)
        rate.sleep()
        angle_turned += speed * 0.1

    # Stop turning after reaching angle
    velocity_message.angular.z = 0
    pub.publish(velocity_message)

if __name__ == "__main__":
    rospy.init_node("turtle_rectangle", anonymous=True)
    pub = rospy.Publisher("/turtle1/cmd_vel", Twist, queue_size=10)

    # Define the dimensions of the rectangle
    length = 3.0
    breadth = 2.0
    speed_straight = 1.0
    speed_turn = 1.0

    try:
        while not rospy.is_shutdown():
            # Move in rectangle: straight -> turn -> straight -> turn
            move_straight(length, speed_straight)
            turn(1.57, speed_turn)  # 90 degrees in radians
            move_straight(breadth, speed_straight)
            turn(1.57, speed_turn)
    except rospy.ROSInterruptException:
        pass
Run the package:

bash
Copy code
rosrun turtle_rectangle turtle_rectangle.py
This code should make the turtle move in a rectangular path. You can modify the dimensions or speed as needed. Once everything works, push your package to a GitHub repository and make the screen recording as specified
