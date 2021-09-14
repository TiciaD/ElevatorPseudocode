# Pseudocode for an Elevator System
## Functionality

**Main Goal**: Passenger should be able to input whether to go up or down to call the elevator. The elevator should go to their floor, open its doors to allow them on and the passenger can then input which floor they'd like to go to. The elevator should take them to their destination while also picking up and dropping off other passengers efficiently along the way.

### **Things to Keep in Mind**
* If the passenger puts in more than one floor number, the elevator stops at the floor it's currently closest to first then heads to the next closest selected floor.
* If a passenger has called the elevator between the floor the elevator is on and its destination, then it will stop on that floor along the way to pick up the extra passenger before reaching the destination.
* The doors of the elevator can only open if the elevator is at a standstill NOT while it's in up or down motion.
- Is the elevator currently going up or down, when a new passenger calls it?
- If people keep inputting higher floor numbers, when does the elevator stop going up and start going down to pick up passengers on the lower floors?

## Objects
1. Elevator
    * When given a destination, the elevator should move either up or down to reach it and when it arrives go to a standstill
2. Doors
    * Doors should open when reaches a destination AND at a standstill, should be closed otherwise
3. Button Panels
    * Array of Buttons, each needs an onPress function to tell the elevator what floor to go to
    * Could add an emergency stop button that overrides every command and forces elevator to standstill regardless if it has reached its destination or not
    * Button panel on outside should only have up button and down button, both should call the elevator to the current floor but will be added to the queue differently depending on what floor the elevator is on and whether it is currently going up or down for another previously assigned destination
4. Display
    * When passenger inputs a button, the button should light up and stay lit until the elevator stops at that floor
    * When elevator is passing a floor, a display panel should show the number of each floor as the elevator passes it or stops at it.

## Pseudocode


