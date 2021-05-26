## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/tytre3d/DC-Rover/edit/main/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```Python
from approxeng.input.selectbinder import ControllerResource
from adafruit_motorkit import MotorKit
kit = MotorKit()
import time
 
# Get a joystick
with ControllerResource() as joystick:
  # Loop until disconnected
  while joystick.connected:
  # Get a corrected value for the left stick x-axis
  left_x = joystick.lx
  # We can also get values as attributes:
  left_y = joystick.ly
  m1m4 = left_y + left_x
  m2m3 = left_y - left_x
  lstrafe = joystick['dleft']
  rstrafe = joystick['dright']
  if m1m4 > 1:
    m1m4 = 0.75
  if m1m4 < -1:
    m1m4 = -0.75
  if m2m3 > 1:
    m2m3 = 0.75
  if m2m3 < -1:
    m2m3 = -0.75
  if lstrafe:
    kit.motor1.throttle = 0.75
    kit.motor2.throttle = -0.75
    kit.motor3.throttle = 0.75
    kit.motor4.throttle = -0.75
  elif rstrafe:
    kit.motor1.throttle = -0.75
    kit.motor2.throttle = 0.75
    kit.motor3.throttle = -0.75
    kit.motor4.throttle = 0.75
  else:
    kit.motor1.throttle = m1m4*(-1)
    kit.motor2.throttle = m2m3*(-1)
    kit.motor3.throttle = m2m3*(-1)
    kit.motor4.throttle = m1m4*(-1)
  time.sleep(0.1)
```
```markdown

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](IMG_1742.jpg)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/tytre3d/DC-Rover/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
