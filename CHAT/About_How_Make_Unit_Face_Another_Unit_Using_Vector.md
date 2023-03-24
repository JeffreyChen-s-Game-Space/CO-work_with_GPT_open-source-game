> Me: 
> ```
> How to make unit face another unit
> ```
> GPT:
> * To make one unit face another unit in a 2D game using Pygame, you can use the pygame.math.Vector2 class to calculate the direction from the first unit to the second unit. 
> * You can then use the pygame.transform.rotate function to rotate the image of the first unit accordingly.
> * Here's an example code snippet that demonstrates how to do this:
```python
import pygame
import math

# Initialize Pygame
pygame.init()

# Set up the game window
screen = pygame.display.set_mode((640, 480))

# Load the image for the unit
unit_image = pygame.image.load("unit.png")

# Create two units with random positions
unit1_pos = pygame.math.Vector2(100, 100)
unit2_pos = pygame.math.Vector2(400, 300)

# Main game loop
while True:
    # Handle events
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            exit()

    # Calculate the direction from unit 1 to unit 2
    direction = unit2_pos - unit1_pos
    # Calculate the angle of the direction vector
    angle = math.atan2(-direction.y, direction.x) * 180 / math.pi

    # Rotate the image of unit 1
    rotated_image = pygame.transform.rotate(unit_image, angle)

    # Get the rect of the rotated image and center it on unit 1's position
    rect = rotated_image.get_rect()
    rect.center = unit1_pos

    # Render the game objects
    screen.fill((255, 255, 255))
    screen.blit(rotated_image, rect)

    # Update the display
    pygame.display.update()
```
> * In this example, we first load the image for the unit using pygame.image.load. We then create two pygame.math.Vector2 objects to represent the positions of the two units.
> * Inside the game loop, we calculate the direction from unit 1 to unit 2 using vector subtraction (unit2_pos - unit1_pos). 
> * We then calculate the angle of this direction vector using the math.atan2 function.
> * Note that we need to negate the y component of the direction vector to account for the inverted y-axis in Pygame.
> * We then use pygame.transform.rotate to rotate the image of unit 1 by the calculated angle. We get the rect of the rotated image using get_rect and center it on unit 1's position using rect.center = unit1_pos.
> * Finally, we render the rotated image using blit and update the display using pygame.display.update().