# train-layout-panel

## turnout

A turnout panel object is composed of two main hardware pieces in addition to the RPi controller

- A button
  - Presses emit an event coded by the Node (MAC address?) and Button IDs so that it is unique
  - Event is a 'transition request'
- A Red/Green LED pair that consumes 3 events
  - Transition request
    - This is initially emitted from the associated button on press
  - Diverging route selected
    - This is emitted from the turnout when it is aligned to the diverging route
  - Main route selected
    - This is emitted from the turnout when it is aligned to the diverging router

On boot the system will request that all routes be set to the main route. There are 3 natural system states with the following behaviours,

- Transition
  - Red/Green LED pair will flash at a 0.5s interval
  - Transition request event is re-emitted at 0.5s interval
- Main
  - Solid green light
  - Off red light
- Diverging
  - Solid red light
  - Off green light

![panel turnout state diagram](https://github.com/geoff-coppertop/python-train-layout-panel/panel-turnout-state-diagram.png)

It would be interesting to serialize the state of each turnout so that on boot this could be de-serialized and requested so that the whole layout doesn't need to be reset