http://sdeuoc.ac.in/sites/default/files/sde_videos/Digital%20Image%20Processing%203rd%20ed.%20-%20R.%20Gonzalez%2C%20R.%20Woods-ilovepdf-compressed.pdf

**Any periodic function** can be expressed as the su m of sines and/or cosines of different frequency, each multiplied by a different coefficient

**Functions that are not periodic** & area under curve is finete, can be expressed as the intergral of sines and/or cosines multiplied by a weighting function.

a function, expressed in either a Fourier series or transform, can be reconstructed completely via an inverse process with no loss of information.
*This is why we can use Fourier transform to deal with praical problem*

![](https://i.imgur.com/7Gs9Kxf.png)


![](https://i.imgur.com/3abwcjW.png)

![](https://i.imgur.com/RmCcOit.png)


## Impulse & sifting property
![](https://i.imgur.com/1b7CJOT.png)

$f(t)$ is continous at $t=0$
![](https://i.imgur.com/wEPqHT9.png)


![](https://i.imgur.com/aKbWNBN.png)

discrete impulse
![](https://i.imgur.com/oPEHgi2.png)

## Fourier Transfomer of functions of one continuous variable

![](https://i.imgur.com/B2jIXtV.png)
![](https://i.imgur.com/qxBzwYl.png)

![](https://i.imgur.com/XlJ32Me.png)

![](https://i.imgur.com/caHcfTb.png)

with Euler's formula:
![](https://i.imgur.com/3h1HA6h.png)

sinusodial terms's frequencies are determined by $\mu$(variable $t$ is intergrated out)

domain of the Fourier transform is **frequency domain**

Example:
![](https://i.imgur.com/6W4S7HQ.png)

![](https://i.imgur.com/XHQ3jhO.png)

### Convolution

convoluton of 2 continuous functions with one continuous variable
![](https://i.imgur.com/jsapBmA.png)

* minus sign accounts for the flipping
* $t$ is the displacement to sliding
* $\tau$ is dummy variable that is  intergrated out

put into Fourier
![](https://i.imgur.com/QBqZK3W.png)

![](https://i.imgur.com/XHqI4hN.png)

convolution theorem
![](https://i.imgur.com/jr9oXe7.png)

## Fourier transform of sampled function
sample
![](https://i.imgur.com/6ngy3VJ.png)


## Discrete Fourier Transform of one variable
![](https://i.imgur.com/4fwjOmt.png)

![](https://i.imgur.com/LG6dshM.png)
inverse:
![](https://i.imgur.com/o0bV4ow.png)

### convolution
![](https://i.imgur.com/1ZVoqJD.png)

## Frequency Domain Filtering
Inverse Discrete Fourier Transform
![](https://i.imgur.com/ThqG9VF.png)
