tags:: [[Effect TS]]

-
- ## Latch
	- [https://medium.com/@trivediajit99/latches-in-concurrent-programming-e0b76b25e27d](https://medium.com/@trivediajit99/latches-in-concurrent-programming-e0b76b25e27d)
	- [https://effect.website/docs/concurrency/latch/](https://effect.website/docs/concurrency/latch/)
	- Latches are synchronization primitives in computer science, used in concurrent programming to make a thread wait for another to complete an operation. They have two states: "set" and "reset," and are available in different types like Counting Latch, Binary Latch, Spin Latch, Queuing Latch, and Read-Write Latch.
	- In Java, latches are implemented using the `java.util.concurrent.CountDownLatch` class. The example provided demonstrates how a CountDownLatch can be used to synchronize two threads. A worker thread performs a task and decreases the latch count upon completion, allowing the main thread to resume execution only after the latch count reaches zero.
	- This mechanism ensures proper execution order and can synchronize more than two threads when initialized with a count greater than 1.
-
-
- ## Fiber
	-