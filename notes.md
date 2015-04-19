# AISB talk notes

## 1
OK, so hello. I'm Matt Thompson, an EngD student based at the University of Bath and a company called 'Sysemia Ltd' in Bristol. Today I'm presenting a paper on an interactive, generative Punch and Judy show we made to test out some new ways of making interactive narratives. The main techniques used were institutions, answer set programming and belief desire intention agents with emotional models.

## 2
So here's what to expect from this talk. First I'll explain what Punch and Judy is, for the people that don't know. Then I'll talk about the narrative model we used to describe the Punch and Judy story world. Then comes a description of how we adapted this formalism into an institutional model implementing the story as a set of social norms. Then how we used ASP to reason about the story and what norms apply at any given time. Then comes a description of the agents' emotional model. Finally, I'll describe the architecture of the system and how all these components fit together.

## 3
Now, if you're not from the UK you might not be familiar with what a Punch and Judy show is. It's a puppet show that dates back to before the 17th century. There isn't much of a story - it's basically about a tyrant called Punch who goes around beating people up with a stick. It starts with him killing his wife and child, and goes downhill from there really. He eventually picks bigger and bigger targets, killing a policeman who comes to arrest him and finally the devil himself. There's no moral at all: it's just a really over-the-top violent farce. It's actually a show for children, and kids in the audience are encouraged to cheer or boo along with the action.

## 4
So, why use this puppet show as a way of exploring ways of implementing interactive narrative? Well, it makes a very good starting point as it's a really simple story domain. Both the story and the characters in it are very simple and easy to model. Each Punch and Judy show is always slightly different, though the main scenes are generally the same. Finally, audience interaction is encouraged, which gives us a handy way to change the course of the narrative.

## 5
In order to model the story world of Punch and Judy, we looked to the field of narratology. While there are more recent and sophisticated formalisms of narrative, we decided to use one created in 1928 by Russian structuralist Vladimir Propp. His formalism was actually created for Russian folktales, but generalises reasonably well to most kinds of story. We decided on Propp's model mostly because of its simplicity, which is ideal for Punch and Judy.

## 6
Propp's formalism describes 31 _story functions_, which are events that move the story onwards. Propp said that any Russian folktale can be described by combining these story function. For example, the _absentation_ function is when a family member leaves home, leaving the hero on their own. Before they leave, though, they usually issue an _interdiction_: a kind of warning that they should or shouldn't do something. For example, an interdiction could be not to go into the woods and pick the mushrooms. Or it could be to watch the family dog to make sure they don't escape.
_Complicity_ is when the villain manages to trick someone into believing them about something, perhaps forcing them to go against the hero.
_Villainy_ is a bit general, but Propp defined 19 different types of villainous acts, including the villain abducting someone, seizing the daylight or commiting an act of cannibalism!

## 7
So, for example, we could describe the scene in Punch and Judy with the sausages and the crocodile using Propp's story functions:

1. First, Joey tells Punch to look after the sausages. That's an interdiction.
2. Punch agrees, and Joey goes along with it, being complicit in his plan.
3. This is where we're stretching Propp a little bit, saying that the sausages are a magical agent that Joey gives to Punch.
4. Joey leaving the stage counts as an _absentation_ Propp move. 
5. Then, when the crocodile comes in and eats the sausages, this _violates_ Punch's promise to protect them.
6. The _struggle_ function happens when Punch fights the crocodile.
7. When Joey returns to the stage, he finds the sausaages are gone, which fits Propp's _return_ function.

## 8
OK, now I'll talk about how we implemented these Propp functions as a set of social norms using an institutional model. Essentially, we've described what each agent is permitted or obliged to to at any point in time in the story. The Propp functions initiate or terminate these permissions or obligations.

## 9
Institutions consist mostly of two things: events that happen at some point, and fluents, which are properties that hold to be true or false at a point in time. Agents trigger _external events_, _internal events_ happen inside the institution and _violation events_ happen when an obligation is violated. The _internal events_ are where we implement our Propp functions.

## 10
So, here we have some examples of types of events. External events are actions the agents perform (list), internal events are the Propp story functions, violation events are events that happen when these story functions are violated, when an agent does something to break the mold of the story.

## 11
Fluents are the other type of information that an institution describes. They're just properties that are true or false at a certain instant in time.
So, some examples would be to describe the properties of the puppet agents at the current point in time: they could be on stage, off stage, they could be heroes or villains, alive or dead, they might not even be characters, they could be items. 

## 12
Permissions describe the external actions that agents are permitted to perform at some point in time. These are kind of like the options available to them at any point.

## 13
Obligations are actions that agents are supposed to do before a certain point in time, otherwise a violation event gets triggered. The violation event usually punishes the agent in some way. For example, it can lower the dominance of the agent in our emotional model, kind of like 'You don't want to follow the story? Fine, you get less influence in it.'. For example, an agent might have to leave the stage before a struggle occurs. If they haven't, the violation event for the struggle function is called.


## 14
External events trigger internal events _if_ a set of preconditions hold. For example, if the _interdiction_ story function is currently active and Punch eats the thing he's supposed to be protecting, then the _violation_ event is triggered.
Likewise, permissions and obligations are initated and terminated as consequences of internal events. For example, Joey leaving the stage and triggering the _absentation_ event would give the crocodile permission to enter the stage, and the obligation to eat the sausages before Joey returns.

## 15
Next I'll explain how we use Answer Set Programming (ASP) to specify and implement the institutional model.

## 16
We have a DSL for specifying institutional models, called 'InstAL'. It's based on the situation and event calculi, and compiles to the AnsProlog language, which is an implementation of ASP. We use it to describe when events are generated, and when permissions and obligations are initiated and terminated.

## 17
(read slide)

## 18
(read slide)

## 19
We use the clingo solver to reason about the events that have happened so far, which are sent to it as a query. Querying against the institution specification, the output is which fluents hold at what times.

## 20
So the entire sausages and crocodile scene, when compiled from InstAL to ASP, would look like this in AnsProlog. If you're familiar with the Event Calculus, it kind of resembles that. The useful part is the holdsat predicates saying what fluents hold at certain instants in time.

## 21
Our characters are modelled as Belief Desire Intention agents in a multi agent system. In addition, we give them an emotional model, based on Russell's circumplex psychological model from 1980. This model describes three variables that affect emotion: valence (or positivity), arousal and dominance. Like with Propp, this isn't the most sophisticated emotional model around, but we found that its simplicity was a good match for the P&J story world.

## 22
So, quickly, here are the spectrum of emotions for low dominance.

## 23
(med dominance)

## 24
(high dominance)

## 25
So, how do we link all of these components together?

## 26
We're using the Bath Sensor Framework to decouple the agents from their environment. Using the XMPP publish/subscribe protocol, the components connect to a central server and are pushed the changes when they happen.

In this case, we're using a BDI agent framework called JASON, which is implemented in Java and where you describe your agents using a DSL called AgentSpeak. The institions are written in InstAL and compiled to AnsProlog, which is solved using the clingo solver. All of this is managed and run using a program written in Clojure. The puppet animation is written in Coffeescript and WebGL and runs in a web browser. All of these components communicate using the XMPP instant messaging protocol.

## 27
The permissions and obligations that hold at the next instant in time are added to the agents as percepts. They then plan their next actions based on these norms. The basis for their decision is their emotional state and their goals.

In times of extreme emotion, an agent may deviate from the norms suggested by the narrative. For example, a furious Punch might beat up Joey instead of accepting the sausages from him. Alternately, a depressed Punch may just give up and leave the stage.






