## Analys av beroenden och ansvarsområden
### Vilka beroenden är nödvändiga?
- VehicleController → Vehicle, Saab95, Scania
- Saab95, Scania, Volvo240 → Vehicle
- Vehicle → Movable
- (Vehicle → Direction)
- VehicleController → TimeListener
- DrawPanel → VehicleImage → Vehicle

### Vilka klasser är beroende av varandra som inte bör vara det?
- VehicleController → VehicleView
- VehicleController.addVehicle() → DrawPanel
- Timelistener → DrawPanel
- VehicleView → VehicleController

### Finns det starkare beroenden än nödvändiga?
Nej.

### Kan ni identifiera några brott mot övriga designprinciper vi pratat om i kursen?
#### Encapsulation
De flesta getters/setters borde vara privata då de endast används inom unit tester.
#### Open Closed Principle
Nej.
#### High Cohesion, Low Coupling
High Cohension: Ja.
Low Coupling: Nej. 
#### Dependency Inversion Principle
Använd Collection istället för ArrayList.
getPosition() borde vara getPositionX() och getPositionY().
#### Interface Segregation Principle
Nej.
#### Single Responsibility Principle
VehicleController borde endast kontrollera modellen. En Application class borde innehålla main() metoden. VehicleView bör reagera på modellen oberoende av VehicleController.
#### Separation of Concern
Model, View, Controller finns redan.
#### Mutual Dependencies
- VehicleView → VehicleController bör tas bort

### Vilka ansvarsområden har era klasser?
#### Model
- Vehicle
	-  Direction
- Movable
- Volvo240
- Saab95
- Scania
#### View
- VehicleView
- DrawPanel
- VehicleImage
#### Controller
- VehicleController
	- TimeListener

## Förbättringar
I och med att vi har separerat main funktionen från att ligga i VehicleController till sin egen funktion har vi bättre SOC, det följer även SRP. Eftersom vi även implementerat observers löser vi både Mutual Dependencies och implementerar ett bättre MVC pattern.

### Refaktoriseringsplan
Det första som kommer tillämpas är Main klassen som kommer att konstruera MVC strukturen och initiera, samt kontrollera knapparna. Därefter ska Observer-designen tillämpas. Detta kommer ske parallellt med refaktoriseringen av VehicleView klassen. Detta görs genom att implementera Observable och Observer i deras korresponderande klass, det vill säga Vehicle- och VehicleView klassen. I VehicleView kommer 8 funktioner implementeras som tar hand om knappkonstruktionen. Main klassen kommer att använda sig av dessa funktioner.