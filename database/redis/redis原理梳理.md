

# 内存回收
由于C语言并不具备自动内存回收功能，所以redis在自己的对象系统中构建了一个引用计数（reference counting）计数实现的内存回收机制。通过这一机制，程序可以跟踪对象的引用计数信息，在适当的时候自动释放对象并进行内存回收。

![redis引用计数器](picture/database/redis/redis引用计数器.png "引用计数器状态变化")
