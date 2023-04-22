from pygame import *
back =(255,255,255)
win_width = 600
win_height = 500
win = display.set_mode((win_width,win_height))
font.init()

font1 = font.Font(None,35)
lose1 = font1.render('Left player lost',True,(100,0,0))
lose2 = font1.render('Right player lost',True,(100,0,0))

class GameSprite(sprite.Sprite):
    def __init__ (self, player_image, player_x, player_y, player_width, player_height ,player_speed):
        super().__init__()
        self.image = transform.scale(image.load(player_image),(player_width,player_height))
        self.speed = player_speed
        self.rect = self.image.get_rect()
        self.rect.x = player_x
        self.rect.y = player_y
        self.width = player_width
        self.height = player_height
    def reset(self):
        win.blit(self.image,(self.rect.x , self.rect.y))



class Player(GameSprite):
    def update_l(self):
        keys_pressed = key.get_pressed()
        if keys_pressed[K_w] and self.rect.y > 5:
            self.rect.y -= self.speed 

        if keys_pressed[K_s] and self.rect.y - 390:
            self.rect.y += self.speed
    def update_r(self):
        keys_pressed = key.get_pressed()
        if keys_pressed[K_UP] and self.rect.y > 5:
            self.rect.y -= self.speed 

        if keys_pressed[K_DOWN] and self.rect.y - 390:
            self.rect.y += self.speed


platform = Player('platform.png',35, 20, 20, 85, 5)
platfrom2 = Player('platform.png',570, 20, 20, 85, 5)
ball = GameSprite('ball.png',100,100,45,45,5)

game = True
Finish = False
FPS = 60
clock = time.Clock()

speedx = 3
speedy =3

while game:
    for e in event.get():
        if e.type == QUIT:
            game = False
    if not Finish:
        ball.rect.x += speedx
        ball.rect.y += speedy

    if ball.rect.y >= 460:
        speedy *= -1
    if ball.rect.y >= 0:
        speedy *= -1
    
    if sprite.collide_rect(ball, platform):
        speedx *= -1
       
    
    if sprite.collide_rect(ball, platfrom2):
        speedx *= -1
        

    if ball.rect.x < 0:
        Finish = True
        win.blit(lose2)
    
    if ball.rect.x > win_width:
        Finish = True
        win.blit(lose1)

        win.fill(back)
        ball.reset()
        platform.reset()
        platfrom2.reset()
        ball.update()
        platform.update_l()
        platfrom2.update_r()


    display.update()
    clock.tick(FPS)
Нижний колонтитул
© 2023 GitHub, Inc.
Нижний колонтитул навигации
Условия
Конфиденциальность
Безопасность
Положение дел
Документы
Связаться с GitHub
Цены
API
Обучение
Блог
О
