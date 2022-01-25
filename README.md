# Task planner
I created task planners that takes tasks as input and returns a list of tasks in order to be completed based on their priority value. 
I store information using Class Task, which allows creating attributes about the sub-tasks. 
The attributes include task ID, task descriptions, duration in minutes, dependencies, and strict starting time. 
Dependencies refer to the tasks that need to be done before executing a task. Strict starting time exists when a task has to start at the time. 
For instance, my family always starts eating dinner at 5:30 PM, so the eating dinner must start at 5:30 PM. 
Each of the tasks will be an instance that has all of these attributes.

I created three Classes: Max heapq, Task, and TaskScheduler. Max heapq implements properties and methods that support a max priority queue data structure. 
The priority queue will be based on the values of priority values of each subtasks, where subtasks with the highest priority value will be at the root of 
the priority queue. It will have all the characteristics of a max heap data structure, where parent node will always be bigger than its child nodes. 
Class Task will store all the information or attributes of the tasks and subtasks. TaskScheduler holds methods that can create a scheduler given inputs. 
Most of the methods are from CS 110 Session 10: heaps and priority queue, but I heavily revised method run_task_scheduler so that it takes account of dependencies 
and adjust priority values when necessary. To be specific, it sets the priority value of a task to 99 if the difference between its strict starting time and current
time is less than the duration of the current root of the priority queue. The task with strict time constraint will now have the highest priority value, 
and the method executes build_max_heap that will heapify the whole heap, placing the updated task to the root.

Priority queue is a well-suited data structure to prioritize tasks because root of the priority queue will always hold a task with the maximum priority value. 
That is exactly what a scheduler requires: it needs to decide which task should be executed first. Priority queue is also very useful because heappush and heapify 
makes efficient insertion and organization of the heap. Thus, with simple modification, adding a new task or updating the priority value in the middle is possible 
without destroying the sorting.

I created a function priority_generator that provides the initial priority values based on the number of dependencies it has, number of other tasks dependent on 
the task, and duration of the task as shown below. To prevent tasks with strict starting time running before its start time, the generator sets their initial 
priority values to be 0. The priority values of these tasks will be set to 99 when no tasks can be done between current time and the strict starting time of a task.
