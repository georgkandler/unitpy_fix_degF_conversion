# UnitPy (Unit Python)

---
---

![Python](https://img.shields.io/pypi/pyversions/unitpy)
![PyPI](https://img.shields.io/pypi/v/unitpy)
![downloads](https://static.pepy.tech/badge/unitpy)
![license](https://img.shields.io/github/license/dylanwal/unitpy)

UnitPy is a Python package for defining, converting, and working with units. 

The goal of the package is to be simple, straightforward, and performant. 

This package directly implements [NIST (National Institute of Standards and Technology)](https://www.nist.gov/pml/special-publication-811/nist-guide-si-chapter-1-introduction) 
official unit definitions. 

---

## Installation

Pip installable package:

`pip install unitpy`

[pypi: unitpy](https://pypi.org/project/unitpy/)


---

## Requirements / Dependencies

Python 3.7 and up

---

## Basic Usage

### Defining Unit

```python
from unitpy import U, Q, Unit, Quantity
# U = Unit

u = Unit("kilometer")
u = U("kilometer")
u = U("km")
u = U.kilometer
u = U.km

u = U("kilometer/hour")
u = U("km/h")
u = U.kilometer / U.hour
u = U.km / U.h

# properties
print(u.dimensionality)  # [length] / [time]
print(u.dimensionless)   # False
print(u.base_unit)       # meter / second
```


### Defining Quantity

** Quantity = Value + Unit **

```python
from unitpy import U, Q , Unit, Quantity
# Q = Quantity

q = 1 * U("kilometer/hour") 
q = 1 * (U.kilometer / U.hour)
q = Quantity("1 km/h")
q = Q("1 kilometer per hour")
q = Q("1*kilometer/hour")


# properties
print(q.unit)            # kilometer / hour
print(q.dimensionality)  # [length] / [time]
print(q.dimensionless)   # False
print(q.base_unit)       # meter / second
```


### Unit Conversion

```python
from unitpy import U, Q , Unit, Quantity
# Q = Quantity

q = 1 * U("km/h") 
q2 = q.to("mile per hour")
print(q2)  # 0.6213711922 mile / hour
```


### Mathematical operation

```python
from unitpy import U, Q 

q = 1 * U("km/h") 
q2 = 2.2 * U("mile per hour")
print(q2 + q)                 # 2.8213711923 mile / hour
print(q2 - q)                 # 1.5786288077 mile / hour
print(q2 * q)                 # 2.2 kilometer mile / hour**2
print(q2 / q)                 # 2.2 mile / kilometer
print((q2 / q).dimensionless) # True
```

### Temperature

__Abbreviations:__

* fahrenheits: degF
* celsius: degC
* kelvin: degK, K
* rankine: degR

```python
from unitpy import U, Q

q = 300 * U("K")
q2 = 200 * U("K")

print(q + q2)        # 500.0 kelvin
print(q.to("degC"))  # 26.85 Celsius
print(q.to("degF"))  # 830.6344444444 Fahrenheit
print(q.to("degR"))  # 166.6666666667 Rankine
```

Temperature units are non-multiplicative units. They are expressed with respect to a reference point (offset).
> degC = 5/9 * (degF - 32) 

Default behavior is **absolute units**.

For **relative units** use dedicated functions `add_rel()` or `sub_rel()`.

```python
from unitpy import U, Q

q = 10 * U("degC")
q2 = 5 * U("degC")

# absolute
print(q.to("K"))         # 283.15 kelvin
print(q + q2)            # 288.15 Celsius 
print((q + q2).to("K"))  # 561.3 kelvin
print(q - q2)            # -268.15 Celsius
print((q - q2).to("K"))  # 5.0 kelvin

# relative
print(q.add_rel(q2))      # 15 Celsius
print(q.sub_rel(q2))      # 5 Celsius
print(abs(-10 * U.degC))  # 10 Celsius
```



## Notes

---

* this package utilizes the American spellings "meter," "liter," and "ton"
