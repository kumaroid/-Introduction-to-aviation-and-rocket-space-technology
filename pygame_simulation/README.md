# В данном файле представлена программа для визуализции гравитационного маневра на языке "Python" с помощью библиотеки PyGame

```c:/PyGame-Simulation/simulation.py
import pygame, math
from pygame import *
from math import *

WIN_WIDTH = 800
WIN_HEIGHT = 640
PLANET_WIDTH = 20
PLANET_HEIGHT = 20
DISPLAY = (WIN_WIDTH, WIN_HEIGHT)
SPACE_COLOR = "#000022"
SUN_COLOR = "yellow"
PLANET_COLOR = "blue"

X0 = WIN_WIDTH // 2
Y0 = WIN_HEIGHT // 2
M0 = 5000
CRASH_DIST = 10
OUT_DIST = 1000

def main():
    pygame.init()
    screen = pygame.display.set_mode(DISPLAY)
    
    bg = Surface((WIN_WIDTH,WIN_HEIGHT))
    bg.fill(Color(SPACE_COLOR))
    draw.circle (bg, Color(SUN_COLOR), (X0, Y0), 10)
                                    
    timer = pygame.time.Clock()
    
    planet = Surface((PLANET_WIDTH, PLANET_HEIGHT))
    planet.fill(Color(SPACE_COLOR))
    draw.circle (planet,
        Color(PLANET_COLOR),
        (PLANET_WIDTH // 2, PLANET_HEIGHT // 2), 5)

    r = 0.0
    x = 100.0
    y = 290.0
    vx = 0.1
    vy = 1.5
    ax = 0.0
    ay = 0.0

    done = False
    while not done:
        timer.tick(25)
        for e in pygame.event.get():
            if e.type == QUIT:
                done = True
                break

        r = sqrt((x - X0)**2 + (y - Y0)**2)
        
        ax = M0 * (X0 - x) / r**3
        ay = M0 * (Y0 - y) / r**3

        vx += ax
        vy += ay

        x += vx
        y += vy

        screen.blit(bg, (0, 0))
        screen.blit(planet, (int(x), int(y)))
        pygame.display.update()

        if r < CRASH_DIST:
            done = True
            print("Crashed")
            break
        if r > OUT_DIST:
            done = True
            print("Out of system")
            break

if name == "main": main()
```
