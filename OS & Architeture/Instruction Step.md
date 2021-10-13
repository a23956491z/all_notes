---
tags : computer-architeture
---

# Instrcution Steps
1. Instruction Fetch
2. Instruction Decode & Register Fetch
3. Computation
	* R-type instruction Execution
	* Memory Read/Write Address
	* Branch/Jump Completion
4. Access
	* Memory Read Access
	* Memory Wite Completion
	* R-type instruction Completion
* Memory Read Completion

## Register Transfer Language
aka RTL



## Step1 : Fetch

### RTL
![](https://i.imgur.com/hUr5UO2.png)

## Step2 : Decode  & Register Fetch 

we don't know don't know exactly instruction rn
* do some preparation

### Preparation
* **Read Register** whether we need or not 
* **Compute Brach Addr** whether we need or not

### RTL
![](https://i.imgur.com/uc2HizC.png)

### Datapath 
(blue line)
![](https://i.imgur.com/Rze9z3p.png)


## Step 3
only R-type doesn't complete its instruction

### Memory reference
RTL:
![](https://i.imgur.com/A6rO7VH.png)

Datapath:
![](https://i.imgur.com/gaOvn7q.png)

### R-type
RTL:
![](https://i.imgur.com/F3Qrjiy.png)

Datapath:
![](https://i.imgur.com/9ANNrbI.png)

### Branch
RTL:
![](https://i.imgur.com/98R1mcJ.png)

Datapath:
![](https://i.imgur.com/aJkjRF1.png)


### Jump
RTL:
![](https://i.imgur.com/aZMiHXx.png)

Datapath
![](https://i.imgur.com/OTSCyrq.png)

## Step 4

### Memory reference
RTL:
![](https://i.imgur.com/hafC9Ru.png)

datapath of `lr`
![](https://i.imgur.com/AEgcnCd.png)

datapath of `sw`
![](https://i.imgur.com/ZaROUGw.png)

### R-type
RTL:
![](https://i.imgur.com/hhy3l9V.png)

