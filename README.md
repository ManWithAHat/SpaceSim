# SpaceSim

<p>SpaceSim is a simple simulation of the inner solar system (Earth,Mars,Mercury and Venus). SpaceSim uses real life data of planets, aside pixel radius, down to scale in order to provide an accurate simulation.</p>

```
class Planet:

    AU = 1.496e+11
    G = 6.67428e-11
    SCALE = 200/AU
    TIMESTEP = 3600 * 24

    def __init__(self,x,y,radius,color,mass):
        self.x =x
        self.y = y
        self.radius = radius
        self.mass = mass
        self.color = color

        self.orbit = []
        self.sun = False
        self.distance_to_sun = 0

        self.x_vel=0
        self.y_vel = 0

    def draw(self,win):
        x = self.x * self.SCALE + WIDTH/2
        y = self.y * self.SCALE + HEIGHT/2
        pygame.draw.circle(WIN,self.color,(x,y),self.radius)
    def attraction(self,other):
        other_x,other_y = other.x,other.y
```

this is the basic object of a planet. The draw functions simply draws the planet position to the sun (Center of window) and the and the attraction functions calculates the x and y velocity of the planets using Newtons law of gravity.
