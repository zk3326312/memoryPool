# memoryPool
一个仿STL的alloc第二层配置器的memoryPool<br>
  　　STL的内存分配器alloc，是分为两层实现的,第一层是对malloc进行了一个简单的封装，当需要分配超过128byte的内存时，直接调用第一层来进行分配，对于分配一些小块的内存时，调用第二层配置器，第二层配置器的做法是以内存池的管理方式实现的：每次配置一大块内存，并维护对应的自由链表（），下次若再有相同大小的内存需求，就直接从freelist中分配，当释放小块的内存块时，就将该内存回收到freelist中，这样避免了很多小额区块造成的内存碎片。<br>
  　　对于维护链表需要的额外指针开销，alloc通过一个巧妙的union解决了这个问题（union体中数据共享同一段内存，以达到节省空间的目的)<br>
    　本段代码大致实现了SGI STL中第二层配置器的功能，并测试了这个分配器的分配效率，测试效果如下：<br>
     ![Image text](https://github.com/zk3326312/Image_folder/blob/master/memoryPool_result/memoryPoolResult.bmp)
        
        
