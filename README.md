# Gilbert Kristian - 2306274951 - Adpro A

## Reflection Notes
## 1.2 Understanding How It Works

Screenshot : 
![Screenshot](ss/1.png)
In asynchronous programming, instructions are not executed sequentially. In this case, the `main()` function first creates an executor and a spawner, then calls spawn on the spawner to initiate an asynchronous task. Once the spawn is called, the instruction to execute the task hasn't been given yet, so the task isn't executed immediately. Afterward, `main()` prints "Spawner has been called, task will run asynchronously.", indicating that the task has been queued but not yet processed. Then, `main()` prints "hey hey" first. Only at the end, when the executor is run, does it pick up the spawned task, which then prints "howdy!" after waiting for two seconds, followed by "done!". This order of execution occurs because the asynchronous task is handled by the executor, while the instructions in `main()` are executed first.

## 1.3 Multiple Spawn and Removing Drop

![Screenshot 1](ss/2.png)
![Screenshot 2](ss/3.png)

In this example, the spawner is called three times, creating three separate tasks that run in parallel on different threads. The print sequence, particularly with the "hey hey" message, follows the order in which the spawner is called, so the print order will always start with `howdy1`, `howdy2`, `howdy3`, followed by `done1`, `done2`, `done3`. These tasks are executed concurrently without waiting for each other to complete. The `drop(spawner)` function is used to signal the executor that no more tasks will be spawned, allowing the executor to stop expecting additional tasks. Without `drop(spawner)`, the program continues running because the executor still expects more tasks, but with `drop(spawner)`, the program finishes execution once all tasks are completed as the executor knows no more tasks will be submitted.

