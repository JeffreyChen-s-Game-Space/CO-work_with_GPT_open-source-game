> Me: 
> ```
> How to know unit is on cover
> ```
> GPT:
> * Detecting whether a unit is behind cover can be accomplished in several ways, depending on the specific requirements of your game. Here are a few general approaches that you can consider:
> * Using a collision detection system: You can define the cover objects in your game as collision objects, and then check whether the unit collides with any of these objects. 
> * This method can work well if the cover objects are simple shapes, such as rectangles or circles.
> * Using raycasting: You can cast rays from the unit's position in different directions and check if they intersect with any cover objects.
> * This method can work well if the cover objects are irregular shapes or have complex geometry.
> * Using a tile-based system: You can divide the game world into tiles and assign each tile a cover value. 
> * The cover value can indicate the level of cover provided by that tile, such as full cover, half cover, or no cover. 
> * You can then check the cover value of the tile the unit is currently standing on to determine if it is behind cover.
> * Here's an example of using a collision detection system to detect if a unit is behind cover:
```python
import pygame

# Define constants
COVER_COLOR = (0, 255, 0)  # Color of the cover objects
UNIT_COLOR = (255, 0, 0)  # Color of the unit
COVER_COLLISION_GROUP = 1  # Collision group for cover objects
UNIT_COLLISION_GROUP = 2  # Collision group for units

# Initialize Pygame
pygame.init()
screen = pygame.display.set_mode((800, 600))
clock = pygame.time.Clock()

# Create cover objects
cover1_rect = pygame.Rect(100, 200, 100, 50)
cover2_rect = pygame.Rect(400, 300, 75, 75)
cover_objects = [cover1_rect, cover2_rect]

# Create collision shapes for cover objects
cover_collision_shapes = []
for cover_rect in cover_objects:
    cover_collision_shapes.append(pygame.Rect(cover_rect.x, cover_rect.y, cover_rect.width, cover_rect.height))

# Create unit object
unit_rect = pygame.Rect(400, 200, 50, 50)

# Create collision shape for unit object
unit_collision_shape = pygame.Rect(unit_rect.x, unit_rect.y, unit_rect.width, unit_rect.height)

# Main game loop
while True:
    # Handle events
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            exit()

    # Update unit position
    unit_rect.x, unit_rect.y = pygame.mouse.get_pos()

    # Check if unit is behind cover
    is_behind_cover = False
    for cover_collision_shape in cover_collision_shapes:
        if unit_collision_shape.colliderect(cover_collision_shape):
            is_behind_cover = True
            break

    # Render game objects
    screen.fill((255, 255, 255))
    for cover_rect in cover_objects:
        pygame.draw.rect(screen, COVER_COLOR, cover_rect)
    pygame.draw.rect(screen, UNIT_COLOR, unit_rect)

    # Update display
    pygame.display.update()
    clock.tick(60)
```
> * In this example, we define two cover objects as Pygame rectangles and store them in a list. We also create corresponding collision shapes for these objects using the pygame.Rect class.
> * We then create a unit object as another Pygame rectangle and create a collision shape for it. We also define two collision groups, one for the cover objects and one for the units.
> * Inside the game loop, we update the position of the unit object based on the mouse position. We then check if the unit is behind cover by checking if its collision shape collides with any