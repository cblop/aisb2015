class: center, middle, inverse
layout: true

---

# Every Object Tells a Story
Matt Thompson, University of Bath & Sysemia Ltd

<!-- punch and judy image -->
<!-- ![Default-aligned-image](img/punchJudy.png) -->

---
layout: false

# About the project

Collaboration between:

- University of Bath
- Sysemia Ltd, Bristol
- Bishop's Palace, Wells

TSB-funded feasibility study

---
layout: false
# Generative narratives

- No pre-written story or narrative exists.
- The narrative emerges as a result of a series of complex interactions in the game.
- This tends to happen in sandbox-style, open-world games
- Examples: Minecraft, Civilisation, Dwarf Fortress

---

## Interactive (non-linear) narratives

- The narrative is pre-written with several branches
- Player's interactions decide which branches play out
- Usually implemented as multiple endings in games
- Examples: Choose Your Own Adventure, Mass Effect, RPG games

---
class: inverse, center, middle
# Have any games done both?

---

# Galatea

- interactive fiction/text adventure
- one character, one room
- story emerges from conversation

---
class: center, middle, inverse
background-image: url(img/facade.jpg)

---
# Façade

- created by Mateus and Stern at Georgia Tech .red[*]
- only one room, two (other) characters
- interact by typing in natural language sentences


.footnote[.red[*] Mateus and Stern - Facade: An Experiment in Building a Fully-Realized Interactive Drama]

---

class: center, middle, inverse

# How do you model a narrative?

---
class: center, inverse
background-image: url(img/shapes.png)

---

# Vladimir Propp

- created a formalism for Russian folk tales
- split stories into series of sequences
- generalises to other stories quite well

---
# Vladimir Propp

- 7 character functions (hero, villain, helper, etc)
- 31 story functions, for example:
	- STRUGGLE: Hero and villain join in direct combat
	- UNRECOGNIZED ARRIVAL: Hero unrecognized, arrives home or in another country


---
class: center, middle, inverse

# How to make a generative, interactive narrative

---


# How Facade does it

- Based on OZ project drama manager
- Dramatic elements are divided into 'beats'
- Agents interact with each other
- Story is guided by the drama manager

---
class: center, middle, inverse

background-image: url(img/punchjudy.png)
# That's the way to do it!

---

# Punch and Judy

- Start with an animation
- Very simple to model
- Limited number of characters
- Characters are pretty simple

---
# Implementation

- narrative ontology
- multi-agent system (BDI)
- logical reasoner
- drama manager

---
# Propp-inspired formalism

- 8 characters (Punch, Judy, Baby, Clown, Policeman, Monkey, Crocodile, Devil)
- 7 possible scenes (babysitting scene, policeman scene, sausages/crocodile scene, etc)
- Narrative shape is generally climactic
- Agents' behaviour changes the outcome of these scenes

---
# RDF ontology

- This formalism is described using the RDF format
- Ideal for capturing relations and semantics
- Can use Semantic Web tech (reasoners)

---
# Characters and emotion

Each character has a main emotional attribute, and a health component.

- Punch: anger
- Policeman: suspicousness
- Clown: happiness

Their behaviour changes according to an emotional score from 1 - 10.


---
# Interaction

We want to mimic audience participation similar to real P&J shows:

- Agents react to noise in environment
- Interaction with smartphones

---
# Uses

- games
- training simulations
- interactive exhibitions


---
class: middle, inverse

# Questions

