# learnpro
# I wrote the code while I was studying

# -*- coding = utf-8 -*-
import random

legal_x = [0, 10]
legal_y = [0, 10]

class Turtle:
    def __init__(self):
        self.power = 100       # 初始体力
        self.x = random.randint(legal_x[0], legal_x[1])    # 初始随机位置
        self.y = random.randint(legal_y[0], legal_y[1])

    def move(self):
        new_x = self.x + random.choice([1, 2, -1, -2])      # 随机计算方向并移动到新位置
        new_y = self.y + random.choice([1, 2, -1, -2])
        if new_x < legal_x[0]:                             # 计算是否超出位置
            self.x = legal_x[0] - (new_x - legal_x[0])
        elif new_x > legal_x[1]:
            self.x = legal_x[1] - (new_x - legal_x[1])
        else:
            self.x = new_x
        if new_y < legal_y[0]:
            self.y = legal_y[0] - (new_y - legal_y[0])
        elif new_y > legal_y[1]:
            self.y = legal_y[1] - (new_y - legal_y[1])
        else:
            self.y = new_y
        self.power -= 1                 # 移动一次体力减一
        return (self.x, self.y)

    def eat(self):
        self.power += 20
        if self.power > 100:
            self.power = 100

class Fish:
    def __init__(self):
        self.x = random.randint(legal_x[0], legal_x[1])  # 初始随机位置
        self.y = random.randint(legal_y[0], legal_y[1])

    def move(self):
        new_x = self.x + random.choice([1, -1])     # 随机移动一步的位置
        new_y = self.y + random.choice([1, -1])
        if new_x < legal_x[0]:                      # 计算x轴是否超出边界
            self.x = legal_x[0] - (new_x - legal_x[0])
        elif new_x > legal_x[1]:
            self.x = legal_x[1] - (new_x - legal_x[1])
        else:
            self.x = new_x
        if new_y < legal_y[0]:                      # 计算Y轴是否超出边界
            self.y = legal_y[0] - (new_y - legal_y[0])
        elif new_y > legal_y[1]:
            self.y = legal_y[1] - (new_y - legal_y[1])
        else:
            self.y = new_y
        return (self.x, self.y)

turtle = Turtle()
fish = []
for i in range(10):
    new_fish = Fish()
    fish.append(new_fish)

while True:
    if not len(fish):
        print('鱼儿都被吃完了!')
        break
    if not turtle.power:
        print('乌龟体力用光了！')
        break

    pos = turtle.move()
    for each_fish in fish[:]:
        if each_fish.move() == pos:             # 鱼儿被吃了
            turtle.eat()
            fish.remove(each_fish)
            print('有条鱼儿被吃了')
