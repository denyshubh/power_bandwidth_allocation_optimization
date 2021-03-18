# Link Budget Model

A link budget is the term used that accounts for the power received at the receiver. This accounts for all of the gain and losses from the transmitter to the point at which it is received by the receiver. It includes losses from cables/fibers and other components in the Tx/Rx chain, gains from the antenna, amplifiers etc. and propagation loss when travelling through air or another medium.

Received power (dBm) = Transmitted power (dBm) + gains (dB) - losses (dB)


```python
# import modules

import numpy as np
import math
from scipy import constants
```


```python
# Calculate link budget for a single beam 

# Signal to Noise Ratio Calculation
def SNR(eirp, obo, gtx, grx, l, Tsys):
    k = constants.k
    snr = eirp - obo + gtx + grx - l - (10*math.log(k*Tsys, 10))
    return snr

# Test SNR() function
print(SNR(63, 5, 52.2, 41.5, 212, 211))
```

    145.0563426202407
    


```python
# Calculate Signal to Noise plus Interfernce ratio
def SNIR(SNR, CABI, CASI, CXPI, C3IM):
    snir = (1/CABI + 1/CASI + 1/CXPI + 1/C3IM + 1/SNR)**-1
    return snir
    
# Test SNIR() function
print(SNIR(145.056, 10000000000,28,30,27))
```

    8.851238047849396
    


```python
# calculate Carrier to adjacent beam interference
def CABI(closest, Pbeam):
    cabi = (10*math.log(Pbeam, 10)) - (10*math.log(sum(closest), 10))
```
