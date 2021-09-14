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
    * Doors should stay open for a certain period of time once it reaches the destination then close
3. Button Panels
* Inside Button Panel
    * Array of Buttons; each needs a function to tell the elevator what floor to go to
    * Add an emergency stop button that overrides every command and forces elevator to standstill regardless if it has reached its destination or not
* Outside Button Panel
    * Button panel on outside should only have up button and down button, both should call the elevator to the current floor but will be added to the queue differently depending on what floor the elevator is on and whether it is currently going up or down for another previously assigned destination
    * Should be several Outside Button Panels, one for each floor that tells the Elevator what floor it's being called to
4. Display
    * When passenger inputs a button, the button should light up and stay lit until the elevator stops at that floor
    * When elevator is passing a floor, a display panel should show the number of each floor as the elevator passes it or stops at it.

## Pseudocode

**Scenario**: Pseudocode for an elevator to service 10 floors

### 1: Define Objects and Functions

* Elevator  
    * elevatorUp  --> currentFloor++
    * elevatorDown  --> currentFloor--
    * elevatorStop  --> currentFloor === onPress() OR currentFloor === passengerFloor()
    * currentFloor  --> READ which floor the elevator is currently on

* Doors
    * doorOpen --> currentFloor === onPress OR currentFloor === passengerFloor()
    * doorClose  --> elevatorUp = true OR elevatorDown = true
    * INIT doorAtDestination()  --> elevatorStop and doorOpen and stays open for predetermined time

* Button Panels
    * INIT onPress()  --> button tells elevator what floor number was pressed and adds to array
        * button1 = 1, button2 = 2, etc.
    * INIT floorQueue  --> array for floors selected
    * INIT emerStop()  --> emergency stop, overrides all commands and implements elevatorStop and doorClose  
 
    - INIT passengerCall() --> tells elevator if floor called is up or down
    - INIT passengerFloor() --> tells elevator what floor passenger called it to and adds floor number to array

* Display
    * isButtonSelected  --> true or false
    * buttonOn --> Turns button light on if isButtonSelected(true)
    * INIT floorDisplay()  --> DISPLAY currentFloor as elevator passes it or stops at it


### 2: Brief Overview Example
```
START

Elevator.currentFloor(10)
ButtonPanels.passengerFloor(Floor1)
ButtonPanels.passengerCall(down)
Elevator.elevatorDown
Doors.doorAtDestination(doorOpen)

Display.floorDisplay(currentFloor)
ButtonPanels.onPress(Floor6)
Display.isButtonSelected(buttonOn)
Elevator.elevatorUp
Doors.doorAtDestination(doorOpen)

END
```

### 3. Pseudocode Objects and Functions
```
START

// Function for elevator to travel from current floor to floor it's been called to

IF currentFloor != passengerFloor
    THEN 
        WHILE currentFloor > passengerFloor
            elevatorDown
            break
        WHILE currentfloor < passengerFloor
            elevatorUp
            break
        END WHILE
ELSE doorAtDestination()



// Function for elevator to travel to floor selected on inside button panel

IF onPress() != currentFloor()
    THEN 
        WHILE currentFloor() > onPress()
            elevatorDown
            break        
        WHILE currentfloor() < onPress()
            elevatorUp
            break        
        END WHILE        
ELSE doorAtDestination()                



// Function for elevator to make stops along the way if it receives new 
calls while it's heading in the same directiion and the new calls are 
between its current floor and its destination

IF passengerCall(up)
    THEN 
        IF elevatorUp === true AND (currentFloor <= passengerFloor <= onPress)
            THEN
                WHILE currentfloor() < passengerFloor()
                    elevatorUp
                    break
                END WHILE
        ELSE doorAtDestination()
ELSE IF passengerCall(down)
    THEN 
        IF elevatorDown === true AND (currentFloor >= passengerFloor >= onPress)
            THEN
                WHILE currentfloor() > passengerFloor()
                    elevatorDown
                    break
                END WHILE
        ELSE doorAtDestination()



// Turn button light on function

IF isButtonSelected() == true  
    buttonOn
END IF 



// Function for emergency stop, needs to override all other functions

IF isButtonSelected() == true
    alert
    doorClose AND elevatorStop
END IF



END
```
