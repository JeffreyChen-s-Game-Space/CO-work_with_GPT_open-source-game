> Me: 
> ```
> How to make a vision on 2d game pygame
> ```
> GPT:
> * Creating a vision system in a 2D game using Pygame can be accomplished in several ways, depending on the specific requirements of your game. 
> * Here is a general approach that you can consider:
> * Determine the range of the vision: Before you start, you need to determine the range of the vision that you want to implement. 
> * You can use a simple circle to represent the field of view, or you can use a more complex shape to represent obstacles and shadows.
> * Create a mask: Once you have determined the shape of the vision, you need to create a mask that represents the vision area.
> * You can create the mask using the Pygame surface module.
> * This mask will be used to limit the rendering of objects that are outside of the vision area.
> * Render the vision: Once you have the mask, you need to render the vision area. 
> * You can do this by rendering all the objects that are within the vision area, and then applying the mask to remove any objects that are outside of the vision area.
> * Update the vision: As the player moves around the game world, the vision area needs to be updated to reflect the new position of the player. 
> * You can achieve this by updating the mask and rendering the vision area again.
> * Here's some sample code to create a simple vision system using a circle as the field of view:

```python
import pygame
import math

# Define constants
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600
VISION_RADIUS = 100

# Initialize Pygame
pygame.init()
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
clock = pygame.time.Clock()

# Load resources
player_image = pygame.image.load('player.png').convert_alpha()

# Define player position
player_pos = (SCREEN_WIDTH // 2, SCREEN_HEIGHT // 2)

# Create vision mask
vision_mask = pygame.Surface((SCREEN_WIDTH, SCREEN_HEIGHT))
vision_mask.set_alpha(128)
pygame.draw.circle(vision_mask, (0, 0, 0), player_pos, VISION_RADIUS)

# Main game loop
while True:
    # Handle events
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            exit()
    # Update player position
    player_pos = pygame.mouse.get_pos()

    # Update vision mask
    vision_mask.fill((0, 0, 0, 0))
    pygame.draw.circle(vision_mask, (0, 0, 0), player_pos, VISION_RADIUS)
    
    # Render game objects
    screen.fill((255, 255, 255))
    screen.blit(player_image, player_pos)
    screen.blit(vision_mask, (0, 0), special_flags=pygame.BLEND_RGBA_MULT)

    # Update display
    pygame.display.update()
    clock.tick(60)
> ```
> * This code creates a Pygame window and loads an image of a player character. 
> * It then creates a vision mask using a circle, which is centered on the player's position. 
> * The mask is then used to limit the rendering of game objects outside of the vision area. 
> * Finally, the game loop updates the position of the player and the vision mask, and renders the player and the mask on the screen.