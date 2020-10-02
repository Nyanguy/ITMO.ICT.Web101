<div align="center"><h1>So, you want to build a high-performance web app?</h1></div>

__tl;dr__ here is the contents
|   Cache  |  Queue |
|:--------:|:------:|
|  Redis   | Celery |
|Memcached |aiohttp?|
| Rabbitmq ||
|Django Cache||

----

## I. Why all the hustle?

In this work we will cover the basic Django optimization methods and practices used to build a high-performance web application.
Some might say that __Python__ as an _interpreted stack-based VM_ is quite slow in compare to a "close to metal" compiled language. While it sertainly true, this statement is decieving of a general nature of a backend workflow. 

> __Any__ given __Task__ can be classified in __two ways__: __CPU-bound__ or __IO-bound__.

Say we have a task(__T__) where we want to _compute_ whether any given _n_ is a member of the Fibonacci sequence:
```python
from typing import Callable
import numpy as np


def is_fib(n: int) -> bool:
"""
>>> is_fib(3)
True
>>> is_fib(55)
True
>>> is_fib(17)
False
"""
  is_perfect_square: Callable[[int, int], bool] = lambda num, root: num == np.power(int(root + 0.5),2)
  value = 5 * np.power(n,2)
  if (root:=np.sqrt(value + 4)) and is_perfect_square(value + 4, root):
    return True
  elif (root:=np.sqrt(value - 4)) and is_perfect_square(value - 4, root):
    return True
  return False
```
In this example we utilize only the CPU and almost don't take any of the RAM or even storage space. Therefore, we can can assume that __T:CPU-bound__ because its performance is highly correlated with the speed of the processor.

Otherwise if a task(__T__) wants to read requests from any given _n_ sources, it would look something like this:
```python
import json
import requests

def send_requests(url: str) -> str: pass

```
Not only the script accessed the local storage to fetch urls, it also has sent them over the network and __waited__ for a response. This is called a __T:IO-bound__. And it is pretty slow. However in comparison Python is a race horse! This is a example of why python dominates in the backend. Most of the backend workflow is __IO-bound__: Database queries, JSON parsing, sending/recieving requests, etc. Even with a _very fast compiled code_, the __performance will be limited by the speed of the peripherals__. Thus, there is no need for the hustle.


### II. But it is still slow

Say there are 5 to 10 urls, it is fine. But if the amount is increased to by orders of a couple magnitudes -- it'll be _very slow_. A common solution for such problem is to split the requests in parallel. 

### Key areas of improvement
* Caching;
* Lazy evalutaion;
* Database optimization;
* HTTP optimizations;
* Static files;
* Cached template loader;
* ;



