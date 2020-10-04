+++
author = "Rogger G. Diaz"
title = "Cars line-up at a car wash | Queue Data Structure"
date = "2020-06-14"
description = "Quickly demonstration of FIFO data structure."
tags = [
    "python",
    "data structure",
    "Algorithms"
]
categories = [
    "Algorithms",
    "Python",
]
series = ["Themes Guide"]
aliases = ["migrate-from-jekyl"]

+++

<!--more-->

## Acknowledge

In Computer Science, world exits algorithms that might be useful when you are looking optimization on your data structure program’s algorithms. The Queue Data Structure(we use QDS to abbreviate). In Computer Science, QDS consist of a collection of items such as when you add a new item happens at one end (since you add a new item this is going back…). The last item is called “rear” of the queue and the items that are removed are called “front”.



When you add of queue’s rear is know as en-queue, and when you remove is know as de-queue. Also exists other operations like peek that return the next value of the element to be de-queue without de-queue it. The queue abstract data type is commonly called FIFO (first-in-first-out). In a FIFO data structure, the most recent items added to a queue must wait at the end collection. The Item that has been for more time in the collection is at the front.







![](https://miro.medium.com/max/703/1*3sb07ob_yOFIWaK4JowCUQ.png)

When you find an algorithm’s efficiency in your environment of execution time, without matter the hardware of the machine’s execution. It is very important to calculate the steps that our algorithm does in the execution process. Each of these steps in the unit of computing. This approach is very useful to qualify our algorithm’s performance. However, depending on what algorithms implement, your algorithm complexity must be difficult or not. The above table shows us the Big-O notation to some specific algorithms of QDS. For more information about this, read the Queue (Abstract Data Type).



## Python Queue Implementation

So now, we need to build an algorithm to understand this better…. Let’s get started!!



##  The problem: Cars line-up at a car wash

Imagine a car wash that has long line-up wait to wash their cars. We need to build a simulation of this. We will construct a modal of a car go into the washer machine. As cars do not into, we need to add them to a waiting list. When the washing machine completes a card, it will look at the queue to see if exists any remaining car to wash. One thing that we must know us is the average that one car lasts to complete their washing.



One wash machine only washes 2 cars per hour. If there 60 cars in the car wash meaning that wash’s machine washed all in 30 hours and 1 car in 0.5 hours (30 minutes). What is the change that at any given second, a car is going to be created? 1 car, 30 minutes.



## Problem solution.

```python
class Queue():
    """docstring for Queue"""

    def __init__(self):
        self.items = []

    def is_empty(self):
        return self.items == []

    def enqueue(self, item):
        self.items.insert(0, item)

    def dequeue(self):
        return self.items.pop()

    def size(self):
        return len(self.items)
```





```python
class carWash:
	def __init__(self, car_per_min):
		self.cpm = car_per_min
		self.current_car = None
		self.time_remaiming = 0

	def tick(self):
		if self.current_car != None:
			self.time_remaiming = self.time_remaiming - 1
			if self.time_remaiming <= 0:
				self.current_car = None

	def busy(self):
		if self.current_car != None:
			return True
		else:
			return False

	def start_next(self, new_car):
		self.current_car = new_car
		self.time_remaiming = new_car.get_cars()  * 60 / self.cpm
```



```python
import random

class Car():
	def __init__(self, time):
		self.timestamp = time
		self.cars = random.randrange(1,3)

	def get_stmap(self):
		return self.timestamp

	def get_cars(self):
		return self.cars

	def wait_time(self, current_time):
		return current_time - self.timestamp
```


```python
from Queue import *
from carWash import *
from Car import *
import random

def main(num_seconds, cars_per_minute):
	car_wash = carWash(cars_per_minute)
	queue = Queue()
	w_time = []

	for  second in range(num_seconds):
		car = Car(second)
		queue.enqueue(car)

		if new_car():
			cara = Car(second)
			queue.enqueue(cara)

		if (not car_wash.busy()) and (not queue.is_empty()):

			next_car = queue.dequeue()
			w_time.append(next_car.wait_time(second))
			car_wash.start_next(next_car)

		car_wash.tick()

	average_wait = sum(w_time) / len(w_time)

	print("Average wait %s secs %d cars remaining." % (average_wait, queue.size()))

def new_car():
	n = random.randrange(1, 30)
	if n == 30:
		return True
	else:
		return False

for i in range(10):
	main(100, 14)
```
##### And Works!



![](https://miro.medium.com/max/530/1*G0Lt_NyuZFw30MYL0lxJhw.png)
