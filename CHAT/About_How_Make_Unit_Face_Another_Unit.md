> Me: 
> ```
> How to make unit face another unit
> ```
> GPT:
> * To make one unit face another unit in a 2D game using Pygame, you can use the pygame.transform module to rotate the unit's image. 
> * Here is an example of how you can do this:
> * First, you need to load the image of your unit and create a Pygame Rect object to represent its position on the screen:
```python
import pygame

# Load the image of the unit
unit_image = pygame.image.load("unit.png")

# Create a Rect object to represent the unit's position and size
unit_rect = unit_image.get_rect()
unit_rect.center = (400, 300)  # Set the center of the Rect object to (400, 300)
```
> * Next, you need to calculate the angle between the two units. You can use the Pythagorean theorem and the math.atan2() function to do this:
```python
import math

# Calculate the distance between the two units
dx = other_unit_rect.centerx - unit_rect.centerx
dy = other_unit_rect.centery - unit_rect.centery
distance = math.sqrt(dx ** 2 + dy ** 2)

# Calculate the angle between the two units
angle = math.atan2(dy, dx) * 180 / math.pi
```
> * The math.atan2() function returns the angle in radians, so you need to convert it to degrees by multiplying it by 180 / math.pi.
> * Finally, you can use the pygame.transform.rotate() function to rotate the unit's image by the calculated angle:
```python
# Rotate the unit's image
rotated_unit_image = pygame.transform.rotate(unit_image, -angle)
rotated_unit_rect = rotated_unit_image.get_rect(center=unit_rect.center)
```
> * The -angle argument is used to rotate the image counterclockwise, which makes the unit face the other unit. The center argument of the get_rect() method is used to set the center of the rotated image to the center of the original Rect object.
> * Here is the complete code:
```python
import pygame
import math

# Initialize Pygame
pygame.init()
screen = pygame.display.set_mode((800, 600))
clock = pygame.time.Clock()

# Load the image of the unit
unit_image = pygame.image.load("unit.png")

# Create a Rect object to represent the unit's position and size
unit_rect = unit_image.get_rect()
unit_rect.center = (400, 300)

# Create another unit for testing
other_unit_rect = pygame.Rect(100, 100, 50, 50)

# Main game loop
while True:
    # Handle events
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            exit()

    # Calculate the angle between the two units
    dx = other_unit_rect.centerx - unit_rect.centerx
    dy = other_unit_rect.centery - unit_rect.centery
    distance = math.sqrt(dx ** 2 + dy ** 2)
    angle = math.atan2(dy, dx) * 180 / math.pi

    # Rotate the unit's image
    rotated_unit_image = pygame.transform.rotate(unit_image, -angle)
    rotated_unit_rect = rotated_unit_image.get_rect(center=unit_rect.center)

    # Render game objects
    screen.fill((255, 255, 255))
    pygame.draw.rect(screen, (255, 0, 0), other_unit_rect)
    screen.blit(rotated_unit_image, rotated_unit_rect)

    # Update display
    pygame.display.update()
    clock.tick(60)
```
