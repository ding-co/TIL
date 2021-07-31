# Doodle

## 1. Interview question (Math + CS)

> ### Q. Function; generates a number from 0 to 1 randomly; uniformly distributed <br/>
>
> ### Calculate the number PI

<br/>

```python
# Idea: Calculate (number of points in circle) / (number of points in square)
# =~ (area of circle) / (area of square) = (PI * r^2) / (2 * r)^2

# PI = 4 * (number of points in the circle) / (the number of points total) [when r = 1]

# r = sqrt(x^2 + y^2)

import random

# input number of points: n
def estimate_pi(n):
  num_point_circle = 0
  num_point_total = 0   # number of points in the square

  for _ in range(n):
    x = random.uniform(0, 1)
    y = random.uniform(0, 1)
    distance = Math.sqrt(x ** 2 + y ** 2)
    if distance <= 1:
      num_point_circle += 1
    num_point_total += 1

  return 4 * (num_point_circle) / (num_point_total)
```

#

## [Reference]

[Reference1](https://www.youtube.com/watch?v=pvimAM_SLic)
