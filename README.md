# visualization-of-the-diffusion-process-using-the-p5js-service

This is a learning task on using JavaScript visualization on the p5js platform

## Diffusion of two substances

This code visualizes the diffusion process between two substances, represented as separate particles, using the library p5.js for rendering.

## Description:

The simulation shows how two substances (green and orange particles), initially separated by a clear boundary, gradually mix with each other due to the random movement of the particles.

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
**Slider “Viscosity"** : Controls the resistance to movement by influencing the diffusion rate.

## Technical details:

The random() function is used to create random values.
The ellipse() function is used to draw particles as circles.
The translate() function is used to shift the coordinate system.

## Goal:

Visualize the basic principle of diffusion: mixing of substances due to the random movement of particles, resulting in a more uniform distribution.
