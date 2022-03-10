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

        if len(self.orbit) > 2:
            updated_points = []
            for point in self.orbit:
                x,y = point
                x= x* self.SCALE + WIDTH/2
                y = y*self.SCALE + HEIGHT/2
                updated_points.append((x,y))
            pygame.draw.lines(WIN,self.color,False,updated_points,2)
        pygame.draw.circle(WIN,self.color,(x,y),self.radius)
    def attraction(self,other):
        other_x,other_y = other.x,other.y
        distance_x = other_x - self.x
        distance_y = other_y - self.y
        distance = math.sqrt(distance_x**2 + distance_y**2)

        if other.sun:
            self.distance_to_sun = distance
        force = self.G * self.mass * other.mass/distance**2
        theta = math.atan2(distance_y,distance_x)
        force_x = math.cos(theta) * force
        force_y = math.sin(theta) * force
        return force_x,force_y
    def update_pos(self,planets):
        total_fx = total_fy = 0
        for planet in planets:
            if self == planet:
                continue
            fx,fy=self.attraction(planet)
            total_fx+=fx
            total_fy += fy
        self.x_vel+=total_fx/self.mass*self.TIMESTEP
        self.y_vel += total_fy / self.mass * self.TIMESTEP

        self.x+=self.x_vel*self.TIMESTEP
        self.y+=self.y_vel*self.TIMESTEP
        self.orbit.append((self.x,self.y))
```

this is the basic object of a planet. The draw functions simply draws the planet position to the sun (Center of window) and the and the attraction functions calculates the x and y force of the planets using Newtons law of gravity. Update position gets the x and y velocity of the planet and updates it's position based on that
