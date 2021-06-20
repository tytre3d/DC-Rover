## Welcome to the DC-Rover Project Page!

### Sample Code

```Python
from approxeng.input.selectbinder import ControllerResource
from adafruit_motorkit import MotorKit
dc = MotorKit()
import time
 
# Main Loop
while True:
 try:
  with ControllerResource() as joystick:
   while joystick.connected:
    # get x-axis value of the left analog stick
    left_x = joystick.lx
    # get y-axis value of the left analog stick
    left_y = joystick.ly
    
    #get d-pad left
    lstrafe = joystick['dleft']
    #get d-pad right
    rstrafe = joystick['dright']
    
    #Simple turn logic
    m1m4 = left_y + left_x
    m2m3 = left_y - left_x
    
    #Cap motor speed to 75% throttle
    if m1m4 > 1:
      m1m4 = 0.75
    if m1m4 < -1:
      m1m4 = -0.75
    if m2m3 > 1:
      m2m3 = 0.75
    if m2m3 < -1:
      m2m3 = -0.75
      
    # strafe left when left d-pad button is pressed
    if lstrafe:
      dc.motor1.throttle = 0.75
      dc.motor2.throttle = -0.75
      dc.motor3.throttle = -0.75
      dc.motor4.throttle = 0.75
    #strafe right when right d-pad button is pressed
    elif rstrafe:
      dc.motor1.throttle = -0.75
      dc.motor2.throttle = 0.75
      dc.motor3.throttle = 0.75
      dc.motor4.throttle = -0.75
    #motor control using left analog stick
    else:
      dc.motor1.throttle = m2m3*(-1)
      dc.motor2.throttle = m2m3*(-1)
      dc.motor3.throttle = m1m4*(-1)
      dc.motor4.throttle = m1m4*(-1)
    time.sleep(0.1)
 except IOError:
  # Will raise an exception if no controller/joystick is connected
  print("No Joystick Found!")
  time.sleep(1)




```

