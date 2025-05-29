# visualization-of-the-diffusion-process-using-the-p5js-service

This is a learning task on using JavaScript visualization on the p5js platform

## Diffusion of two substances

This code visualizes the diffusion process between two substances, represented as separate particles, using the library p5.js for rendering.

<img width="408" alt="Снимок экрана 2025-05-29 в 09 28 50" src="https://github.com/user-attachments/assets/afb925aa-7f8e-426c-968e-43ed25831c3a" />


## Description:

The simulation shows how two substances (green and orange particles), initially separated by a clear boundary, gradually mix with each other due to the random movement of the particles.


## Code:

```
let particles1 = [];
let particles2 = [];
let numParticles = 100;
let particleSize = 5;

let temperature = 1;
let viscosity = 1;
let initialAttraction = 0.05;
let attractionDecayRate = 0.001;
let penetrationProbability = 0.005;

let temperatureSlider;
let viscositySlider;

function setup() {
  createCanvas(400, 400);
  background(220);

  temperatureSlider = createSlider(0.1, 5, temperature, 0.1);
  temperatureSlider.position(20, 20);

  viscositySlider = createSlider(0.1, 5, viscosity, 0.1);
  viscositySlider.position(20, 50);

  initializeParticles();
}

function draw() {
  background(220, 10);

  temperature = temperatureSlider.value();
  viscosity = viscositySlider.value();

  initialAttraction = max(0, initialAttraction - attractionDecayRate);

  moveParticles();

  translate(0, 80);

  fill(0, 255, 0);
  noStroke();
  for (let particle of particles1) {
    ellipse(particle.x, particle.y, particleSize, particleSize);
  }

  fill(255, 165, 0);
  noStroke();
  for (let particle of particles2) {
    ellipse(particle.x, particle.y, particleSize, particleSize);
  }

  translate(0, -80);

  fill(0);

  text('Temperature: ' + temperature, temperatureSlider.x * 2 + temperatureSlider.width, 35);
  text('Viscosity: ' + viscosity, viscositySlider.x * 2 + viscositySlider.width, 65);
}

function initializeParticles() {
  particles1 = [];
  particles2 = [];

  for (let i = 0; i < numParticles; i++) {
    particles1.push({
      x: random(width / 2 - particleSize * 2),
      y: random(height)
    });
  }

  for (let i = 0; i < numParticles; i++) {
    particles2.push({
      x: random(width / 2 + particleSize * 2, width),
      y: random(height)
    });
  }
}

function moveParticles() {
  let boundaryX = width / 2;

  for (let particle of particles1) {
    let vx = random(-1, 1) * temperature;
    let vy = random(-1, 1) * temperature;

    let distanceToCenter = particle.x - boundaryX;
    vx -= initialAttraction * distanceToCenter / viscosity;

    particle.x += vx / viscosity;
    particle.y += vy / viscosity;

    if(random(1) < penetrationProbability){
      particle.x += random(particleSize*2);
    }

    if (particle.x < 0) particle.x = width;
    if (particle.x > width) particle.x = 0;
    if (particle.y < 0) particle.y = height;
    if (particle.y > height) particle.y = 0;
  }

  for (let particle of particles2) {
    let vx = random(-1, 1) * temperature;
    let vy = random(-1, 1) * temperature;

    let distanceToCenter = particle.x - boundaryX;
    vx -= initialAttraction * distanceToCenter / viscosity;

     if(random(1) < penetrationProbability){
        particle.x -= random(particleSize*2);
     }

    particle.x += vx / viscosity;
    particle.y += vy / viscosity;

    if (particle.x < 0) particle.x = width;
    if (particle.x > width) particle.x = 0;
    if (particle.y < 0) particle.y = height;
    if (particle.y > height) particle.y = 0;
  }
}
```

## Main components:

**particles1, particles2** Arrays that store particle objects for each substance (green and orange). Each object contains the x and y coordinates of a particle.

**numParticles** The number of particles of each substance

**particleSize** The size of each particle (diameter of the circle)

**temperature** A parameter that affects the speed of movement of particles. Higher temperature leads to faster movement

**viscosity** A parameter that affects the resistance to particle motion. Higher viscosity slows down movement

**initialAttraction** The force with which particles are attracted to the interface. This force helps maintain the concentration of particles at the boundary at the beginning of the simulation.

**attractionDecayRate** The rate at which the force of attraction to the center decreases

**penetrationProbability** The probability that a particle will try to penetrate the area of another substance in each frame

## Functions:

**setup()** Creates a canvas for rendering.
Creates sliders to control temperature and viscosity.
Calls initializeParticles() to create and place particles in their initial positions.

**draw()** Cleans the canvas with a slight transparency, creating a “fade-in” effect and visualizing the movement of particles.
Gets the temperature and viscosity values from the sliders.
Reduces initialAttraction by attractionDecayRate each frame.
Calls moveParticles() to update the position of each particle.
It draws the particles of each substance in its own color (green and orange).
Displays the values of temperature and viscosity on the screen.

**initializeParticles()** Creates arrays of particles 1 and particles 2.
Fills each array with particle objects, randomly placing them in the corresponding halves of the screen:
particles 1 (green) - in the left half.
particles 2 (orange) - in the right half.
The initial location of the particles is limited by a small distance from the central boundary.

**moveParticles()** For each particle:
Generates a random speed change (vx, vy).
Calculates the force of attraction to the center and adjusts the speed.
Updates the particle position (x, y) based on velocity and viscosity.
Ensures that the particles do not go beyond the boundaries of the screen.
Implements the logic of penetration: with the probability of penetration, the particle shifts towards the area of another substance.

## Control Sliders: 

**Slider “Temperature"**: Controls the overall velocity of the particles.


https://github.com/user-attachments/assets/0e4bb86c-ab99-4073-9b51-a487683060ff



**Slider “Viscosity"** : Controls the resistance to movement by influencing the diffusion rate.


https://github.com/user-attachments/assets/9e5ee458-589e-49cf-acb9-7b614573409b




## Technical details:





The random() function is used to create random values.
The ellipse() function is used to draw particles as circles.
The translate() function is used to shift the coordinate system.

## Goal:

Visualize the basic principle of diffusion: mixing of substances due to the random movement of particles, resulting in a more uniform distribution.
