# timeout_manager
A timeout manager stores a priority queue of timeout items, each a (callback method, callback time) pair. Ex:

At time t = 0, a 500 millisecond timeout is set for method A
At time t = 100, a 3000 millisecond timeout is set for method B
At time t = 2000, a 1000 millisecond timeout is set for method C
So the timeout manager should call the callbacks as follows:

Call method A at time t = 0 + 500 = 500
Call method C at time t = 2000 + 1000 = 3000
Call method B at time t = 100 + 3000 = 3100
A timeout item with a callback time <= the current time is said to be "expired".

Millisecond-level callback precision is often unfeasible. So a timeout manager typically has an update method that is called by external code every so often, ex: every 100 milliseconds. The manager's update method calls each expired timeout's callback method.


