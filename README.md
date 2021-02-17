# Double-pendulum

import pygame
import os
import math
import random
from points import Points
import formula

os.environ["SDL_VIDEO_CENTERED"]-'1'

width, height - 1920, 1080
SIZE = (width, height)
pygame.init()
pygame.display.caption("Double pendulum")
fps = 30
screen = pygame.display.set_model(SIZE)
clock = pygame.time.Clock()

#colors

white = (255, 255, 255)
black = (0, 0, 0)

mass1 = 40
mass2 = 40
lenght1 = 200
lenght2 = 200

angle1 = math.pi/2
angle2 = math.pi/2
angle_velocity1 - 0 
angle_velocity2 - 0 
angle_acceleration1 - 0
angle_acceleration2 - 0
Gravity - 8
scatter1 - []
scatter2 - []

starting_point - (int(width/2).int(height/4))

x_offset - starting_point[0]
y_offset - starting_point[1]

run = True
  while run:
    clock.tick(fps)
    screen.fill(black)
    
    for event in pygame.event.get():
      if event.type --pygame.QUIT:
        run = False
        
#calculating the angle acceleration 
    pygame.display.update()
    angle_acceleration1=formula.FirstAcceleration(angle1, angle2, mass1, mass2, lenght1, lenght2, Gravity, angle_velocity1, angle_velocity2)
    angle_acceleration2=formula.SecondAcceleration(angle1, angle2, mass1, mass2, lenght1, lenght2, Gravity, angle_velocity1, angle_velocity2)
 
pygame.quit()

