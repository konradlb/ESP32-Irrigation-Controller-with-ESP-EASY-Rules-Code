# ESP32 Irrigation Controller with ESP EASY - Rules Code

This project showcases the ESP EASY rules code for an ESP32-based irrigation controller.

## Requirements

I used the following components to build the controller:

- ESP32 microcontroller
- ESP EASY software
- Custom-built 24V water valve power driver

## Rules set 1

```
on System#Boot do
 Let,1,900 //gras back  in sec
 Let,2,1100 //gras front  in sec
 Let,3,1800 //dripline  in sec
 Let,4,1500  //weges  in sec
 Let,5,2400 //Greenhouse  in sec

Let,11,[Var#1]/2 //short
Let,12,[Var#2]/2 //
Let,13,[Var#3]/2 //
Let,14,[Var#4]/2 //
Let,15,[Var#5]/2 //

endon
on GrassBackON do
  gpio,13,1
endon
on GrassBackOFF do
  gpio,13,0
endon
on GrassFrontON do
  gpio,12,1
endon
on GrassFrontOFF do
  gpio,12,0
endon
on DripLineON do
  gpio,14,1
endon
on DripLineOFF do
  gpio,14,0
endon
on GreenhouseLeftON do
  gpio,27,1
endon
on GreenhouseLeftOFF do
  gpio,27,0
endon
on GreenhouseRightON do
  gpio,26,1
endon
on GreenhouseRightOFF do
  gpio,26,0
endon
on VegetablesON do
  gpio,25,1
endon
on VegetablesOFF do
  gpio,25,0
endon
on start do
  event,startWatering
endon
on startWatering do
	timerSet,1,%v1%
  event,GrassBackON
endon
On Rules#Timer=1 do
  event,GrassBackOFF
  event,startWateringFront
endOn
on startWateringFront do
	timerSet,2,%v2%
  event,GrassFrontON
endon
On Rules#Timer=2 do
  event,GrassFrontOFF
  event,startDrip
endOn
on startDrip do
	timerSet,3,%v3%
  event,DripLineON
  timerSet,4,%v4%
  event,VegetablesON
  timerSet,5,%v5%
  event,GreenhouseLeftON
  event,GreenhouseRightON
endon
On Rules#Timer=3 do
  event,DripLineOFF
endOn
On Rules#Timer=4 do
  event,VegetablesOFF
endOn
On Rules#Timer=5 do
  event,GreenhouseRightOFF
  event,GreenhouseLeftOFF
endOn

```

## Rules set 2

```
//short
on startShort do
	timerSet,21,%v11%
  event,GrassBackON
endon
On Rules#Timer=21 do
  event,GrassBackOFF
  event,startShort2
endOn
on startShort2 do
	timerSet,22,%v12%
  event,GrassFrontON
endon
On Rules#Timer=22 do
  event,GrassFrontOFF
  event,startDripShort
endOn
on startDripShort do
	timerSet,23,%v13%
  event,DripLineON
  timerSet,24,%v14%
  event,VegetablesON
  timerSet,25,%v15%
  event,GreenhouseLeftON
  event,GreenhouseRightON
endon
On Rules#Timer=23 do
  event,DripLineOFF
endOn
On Rules#Timer=24 do
  event,VegetablesOFF
endOn
On Rules#Timer=25 do
  event,GreenhouseRightOFF
  event,GreenhouseLeftOFF
endOn
//only GreenHouse
on startGreen do
  timerSet,26,%v5%
  event,GreenhouseLeftON
  event,GreenhouseRightON
endon
On Rules#Timer=26 do
  event,GreenhouseRightOFF
  event,GreenhouseLeftOFF
endOn
on stop do
	timerSet,1,0
	timerSet,2,0
	timerSet,3,0
	timerSet,4,0
	timerSet,5,0
  timerSet,21,0
	timerSet,22,0
	timerSet,23,0
	timerSet,24,0
	timerSet,25,0
  timerSet,26,0
  event,GrassBackOFF
  event,GrassFrontOFF
  event,DripLineOFF
  event,VegetablesOFF
  event,GreenhouseRightOFF
  event,GreenhouseLeftOFF
endon
```
