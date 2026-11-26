# Asteroids

A classic arcade-style space shooter written in Python with pygame. Fly a
ship around the screen, shoot incoming asteroids, and split the big ones
into smaller pieces before they hit you. Built as a guided project in
[boot.dev](https://www.boot.dev)'s backend developer path.

<!-- Add a screenshot or short GIF of the game here, for example: -->
<!-- ![Asteroids gameplay](docs/gameplay.gif) -->

## Features

- A triangle ship that rotates, moves forward and backward, and fires shots
- A short cooldown between shots, so you can't fire nonstop
- Asteroids in three sizes that spawn from a random screen edge every 0.8 seconds
- Hitting a large or medium asteroid splits it into two smaller, faster ones
  flying off at random angles; the smallest ones are destroyed
- Circle-based collision detection between the ship, shots, and asteroids
- Game over when an asteroid hits the ship
- Frame-rate independent movement, capped at 60 FPS

## Controls

| Key | Action |
| --- | --- |
| W / S | Move forward / backward |
| A / D | Rotate left / right |
| Space | Shoot |

Close the window to quit.

## Built with

- Python 3.13
- [pygame](https://www.pygame.org) 2.6.1
- [uv](https://docs.astral.sh/uv/) for the virtual environment and dependencies

## Run it

With uv:

```bash
git clone https://github.com/jwahbeh/asteroids.git
cd asteroids
uv run main.py
```

Or with pip and a virtual environment:

```bash
git clone https://github.com/jwahbeh/asteroids.git
cd asteroids
python3 -m venv .venv
source .venv/bin/activate
pip install pygame==2.6.1
python3 main.py
```

## What's in here

- `main.py`: sets up pygame, runs the game loop, and checks collisions
- `circleshape.py`: `CircleShape`, the base class every game object inherits from (position, velocity, radius, collision check)
- `player.py`: the ship, its controls, and shooting
- `asteroid.py`: asteroid movement and splitting
- `asteroidfield.py`: spawns asteroids from the screen edges on a timer
- `shot.py`: the bullets
- `constants.py`: screen size, speeds, sizes, and timings in one place
- `logger.py`: writes game state and events to local `.jsonl` files

## How it works

Every object in the game is a pygame sprite that inherits from
`CircleShape`. The main loop puts each object into sprite groups
(`updatable`, `drawable`, `asteroids`, `shots`), so each frame it can call
`update(dt)` and `draw(screen)` on whole groups at once instead of
tracking every object by hand. Movement is scaled by `dt`, the time since
the last frame, so the game runs at the same speed on any machine.

## What I learned

- Building a real-time game loop: handle input, update state, draw, repeat
- Object-oriented design with a shared base class and inheritance
- Using pygame sprite groups to manage many objects cleanly
- Vector math for rotation, movement, and aiming with `pygame.Vector2`
- Simple collision detection by comparing distance to combined radii
- Keeping tunable values in a constants module
- Managing a Python project and its dependencies with uv and `pyproject.toml`
