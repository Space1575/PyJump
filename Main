import random,time,pygame,asyncio
from sys import exit
pygame.mixer.init()
pygame.font.init()
pygame.display.init()
font = pygame.font.SysFont('Monospace', 35)
f = pygame.font.SysFont('Roman',105)
Jump = False
stand = False
stop = False
s = False
run = False
gravity = 1
jump_height = 24
VelY = jump_height
FPS = 100
W, H = 500, 690
p_x = 20
vel = 1
p_y = 500
X, Y = W//2 -50, 200
platforms = []
p = pygame.image.load('PLAYER PYTHON JUMP.png')
py = pygame.transform.scale(p, (60, 60))
screen = pygame.display.set_mode((W, H))
pygame.display.set_caption("Python Jump")
start_time = time.time()
now_time = 0
clock = pygame.time.Clock()
key = pygame.key.get_pressed()
l = pygame.image.load('LOGO.png')
logo = pygame.transform.scale(l,(W +2,190))
plt = pygame.Rect((W//2 - 75),550,150,10)
def Text(now_time):
  text = font.render(f'Score: {round(now_time)}', True, 'Black')
  screen.blit(text, (0, 180))
def Check(now_time):
  if round(now_time) >= 0 and round(now_time) < 40:
    pause_time =200
  if round(now_time) >= 40 and round(now_time) < 60:
    pause_time = 270
  if round(now_time) >= 60 and round(now_time) < 80:
    pause_time = 290
  if round(now_time) >= 80 and round(now_time) < 120:
    pause_time = 310
  if round(now_time) >= 120:
    pause_time = 390
  return pause_time
async def main():
  global VelY, Jump, p_y, p_x, platforms, p, X, Y, vel, stand,player,platform,now_time,pause_time,key,s,stop,plt
  fall = 10
  run = True
  while run:
    key = pygame.key.get_pressed()
    player = pygame.Rect(X, Y, 60, 60)
    now_time = time.time() - start_time
    fall += clock.tick(FPS)
    screen.fill((50, 190, 100))
    pygame.draw.rect(screen,(240,200,100),(0,0,150,H-200))
    pygame.draw.rect(screen,(133, 206, 250),(W-150,0,150,H-100))
    pygame.draw.rect(screen,(0,80,80),(0,H-200,W-150,200))
    screen.blit(logo,(-2,0))
    Text(now_time)
    pause_time = Check(now_time)
    if vel <= 6:
      vel += 1
    else:
      vel += 0
    if fall > pause_time:
      for i in range(1):
        p_y = -10
        p_x = random.randint(0, W - 80)
        platform = pygame.Rect(p_x, p_y, 80, 15)
        platforms.append(platform)
        fall = 0
    for platform in platforms[:]:
      pygame.draw.rect(screen, (0, 0, 0), platform)
      platform.y += vel
      if platform.y > H + 20:
        platforms.remove(platform)
      if stop:
        platforms.remove(platform)
    for platform in platforms:
      if player.colliderect(platform):
          Y = platform.y-67
          VelY = jump_height
          stand = True
          Jump = False
          s = True
      if Y == platform.y-67 and not player.colliderect(platform):
        s = False
    if s == False:
      Y += vel+2
    if s == True:
      if Jump:
        Jump = True
    for event in pygame.event.get():
      if event.type == pygame.QUIT:
        pygame.quit()
        exit()
    if key[pygame.K_UP]:
      Jump = True
    if key[pygame.K_RIGHT] and X < 438:
      X += 6
    if key[pygame.K_LEFT] and X > 0:
      X -= 6
    if Jump == True:
      stand = False
      Y -= VelY
      VelY -= gravity
    if stand == True:
      Y += vel
    if Y > H:
      t = f.render("Game Over",True,(0,0,0))
      screen.blit(t,(3,H//2-40))
      pygame.display.update()
      stop= True
      for platform in platforms:
        platforms.remove(platform)
      pygame.time.delay(2000)
      break
    screen.blit(py, (player.x+10, player.y))
    if now_time >= 0 and now_time < 3.5:
      pygame.draw.rect(screen,(0,0,0),plt)
      if player.colliderect(plt):
        stand = True
        Y = plt.y -65
        s = True
    pygame.display.update()
    clock.tick(FPS)
    await asyncio.sleep(0)
asyncio.run(main())
