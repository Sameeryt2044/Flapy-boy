```bash 
pip install pygame 
``` 
Basic Flappy Bird Game Code: 
```python 
import pygame 
import random 
# Pygame initialize karein 
pygame.init() 
# Screen ke dimensions 
SCREEN_WIDTH = 400 
SCREEN_HEIGHT = 600 
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT)) 
# Colors define karein 
WHITE = (255, 255, 255) 
BLACK = (0, 0, 0) 
GREEN = (0, 255, 0) 
# Clock object 
clock = pygame.time.Clock() 
# Bird class 
class Bird: 
def __init__(self): 
self.x = 50 
self.y = 250 
self.width = 34 
self.height = 24 
self.gravity = 0.6 
self.velocity = 0 
self.jump_strength = -10 
def jump(self): 
self.velocity = self.jump_strength 
def move(self): 
self.velocity += self.gravity 
self.y += self.velocity 
 
def draw(self, screen): 
pygame.draw.rect(screen, BLACK, (self.x, self.y, self.width, self.height)) 
# Pipe class 
class Pipe: 
def __init__(self): 
self.x = SCREEN_WIDTH 
self.height = random.randint(150, 450) 
self.gap = 150 
def move(self): 
self.x -= 5 
def draw(self, screen): 
pygame.draw.rect(screen, GREEN, (self.x, 0, 50, self.height)) 
pygame.draw.rect(screen, GREEN, (self.x, self.height + self.gap, 50, SCREEN_HEIGHT)) 
# Game function 
def game(): 
bird = Bird() 
pipes = [Pipe()] 
score = 0 
running = True 
while running: 
clock.tick(30)  # Frame rate 
for event in pygame.event.get(): 
if event.type == pygame.QUIT: 
running = False 
if event.type == pygame.KEYDOWN: 
if event.key == pygame.K_SPACE: 
bird.jump() 
 
bird.move() 
if bird.y > SCREEN_HEIGHT or bird.y < 0: 
running = False 
for pipe in pipes: 
pipe.move() 
if pipe.x < bird.x < pipe.x + 50: 
if bird.y < pipe.height or bird.y + bird.height > pipe.height + pipe.gap: 
running = False 
 
if pipes[0].x < -50: 
pipes.pop(0) 
pipes.append(Pipe()) 
score += 1 
screen.fill(WHITE) 
bird.draw(screen) 
for pipe in pipes: 
pipe.draw(screen) 
 
pygame.display.flip() 
pygame.quit() 
# Game run karein 
game() 
``` 
