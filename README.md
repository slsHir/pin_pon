# pin_pongfrom
pygame import *


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
    def update(self):
        keys_pressed = key.get_pressed()
        if keys_pressed[K_LEFT] and self.rect.x > 5:
            self.rect.y -= self.speed 

        if keys_pressed[K_RIGHT] and self.rect.x < 635:
            self.rect.x += self.speed

game = True
finish = False
clock = time.Clock()
FPS = 60


while game:

    for e in event.get():
        if e.type == QUIT:
            game = False

       
    
    display.update()
    time.delay(FPS)
