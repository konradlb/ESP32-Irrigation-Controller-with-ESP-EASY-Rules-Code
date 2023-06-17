# ESP-EASY-Rules

ESP EASY Rules

```
on System#Boot do
	loopTimerSet,11,60
  Let,1,900 //gras  in sec
  Let,2,2000 //dripline  in sec
  Let,4,1600  //weges  in sec
  Let,5,5 //Greenhouse  in sec
endon
on Rules#Timer=11 do
 Pulse,33,1,100 //pulse led on pin 33 shortly on 100ms
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
on startWatering do
	timerSet,1,%v1%
  event,GrassBackON
endon
On Rules#Timer=1 do
  event,GrassBackOFF
  event,startWatering2
endOn
on startWatering2 do
	timerSet,2,%v1%
  event,GrassFrontON
endon
On Rules#Timer=2 do
  event,GrassFrontOFF
  event,startWatering3
endOn
on startWatering3 do
	timerSet,3,%v2%
  event,DripLineON
endon
On Rules#Timer=3 do
  event,DripLineOFF
  event,startWatering4
endOn
on startWatering4 do
	timerSet,4,%v4%
  timerSet,5,%v5%
  event,VegetablesON
  event,GreenhouseLeftON
  event,GreenhouseRightON
endon
On Rules#Timer=4 do
  event,VegetablesOFF
endOn
On Rules#Timer=5 do
  event,GreenhouseRightOFF
  event,GreenhouseLeftOFF
endOn
on stopWatering do
	timerSet,1,0
	timerSet,2,0
	timerSet,3,0
	timerSet,4,0
	timerSet,5,0
  event,GrassBackOFF
  event,GrassFrontOFF
  event,DripLineOFF
  event,VegetablesOFF
  event,GreenhouseRightOFF
  event,GreenhouseLeftOFF
endon
on ToggleGPIO do
  GPIO,%eventvalue1%,%eventvalue2%
endon
on SetGPIOforTime do
  GPIO,%eventvalue1%,1
  timerSet,11,%eventvalue2%
  Let,11,%eventvalue1%
endon
on Rules#Timer=11 do
  GPIO,%v11%,0
endon
```
