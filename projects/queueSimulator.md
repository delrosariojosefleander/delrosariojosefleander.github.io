---
layout: project
type: project
image: img/queue.jpg
title: "Queue Simulator"
date: 2022
published: true
labels:
  - Java
summary: "A simulation of a queue that I developed for ICS 211."
---
This program implements a simulation of a queuing system where customers arrive with randomly generated arrival and service times. The Customer class defines the attributes for a customer, and a Server class represents a server with a finish time and methods to check its availability. The QueueSimulator class orchestrates the simulation, allowing for either a single queue or ten queues, and calculates the total wait time for customers based on the chosen queue configuration. The simulation runs for a day (86400 seconds), and customers are added to the shortest queue based on arrival times. The main method initiates the simulation for a specified number of customers using both single and multiple queue configurations, providing the total wait times for analysis. The code demonstrates object-oriented design and simulation techniques to model and evaluate queuing scenarios.

Here is an example of the output: 
<img class="img-threshold" width = "300px" src="../img/resultOfQueue.PNG">
