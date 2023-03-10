- 常见的I/O设备
	- 人机交互设备，存储设备
- ## I/O控制方式
	- ### 程序控制
		- 由 CPU 发送控制命令，直接控制 I/O 设备完成输入输出操作，适用于 I/O 操作较简单的设备。
		- Windows操作系统中，命令行窗口中的各种命令都是使用程序控制方式实现的。
	- ### 中断驱动
		- 由 I/O 设备向 CPU 发送中断请求，通知 CPU 有数据需要输入或输出，适用于 I/O 操作较复杂、数据量较大的设备。
		- 在Windows操作系统中，所有设备的驱动程序都是采用中断驱动方式实现的。
	- ### DMA（直接存储器访问）
		- 由 DMA 控制器控制 I/O 设备直接与内存进行数据传输，减轻了 CPU 的负担，提高了系统性能，适用于数据量较大的 I/O 设备。
		- 在Windows操作系统中，一些需要大量数据传输的设备，如硬盘、网络适配器等。
	- ### 通道控制
		- 由 I/O 控制器（通道）独立完成数据传输，与 CPU 并行处理，可以实现高速、大容量的数据传输，适用于高性能、高容量的 I/O 设备。
		- 在Windows操作系统中，一些大型应用程序，如数据库、图像处理软件等，可能会采用存储映射I/O控制方式实现。
- ## 缓冲区
	- ### 作用
		- 操作系统缓冲区的主要作用是为了加快数据读写操作的速度。当应用程序需要读写数据时，操作系统会将数据缓存到内存中，以便下次访问时可以更快地获取数据，而不必再从磁盘或其他慢速存储介质中读取。通过使用缓冲区，可以减少磁盘和其他外部设备的访问次数，从而提高系统性能和响应速度。
		- 另外，缓冲区还可以提供一种机制来控制不同进程之间的数据传输。例如，操作系统可以使用缓冲区来实现进程间的通信。
	- 用户级缓冲区
	- 内核级缓冲区
	- 双缓冲区
	- 缓冲池
		-