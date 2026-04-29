Python
import pygame
import sys

# Initialize
pygame.init()

# Screen
WIDTH, HEIGHT = 600, 400
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Stickman Jump Game")

# Colors
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)

# Player
x = 100
y = 300
velocity = 0
gravity = 0.8
jump_power = -15
on_ground = True

clock = pygame.time.Clock()

def draw_stickman(x, y):
    # Head
    pygame.draw.circle(screen, BLACK, (x, y-40), 10, 2)
    # Body
    pygame.draw.line(screen, BLACK, (x, y-30), (x, y), 2)
    # Arms
    pygame.draw.line(screen, BLACK, (x-10, y-20), (x+10, y-20), 2)
    # Legs
    pygame.draw.line(screen, BLACK, (x, y), (x-10, y+20), 2)
    pygame.draw.line(screen, BLACK, (x, y), (x+10, y+20), 2)

# Game loop
while True:
    screen.fill(WHITE)

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()

        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_SPACE and on_ground:
                velocity = jump_power
                on_ground = False

    # Gravity
    velocity += gravity
    y += velocity

    # Ground collision
    if y >= 300:
        y = 300
        velocity = 0
        on_ground = True

    # Draw ground
    pygame.draw.line(screen, BLACK, (0, 320), (WIDTH, 320), 3)

    # Draw player
    draw_stickman(x, int(y))

    pygame.display.update()
    clock.tick(60)
