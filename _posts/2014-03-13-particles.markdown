---
layout: post
title:  "Particular"
subtitle:  "Creating art with code, a Processing adventure"
date:   2014-03-13
categories: Processing Particles
name: "particular"
color: "#2980b9"
link: https://www.khanacademy.org/cs/particular/5469568509149184
---

Particular is an processing experiment. 

I recently discovered processing, a programming language, development environment, and online community. Processing serves as a software sketchbook. Programs written in this medium are called sketches because they are experimental pieces of algorithmic art. Much as you would sketch with a pencil on paper, i decided to write some sketches in this java enviornment. The result is this.

I implemented a very simply particular system with 10,000+ nodes each having their own characteristics. Interactions on the canvas bring the particles to life. Using some basic physics, the effect i got is incredibly dramatic and smooth. I haven't experienced such immediate gratification since discorvering mandelbrot and julia sets in grade 10. 

{% highlight java %}
void setup(){
  size(1080, 640 , P2D);
  stroke(245,236,217);
  mParticles = new ArrayList<Particle>();
  
  for(int i = 0; i<PARTICLES; i++){
    Particle particle = new Particle();
    particle.x = random(1)* width ;
    particle.y = random(1)* height ;
    particle.dx = 0;
    particle.dy = 0;
    particle.lastX = particle.x;
    particle.lastY = particle.y;
    mParticles.add(particle);
    particle.colour = color(245,236,217);
  }
}

void draw(){
    fill(59,59,59,100);
    noStroke();
    rect(0, 0, width, height);

    Float angle;
    for(Particle particle : mParticles){
      particle.lastX = particle.x;
      particle.lastY = particle.y;
    
      angle = atan2( particle.y - mouseY, particle.x - mouseX );
      particle.dx -= SPEED * cos(angle);
      particle.dy -= SPEED * sin(angle);
      particle.x += particle.dx;
      particle.y += particle.dy;
      particle.x *= 0.97;
      particle.y *= 0.97;
      stroke(particle.colour);


      line( particle.lastX, particle.lastY, particle.x, particle.y);
    }
}


void mouseClicked() {
  float randAngle;
  float randPower;
  for(Particle particle : mParticles){
    randAngle = random(1)* PI*2;
    randPower = random(1)* POWER/2;
    particle.dx += randPower * cos(randAngle);
    particle.dy += randPower * sin(randAngle);  
  } 
}
{% endhighlight %}

Proccessing turned out to be very popular. it has a javascript port which makes it easy to share sketches on the web. Khan Academy's programs written by students also uses a variation on processing.js for their online programming exercises. I decided to port my java version here as well. 