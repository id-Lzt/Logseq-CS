- 主要为了执行同步操作
- 会为其修饰的变量，代码块（可以自由定义锁的类型），方法给予一个锁，如果不同synchronized修饰的东西如果是使用的相同的锁的话，只有一个可以拥有这个锁，
- 当锁内任务完成线程进入死亡状态后会释放锁随机唤醒一个，
- 对于多线程工作都公用同一个锁时，线程会变成串行的。