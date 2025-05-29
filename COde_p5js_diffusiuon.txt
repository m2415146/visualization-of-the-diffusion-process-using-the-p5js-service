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