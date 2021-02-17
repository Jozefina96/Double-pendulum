# Double-pendulum

import pygame
import os
import math
import random
from points import Points
import formula

os.environ['SDL_VIDEO_CENTERED']='1' #centers the video in the middle of the screen

width, height = 1920, 1080 #size of the video
SIZE = (width, height)
pygame.init()
pygame.display.set_caption("Double pendulum")
fps = 30
screen = pygame.display.set_mode(SIZE)
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
angle_velocity1 = 0 
angle_velocity2 = 0 
angle_acceleration1 = 0
angle_acceleration2 = 0
Gravity = 8
scatter1 = []
scatter2 = []

starting_point = (int(width/2), int(height/4))

x_offset = starting_point[0]
y_offset = starting_point[1]

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
    
    x1 = float(lenght1*math.sin(angle1) +x_offset)
    y1 = float(lenght1*math.cos(angle1) +y_offset)
    
    x2=float(x1+lenght2*math.sin(angle2))
    y2=float(y1+lenght2*math.cos(angle2))
    
 #the angle varies with respect to the velocity and the velocity wrt the FirstAcceleration
 
    angle_velocity1 +- angle_acceleration1
    angle_velocity2 +- angle_acceleration2
    angle1 +- angle_velocity1
    angle2 +- angle_velocity2
 
    scatter1.append((x1,y1))
    scatter2.append((x2,y2))
 
    for point in scatter2:
        random_color=(random.randint(0,255), random.randint(0,255), random.randint(0,255))
        plot = Points(point[0], point[1], screen, white, scatter2)
        plot.draw()
    
    pygame.draw.line(screen, white, starting_point, (x1,y1), 6)
 
    pygame.draw.line(screen, white, (x1,y1), (x2,y2), 6)
 
    pygame.draw.circle(screen, white, (int(x2), int(y2)), 10)
 
    pygame.draw.circle(screen, (20, 200, 30), (int(x1), int(y1)), 20 )
 
    if len(scatter1)>1:
        pygame.draw.lines(screen, (100, 50, 100), False, scatter1, 1)
  
 
    pygame.quit()



