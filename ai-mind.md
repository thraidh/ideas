# Overview

Thoughts about building a really good NPC AI.
Basic idea: have different subsystems which are completely different, but work
together somehow, instead of having one unifying underlying system.

# systems

- planner, backwards inference
- planner, forward inference
- planner with antagonist (try to thwart original plan)
- motivations (provide goals without external triggers)
- ethics and sympathy (check goals for acceptability)
- routine planner (try to find a plan just by checking upon previously done tasks)
- plan memory (remember when goals popped up, what triggered the goal, what plan was made to meet that goal)
- action/event memory (remember what happened when, link to plan memory)
- expectations (predict what will happen from memory)
- simulator (use forward planner to predict what other people will do and infer goals)
- internal sensors (make events from things happening within)
- external sensors (detect what happens around you and make events/sentences from that)
- pattern detector (turns event memory into plan steps, trying to find patterns like "alice enter the house"+"bob enters the house"->"X enters the house")
- generalizer (tries to group objects based on same behavior/same actions: "alice enters"+"bob enters"->person=[alice,bob] -> "X:person enters")
- related stuff (object-objects, object-rules, object-memories, object-emotions) (if I say X, whay comes into your mind?) (limit planner mostly to those things)
- recursive knowledge (what do I know, what do I think about what X knows, what do I think about what X knows about Y (including me))


# planner elements

A -> B (A always leads to B)
A => B (A is required for B, but does not necessarily lead to B)

each rule can be connected to an emotion with value and a general "want" value. when the mind is in the same emotion, it would prefer rules connected to that emotion, where high emotion with high rule emotion will have a high chance to be picked.
"want" can be negative to indicate that the mind doesn't want that, but it could be that a negative "want" (or "logic"?) is overridden by a high "fear" value, which make the mind to choose this rule anyway

## Planning

The planner uses its knowledge about states and rules to plan actions or simulate the future.
These rules are not used to simulate the world, as the known rules could differ from the actual rules which make up the world.

## Action

An action is something which a person or group does, which may or may not succeed. If it succeeds it leads to an event of the same name.
An action may fail if prereqs are not met or by chance.
If an action fails the associated event does not happen.

## State S0, Event A, State S1 leads to B

S0 is state before A, S1 after A. If there is no A, the current state is used.

B can be one or more of:
- state change
- goal change
- temporary or permanent rule (might be bound to some memory, which might become false, invalidating this rule)
    or not? maybe rules should be bound to memories when someone says something also bound to some emotion
    but there should be rules, so that the ai can reason about giving rules to other people

Several modes:
- left side always and automatically leads to right side, because it is a definition or axiom or left side implies right side (l =: r, r := l)
- left side (almost) always is followed by right side (it's a rule, but there might be exceptions) (l -> r, r <- l)
- left side can be followed by right side (unknown factors/chance may be involved to decide whether it leads to or not) (l --> r, r <-- l)
- left side is required for right side, but does not (necessarily) lead to right side (l :> r, r <: l)


## Process X is, when S0, E1, S1, ... En, Sn are met




# emotion system

increase/decrease certain emotions when specific actions happen. these actions can have additional conditions.

when simulating, we need to calculate how probably that goal would be. then
we can calculate what potential emotion changes there are and how probable these are.

potential X generates Y

- sadness -> fear
- pain -> fear
- happiness -> anticipation

every mind has different rates how each emotion is increased or decreased.

alice: fury +10 -10 -> alice gets furious fast, but cools off fast, too

bob: sadness +10 -5, fear +1 -1 -> bob gets sad fast and stays sad longer, but is not very prone to fear


example:

action: X is dead
condition: Y likes X
desire: negative
emotion: increase(Y.sadness)

action: Z kills X
condition: Y likes X
desire: negative
emotion: increase(Y.sadness, times-two), decrease(Y.likes[Z], times-two), increase(Y.revenge)



- concept of ownership (vs. legal ownership)
- concept of loss
- concept of subjective value of an object/role/idea/place/concept (the triple-bladed sword is mine, because i invented it: ah, i see that you carry my sword; but i don't feel that the actual object belongs to me)
- concept of organizational identification (I feel that I am part of a group: I am a paladin)
- concept of organizational commitment (I want to be a paladin because I support the motivations/values of paladins, but I don't want to be a Dark Elf since they believe in killing and I don't like that)




# planner sample rules
goal: king is dead

goal for K:king: K.money+=V

Badking:king owns Goldmine:mine.
Goldmine produces Gold.

X has Y, P.money>=V :> X sells Y to P for V
    state, state (is prereq for) action
X sells Y to P for V -> P has Y, P.money-=V, X.money+=V
    action (leads to change of) state, state, state
     
X owns M:mine, Y works in M, M produces G -> X has G
    state, action, state (leads to change of) state

X kills Y -> Y is dead
    action (ltco) state
X is poisoned -> X dies
    state (implies) state
X dies, time passes -> X is dead
    state, action (ltco) state

X dies, X is poisoned, X drinks anti-poison -> not(X dies)
    state, state, action (ltco) state

X hits Y with Z:weapon -> Y.health -= V
    action (ltco) state
Y.health <= 0 -> Y is dead
    state (implies) state

distance(X.location, Y.location) < Z.range, X has Z:weapon, X can use Z => X hits Y with Z:weapon
    state, state (is required for) action
    
X picks up Y -> X has Y:object
    action (ltco) state
A has Y, A gives Y to X -> X has Y:object
    sa>s
X steals Y from A -> X has Y:object
    a>s
X makes Y:object -> X has Y
    a>s

A has Y, something happens, not(A has Y) -> A loses Y
    state @ t1, event, state @ t2>t1 (defines event) event
A loses Y, something happens, A has Y -> A gets-back Y
    event @ t1, event @ t2>t1, state @ t3>=t2 (defines event) event
    
A gets-back Y -> A.fury-=5
    event (can lead to changed) state
    actually this particular rule is more about emotion and counter-acting the results of loss
    but there needs to be a rule in the knowledge base so that the ai knows how to reduce fury
    actually getting something back does not reduce fury, but removes the reason for the fury, so it should be phrased differently

A has Y, A notices-theft of Y-> A cries alarm, A.fury+=10, A.add-goal(A gets-back Y; A.fury), A.add-goal(S punishes X; A.fury)
    state@t1,event@t2>t1 (causes reaction) action, state change, goal change, goal change
    this is a hard one
    what actually happens:
        A has X
        A notices theft
        A has a sense of loss about X
            if it is high, an emotional reaction to that loss happens -> sadness, fury
            infer the cause of that loss
            also an emotional reaction to the cause of that loss happens -> fury, revenge
            if it is low, no reaction to the loss or cause of loss happens (if someone steals a paper tissue from you, that doesn't upset you a lot)
        anyway, theft implies, that there is a thief
        theft triggers an emotional reaction -> injustice
        injustice against me makes me like the cause/actor/related person of injustice like less and triggers emotional reaction against that person -> hate, fury, revenge
        injustice against anyone else triggers sympathy rules
            depending on my connection to that anyone, I feel like it happened to me
        revenge makes me want the target of my revenge to be punished (if feeling of revenge fades, the need of punishment fades, too)
        since "guard notices thief T -> ... -> X punishes T", we need to make guard notice the thief
        to do that pull attention to us by screaming or waving
        then redirect attention to the thief by pointing
        why not punish the thief on your own?
            - need to catch him first and maybe i can't or probability not high
            - need to overpower him and maybe i'm weaker and can't punish him
            - punishing him is unlawful and i'm too lawful to do that
            - punishing him is unlawful and i might be punished for that
                - i follow that line of thought because (un)lawfulness is strongly connected punishing someone and unlawfulness (maybe) activates fear of punishment or imprisonment


X attempts-to-steal Y from A, Y.secured-level < X.thievery-attention-level(A,X) -> X steals Y from A
X attempts-to-steal Y from A, Y.secured-level >= X.thievery-attention-level(A,X) -> X steals Y from A, A notices-theft
X attempts-to-steal Y from A, Y.secured-level >= X.thievery-attention-level(A,X) -> X steals Y from A
X attempts-to-steal Y from A, Y.secured-level >= X.thievery-attention-level(A,X) -> A notices-theft
    these are about possible outcomes on success or failure
    "X steals Y from A" requires "Y.secured-level < X.thievery-attention-level(A,X)" to be successful
        failed(X steals Y from A) (can lead to) event(X takes Y from A)
        failed(X steals Y from A) (can lead to) event(A notices-theft)
        


X asks Y for G -> add-goal(Y; G; favor), X.owes[Y]++
    action (causes change of) goal, state
X intimidates Y for G with T, (T -> Y.fear+=V) -> add-goal(Y; G; Y.fear), Y.fear+=X.indimidation, add-rule(Y; not(G) -> T; Y.fear)
    action (with additional qualifier) (causes change of) goal, state, rule

X.health-=H -> X.fear+=V
Y is dead; X likes Y -> X.fear+=V
Y.health-=H; X likes Y -> X.fear+=V
Z is destroyed; X owns Z -> X.fear+=V
Y has Z; X owns Z, not(X likes Y) -> X.fear+=V
    rules about fear, but these are actually wrong. see above about potential X leads to Y
    the actual rules are covered by the emotion system, but there need to be rules anyway, so that the ai can reason about that
    some of these rules actually have a prerequisite, which the reasoner uses, but does not try to make true
    otherwise
        goal: X.fear increases
        rule: Z is destroyed, X owns Z -> X feels loss
        rule: X feels loss -> X.fear increases
        planner tries to make rule become true by threatening to declare that this flower now belongs to X and destroy it afterwards
        which would be hilarious, but not realistic
        also not good:
        rule: Z is valuable to X, Z is destroyed -> X feels loss
        planner would threaten to try to find a Z that is valuable to X or produce a Z and engineer it to be valuable to X and destroy it
        better:
        rule: Z is destroyed -> X feels loss
        rule: Z is valuable to X (is prereq for) (Z is destroyed -> X feels loss)
        planner now tries to find a chain which leads to "X.fear increases", and finds one which does not directly include the prereq, so it can threaten with "Z is destroyed", but as the rule is only eligible if the prereq is met, it has either to find vars so that it is true or make it true
        


X can make Y => X makes Y:object

X knows how to make Y,
X has all resources for Y,
X follows process for making Y -> X can make Y

for each I: I is resource for Y, X has I -> X has all resources for Y

X:smith knows how to make Y:made-of-metal.


X is a [smith], Y is [made of metal] =: X knows how to make Y.
    if a person is a smith, he probably knows how to make something which is made out of metal

Y:sword =: Y:made-of-metal
Y:sword =: Y:weapon



I:metal is resource for Y:sword.

X has M:metal-bar, X heats M, X hammers M -> M.height--
X has M, M:metal-bar.height = 3, X sharpens M -> convert(M, S:sword), X follows process for making S:sword

X has M, X holds M in F:fire -> X heats M
X puts M on A:anvil, X uses H:hammer on M -> X hammers M

X has Y -> Y.location = (on-person X)

# forward inferencer

# antagonist planner

- planner with antagonist (try to thwart original plan)

# motivations

- motivations (provide goals without external triggers)

# routine planner

- routine planner (try to find a plan just by checking upon previously done tasks)

# plan memory

- plan memory (remember when goals popped up, what triggered the goal, what plan was made to meet that goal)

# event memory

- action/event memory (remember what happened when, link to plan memory)

# expectations

- expectations (predict what will happen from memory)

# simulator

- simulator (use forward planner to predict what other people will do and infer goals)

# internal sensors

make events from things happening within
- hunger
- pain
- ...

# external sensors

detect what happens around you and make events/sentences from that
- what i see 
    - trigger spatial reasoning about that
- what i hear
- what i feel
- direct attention to loud noises, movements etc

# pattern detector

turns event memory into plan steps, trying to find patterns

simple:
- "alice enter the house"+"bob enters the house"->"X enters the house"
- people can enter buildings

complex:
- jim unsheathes sword + jim uses sword on jack + jack screams + jack is dead
- make rules:
    X unsheathes W --> X uses W on P
    X unsheathes W --> P screams
    X unsheathes W --> P is dead
    X uses W on P --> P screams
    X uses W on P --> P is dead
    P screams --> P is dead
- these rules are put into "potential rules" area
- when the same rules are entered again a number of times, they are moved to "general knowledge" area
- when there are rules to be checked all areas are considered

# generalizer

tries to group objects based on same behavior/same actions: "alice enters"+"bob enters"->person=[alice,bob] -> "X:person enters"

# relations

object-objects, object-rules, object-memories, object-emotions
- if I say X, whay comes into your mind?
- limit planner mostly to those things


# fact and rule knowledge retrieval

- generel knowledge (things that everyone knows, common sense)
- group knowledge
    - all things a group of related people know (all smiths, all paladins, all citizens of a town, ...)
    - a person can be a member of several groups at once
- personal knowledge (built/infered from memory)
- what person X knows
    - based on general knowledge
    - group knowledge (as far as I know about those groups)
    - what I know about X, i.e. shared memory, what other people told me about X

# focus

mind focuses on a person, object or process. predictions/simulations will mainly be done about the focused thing and things which interact with the focused things.

the mind can focus on a very limited number of things, mainly those which the maind can sense (mostly see).

the mind can focus on one or more internal goals, plus one or maybe two sensed things.

sudden noises, flashes or unusual touches, etc will move the focus. unusual touches are stronger or unexpected. expected touches are touches of the same strength and locations as those in the immediate past (eg. while moving through a crowd, simple jostling won't pull focus unless the mind is paranoid or in a state of fear).

# spatial awareness

- map world
- backward inference to tell reasons, why something is where it is
- forward inference to tell where things will be
- provide probabilities where things might be
- pattern detection (if there is a fire and an anvil, the location is a smithy)
- generalize locations with probabilities (in a smithy is usually a fire and an anvil, and also a smith and maybe an apprentice. an anvil is seldom found out of a smithy)

 

