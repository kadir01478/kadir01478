#pgzero
import random

WIDTH = 600
HEIGHT = 400

TITLE = "UZAY SAVAŞI"
FPS = 90

uzay = Actor ("uzay")
gemi = Actor ("gemi",(300,350))
dusmanlar = []
mod = "oyun"

for i in range(5):
    x = random.randint(20,580)
    y = random.randint(-300,-50)
    dusman = Actor("düşman",(x,y))
    dusman.speed = random.randint(2,7)
    dusmanlar.append(dusman)

def yeni_dusman():
    x = random.randint(20,580)
    y = -50
    dusman = Actor("düşman",(x,y))
    dusman.speed = random.randint(2,7)
    dusmanlar.append(dusman)
    
def draw():
    if mod == "oyun":
        uzay.draw()
        gemi.draw()
        for i in range(len(dusmanlar)):
            dusmanlar[i].draw()
    elif mod == "son":
        uzay.draw()
        screen.draw.text("Oyun Bitti",pos = (200,200),color = "red", fontsize = 40)

def on_mouse_move(pos) : 
    gemi.pos = pos

def dusman_gemisi():
    for i in range(len(dusmanlar)):
        if dusmanlar[i].y < 450:
            dusmanlar[i].y = dusmanlar[i].y + dusmanlar[i].speed
        else:
            dusmanlar.pop(i)
            yeni_dusman()
            break
            
def carpisma():
    global mod
    for i in range(len(dusmanlar)):
        if gemi.colliderect(dusmanlar[i]):
            mod = "son"

def update(dt):
    global mod
    dusman_gemisi()
    carpisma()****
