24 июля 2026 г.

# Зацени подробные красивые commit messages


```
WIP7: integrating KeplerOrbitAnimation into TheRings

 + fixed BUG the ship does not fly when the direction hold mode is selected (for example, prograde)
 + improved Ship Rotating logic by physics constaraints
 + improved Ship Rotate Stabilishing logic by physics constaraints
 + removed backup code variants for SAS, removed some debug code
 + updated RCS SAS Poser settings
 + Player controller. Added for RCS SAS power continue changing logic
 + fixed ghosting for Master ring surface mat (added Output Depth and Velocity)
```
```
info: added code optimization for ue5, update md syntax
```
```
WIP6: integrating KeplerOrbitAnimation into TheRings

 + fixed BUG wrong UI apo/peri height. wrong translate from cm to m
 + Added target orbit info on Simple HUD. Collapsed separated ShipHUD-variables to One ShipHUD-structure variable. New Logic for displing exponential gravity acceleration.
 + Rover: sync Update HUD function with Flying pawn
 + Update Mu for RoverOnMoon map
 + A bit updeted BigMass gravity, and gravities ans radiuses for space body properties
 + Added Gravity property to SpaceBodyProperty structure
```
```
WIP5: integrating KeplerOrbitAnimation into TheRings

 + New orbits visual implemented
 + Added node radius vector calculations in StateVector mode to the code. This was missed.
 + re-set up flying bodies on the main scene. Slightly reduced the big mass body Mu (reducing speed).
 + setup retrograde/prpgrade colors (node points, apsis points)
```
```
WIP4: integrating KeplerOrbitAnimation into TheRings

 - setup orbit motion on level MainAllRingsScaleX3
 - bTickPhysicsAsync=True, AsyncFixedTimeStepSize=0.010000
 - optimized list of console commands
```
```
WIP3: integrating KeplerOrbitAnimation into TheRings

 - заменить расчет орбиты старый компонент на новый (BP_BaseSpaceBody должен запускаться и летать на нем)
 - deleted useless nodes and functions
 - new gamemode for testing orbits
 - in actor manager, registrate - replaced add to addunique. It's More logically
 - updated synodic period logics in baseSpaceBody classes
 - fixed wrong Period math formula in `KOA`.cpp
```
```
WIP2: integrating KeplerOrbitAnimation into TheRings

- заменить расчет орбиты старый компонент на новый (должен запускаться и летать на нем)
  /Game/TheRings/Core/Space/BP_BaseSpaceBody
```
``` 
WIP: integrating KeplerOrbitAnimation into TheRings

- заменить расчет орбиты старый компонент на новый (должен запускаться и летать на нем)
  /Game/TheRings/Core/Space/BP_BaseSpaceBody
```

**Это work in progress на каждый день.** 

Когда я завершу, склею их в один и получится что-то типа: 

```
feature: integrating KeplerOrbitAnimation into TheRings

 + improved Ship Rotating logic by physics constaraints
 ... большой список всех изменений
 + replaced old orbit component to new
```
хороший способ держать все под контролем. но это не точно. А git все помнит и ни один коммит не будет удален.