
## 栈

```js
    /**
    * 数据结构: 栈
    * 特性: 后进先出
    * 功能: 添加元素、删除元素、获取栈顶元素、是否为空、获取栈长度、清除元素
    *
    */
    function Stack() {
      this.items = [];
    }
    Stack.prototype = {
      constructor: Stack,
      push: function(element) {
        this.items.push(element);
      },
      pop: function(element) {
        return this.items.pop();
      },
      peek: function() {
        return this.items[this.items.length - 1];
      },
      isEmpty: function() {
        return this.items.length === 0;
      },
      clean: function() {
        this.items = [];
      },
      size: function() {
        return this.items.length;
      },
      print: function() {
        console.log(this.items.toString());
      }
    }

    // 栈的基本使用
    var stack = new Stack();
    console.log(stack.isEmpty());
    stack.push(5);
    stack.push(8);
    console.log(stack.peek());
    stack.push(11);
    console.log(stack.size());
    console.log(stack.isEmpty());
    stack.push(15);
    stack.pop();
    stack.pop();
    console.log(stack.size());
    console.log(stack.print());

    // 通过栈实现对正整数的二进制转换
    function divideBy2(decNumber) {
      var decStack = new Stack();
      var rem;
      var decString = '';
      while(decNumber > 0) {
        rem = decNumber%2;
        decStack.push(rem);
        decNumber = Math.floor(decNumber/2);
      }
      while(!decStack.isEmpty()) {
        decString += decStack.pop().toString();
      }
      return decString;
    }

    console.log(divideBy2(10));
```

## 队列

```js
  /**
  * 数据结构: 队列
  * 特点: 先进先出(FIFO, Firs In First Out)
  * 功能: 队列尾部添加元素、队列顶部移除元素、获取顶部元素、是否为空、获取长度、清空、打印
  */

  function Queue() {
    this.items = [];
  }
  Queue.prototype = {
    constructor: Queue,
    enqueue: function(element) {
      this.items.push(element);
    },
    dequeue: function() {
      return this.items.shift();
    },
    front: function() {
      return this.items[0];
    },
    isEmpty: function() {
      return this.items.length === 0;
    },
    size: function() {
      return this.items.length;
    },
    clear: function() {
      this.items = [];
    },
    print: function() {
      console.log(this.items.toString());
    }
  }

  // 队列的基本使用
  var queue = new Queue();
  console.log(queue.isEmpty());
  queue.enqueue('pig');
  queue.enqueue('dog');
  console.log(queue.print());
  console.log(queue.size());
  console.log(queue.isEmpty());
  queue.enqueue('duck');
  console.log(queue.dequeue());
  console.log(queue.print());

  /**
  * 数据结构: 优先队列
  * 特点: 元素的添加和移除是基于优先级
  * 功能: 按照优先级放置队列的元素
  */
  function PriorityQueue() {
    Queue.call(this);
  }
  PriorityQueue.prototype = new Queue();
  PriorityQueue.prototype.constructor = PriorityQueue;
  PriorityQueue.prototype.enqueue = function(element, priority) {
    function QueueElement(tempelement, tempprioripty) {
      this.element = tempelement;
      this.priority = tempprioripty;
    }
    var queueElement = new QueueElement(element, priority);
    if (this.isEmpty()) {
      this.items.push(queueElement);
    }else {
      var added = false;
      for (var i = 0; i < this.items.length; i++) {
        if (this.items[i].priority > queueElement.priority) {
          this.items.splice(i, 0, queueElement);
          added = true;
          break;
        }
      }
      if (!added) {
        this.items.push(queueElement);
      }
    }
  }
  PriorityQueue.prototype.print = function() {
    var result = '';
    for (var i = 0; i < this.items.length; i++) {
      result += JSON.stringify(this.items[i]);
    }
    return result;
  }

  // 优先队列的基本使用
  var priorityQueue = new PriorityQueue();
  priorityQueue.enqueue('dog', 2);
  priorityQueue.enqueue('pig', 3);
  priorityQueue.enqueue('duck', 1);
  console.log(priorityQueue.print());
  console.log(priorityQueue.size());
  console.log(priorityQueue.dequeue());
  console.log(priorityQueue.size());
```

## 链表

```js
    /**
    * 数据结构: 链表
    * 特点: 链表元素在内存中不是连续存放，访问需要从头开始遍历
    * 功能:
    */
    function LinkedList() {
      function Node(element) {
        this.element = element;
        this.next = null;
      }
      this.head = null;
      this.length = 0;
      if ((typeof this.append !== 'function') && (typeof this.append !== 'string')) {
        // 添加元素
        LinkedList.prototype.append = function(element) {
          var node = new Node(element);
          var current;
          if (this.head === null) {
            this.head = node;
          }else {
            current = this.head;
            while(current.next != null) {
              current = current.next;
            }
            current.next = node;
          }
          this.length++;
        }
      };

      // 插入元素，成功为true, 失败为false
      LinkedList.prototype.insert  = function(position, element) {
        if (position > -1 && position < this.length) {
          var current = this.head;
          var previous;
          var index = 0;
          var node = new Node(element);
          if (position == 0) {
            node.next = current;
            this.head = node;
          }else {
            while(index++ < position) {
              previous = current;
              current = current.next;
            }
            node.next = current;
            previous.next = node;
          }
          this.length++;
          return true;
        }else {
          return false;
        }
      };

      // 根据位置删除指定元素，成功返回元素， 失败返回null
      LinkedList.prototype.removeAt = function(position) {
        if (position > -1 && position < this.length) {
          var current = this.head;
          var previous = null;
          var index = 0;
          if (position == 0) {
            this.head = current.next;
          }else {
            while(index++ < position) {
              previous = current;
              current = current.next;
            }
            previous.next = current.next;
          }
          this.length--;
          return current.element;
        }else {
          return null;
        }
      };

      // 根据元素删除指定元素，成功返回元素，失败返回null
      LinkedList.prototype.remove = function(element) {
        var index = this.indexOf(element);
        return this.removeAt(index);
      };

      // 返回给定元素的索引，如果没有返回-1
      LinkedList.prototype.indexOf = function(element) {
        var current = this.head;
        var index = 0;
        while(current) {
          if (current.element === element) {
            return index;
          }
          index++;
          current = current.next;
        }
        return -1;
      };

      LinkedList.prototype.isEmpty = function() {
        return this.length === 0;
      };

      LinkedList.prototype.size = function() {
        return this.length;
      };

      LinkedList.prototype.toString = function() {
        var string = '';
        var current = this.head;
        while(current) {
          string += current.element;
          current = current.next;
        }
        return string;
      };

      LinkedList.prototype.getHead = function() {
        return this.head;
      };
    }

    // 链表的基本使用
    var linkedList = new LinkedList();
    console.log(linkedList.isEmpty());
    linkedList.append('dog');
    linkedList.append('duck');
    linkedList.insert(1, 'pig');
    console.log(linkedList.toString());
    console.log(linkedList.indexOf('duck'));
    console.log(linkedList.size());
    console.log(linkedList.removeAt(2));
    console.log(linkedList.toString());

    /**
    * 数据结构: 双向链表
    * 特点: 链接是双向的，一个链向下一个元素，另一个链向前一个元素
    * 功能:
    */
    function inheritPrototype(subType, superType) {
      function object(o) {
        function F() {}
        F.prototype = o;
        return new F();
      }
      var prototype = object(superType.prototype);
      prototype.constructor = subType;
      subType.prototype = prototype;
    }
    function DoubleLinkedList() {
      function Node(element) {
        this.element = element;
        this.next = null;
        this.prev = null;
      }
      this.tail = null;
      LinkedList.call(this);
      this.insert = function(position, element) {
        if (position > -1 && position <= this.length) {
          var node = new Node(element);
          var current = this.head;
          var previous;
          var index = 0;
          if (position === 0) {
            if (!this.head) {
              this.head = node;
              this.tail = node;
            } else {
              node.next = current;
              current.prev = node;
              this.head = node;
            }
          } else if (position === this.length) {
            current = this.tail;
            current.next = node;
            node.prev = current;
            this.tail = node;
          } else {
            while(index++ < position) {
              previous = current;
              current = current.next;
            }
            previous.next = node;
            node.next = current;
            current.prev = node;
            node.prev = previous;
          }
          this.length++;
          return true;
        }else {
          return false;
        }
      };

      this.append = function(element) {
        var node = new Node(element);
        var current;
        if (this.head === null) {
          this.head = node;
          this.tail = node;
        } else {
          current = this.head;
          while(current.next !== null) {
            current = current.next;
          }
          current.next = node;
          node.prev = current;
          this.tail = node;
        }
        this.length++;
      };

      this.removeAt = function(position) {
        if (position > -1 && position < this.length) {
          var current = this.head;
          var previous;
          var index = 0;
          if (position === 0) {
            this.head = current.next;
            if (this.length === 1) {
              this.tail = null;
            }else {
              this.head.prev = null;
            }
          }else if (position === (this.length - 1)) {
            current = this.tail;
            this.tail = current.prev;
            this.tail.next = null;
          }else {
            while(index++ < position) {
              previous = current;
              current = current.next;
            }
            previous.next = current.next;
            current.next.prev = previous;
          }
          this.length--;
          return current.element;
        }else {
          return false;
        }
      };
    }
    inheritPrototype(DoubleLinkedList, LinkedList);

    // 双向链表的基本使用
    var doublyList = new DoubleLinkedList();
    console.log(doublyList.isEmpty());
    doublyList.append('blue');
    doublyList.append('green');
    doublyList.insert(1, 'red');
    console.log(doublyList.toString());
    console.log(doublyList.indexOf('red'));
    console.log(doublyList.size());
    console.log(doublyList.removeAt(2));
    console.log(doublyList.toString());
```