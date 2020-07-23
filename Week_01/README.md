学习笔记

### 1. HashMap 的小总结

- 扩容是一个特别耗性能的操作，所以当程序员在使用HashMap的时候，估算map的大小，初始化的时候给一个大致的数值，避免map进行频繁的扩容。
- 负载因子是可以修改的，也可以大于1，但是建议不要轻易修改，除非情况非常特殊。
- HashMap是线程不安全的，不要在并发的环境中同时操作HashMap，建议使用ConcurrentHashMap。
- JDK1.8引入红黑树大程度优化了HashMap的性能。


### 2. 用 add first 或 add last 这套新的 API 改写 Deque 的代码：

```
public void test() {
    Deque<String> deque = new LinkedList<>();
    deque.addFirst("a");
    deque.addLast("b");
    deque.offerFirst("c");
    System.out.println(deque);

    String str = deque.peekLast();
    System.out.println(str);
    System.out.println(deque);

    while (deque.size() > 0) {
        System.out.println(deque.pollLast());
    }
    System.out.println(deque.pollFirst());
    System.out.println(deque);
}
```

### 3. 分析 Queue 和 Priority Queue 的源码：

(1) Queue是一个接口，定义了队列的基本操作：
```
public interface Queue<E> extends Collection<E> {

    boolean add(E e);

    boolean offer(E e);

    E remove();

    E poll();

    E element();

    E peek();
}
```

(2) Priority Queue是Queue的实现类，一个优先级队列。
- PriorityQueue是一种无界的，线程不安全的队列。
- PriorityQueue是基于数组实现的平衡二叉堆，节点queue[n]的两个孩子节点从左到右分别是queue[2n+1]和queue[2(n+1)]。
- PriorityQueue存储的元素要求必须是可比较的对象， 如果不是就必须明确指定比较器。
- 初始化容量为11, 每一个父节点都比子节点小，根结点queue[0]为最小值。