# How the pieces fit together

```
   ┌──────────────┐                 ┌───────────────────────────┐              ┌───────────────┐
   │ WHAT THE FLY │ ──────────────► │       MY BRAIN            │ ───────────► │  FLY BODY     │
   │ SENSES       │   where the     │  learned input stage      │  one walking │  simulator's  │
   │              │   target is,    │            ↓              │  command per │  own walking  │
   │ target,      │   what is in    │  nerve-cord circuit from  │  side of the │  controller   │
   │ obstacles,   │   the way, how  │  a real fly connectome    │  body        │  → legs       │
   │ own motion   │   it is moving  │  (~5,000 neurons, wiring  │              │  → physics    │
   └──────────────┘                 │   fixed, not learned)     │              └───────────────┘
          ▲                         │            ↓              │                      │
          │                         │  left / right leg-muscle  │                      │
          │                         │  pools                    │                      │
          │                         └───────────────────────────┘                      │
          └───────────  the fly moves, the world changes, sense again  ◄────────────────┘

   The boxes on the left and right are the open-source simulator, unmodified.
   Only the middle box is mine.
```

**The simulator** is FlyGym / NeuroMechFly v2: a physics model of a fruit fly built from a
micro-CT scan, with its own walking controller that turns a simple "how hard to drive each
side" command into coordinated leg motion. I did not change any of it.

**The middle box** is the part I built. It takes what the fly can sense about its
surroundings and decides how to drive each side of the body. In the experimental version,
that decision passes through a circuit whose wiring is copied from a real fruit-fly
connectome: a map of actual neurons and the connections between them, measured from
electron-microscope images of a real nerve cord. The wiring is fixed. Only a small number
of strengths around it are learned.

**Training** is evolutionary: many slightly different brains are tried each round, the
better ones steer the next round, and nothing is hand-programmed about how to steer.

Implementation details (what exactly the fly senses, how the scoring works during
training, the internals of the learned stages) are deliberately left out of this folder.
