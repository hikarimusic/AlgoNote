Data Structure
==============

Array
-----
:insert: O(N)
:delete: O(N)
:get: O(1)

.. tabs::

    .. code-tab:: python

        class Array:
            def __init__(self, size):
                self.size = size
                self.arr = [None] * size
                self.len = 0

            def insert(self, data, pos):
                for i in range(self.len, pos, -1):
                    self.arr[i] = self.arr[i-1]
                self.arr[pos] = data
                self.len += 1

            def delete(self, pos):
                for i in range(pos, self.len-1, 1):
                    self.arr[i] = self.arr[i+1]
                self.len -= 1

            def get(self, pos):
                return self.arr[pos]

        if __name__ == '__main__':
            array = Array(5)
            array.insert(3, 0)
            array.insert(1, 0)
            array.insert(0, 0)
            array.insert(4, 2)
            array.insert(2, 1)
            array.delete(0)
            array.delete(2)

            result = []
            for i in range(array.len):
                result.append(array.get(i))
            print(result)

    .. code-tab:: c++

        working

    .. code-tab:: java

        working

Linked List
-----------
:insert_next: O(1)
:insert_prev: O(1)
:delete: O(1)
:get: O(N)

.. tabs::

    .. code-tab:: python

        class Node:
            def __init__(self, data):
                self.data = data
                self.next = None
                self.prev = None

        class LinkedList:
            def __init__(self):
                self.head = None
                self.size = 0

            def insert_next(self, new_data, pre_node):
                new_node = Node(new_data)
                if not pre_node:
                    new_node.next = self.head
                    self.head = new_node
                    if new_node.next: new_node.next.prev = new_node
                else:
                    new_node.next = pre_node.next
                    pre_node.next = new_node
                    new_node.prev = pre_node
                    if new_node.next: new_node.next.prev = new_node
                self.size += 1
            
            def insert_prev(self, new_data, nex_node):
                new_node = Node(new_data)
                if not nex_node:
                    new_node.prev = self.get(-1)
                    if new_node.prev: new_node.prev.next = new_node
                else:
                    new_node.prev = nex_node.prev
                    nex_node.prev = new_node
                    new_node.next = nex_node
                    if new_node.prev: new_node.prev.next = new_node
                self.size += 1

            def delete(self, node):
                if not node.prev:
                    self.head = node.next
                    node.next.prev = None
                elif not node.next: 
                    node.prev.next = None
                else:
                    node.prev.next = node.next
                    node.next.prev = node.prev
                self.size -= 1
            
            def get(self, pos):
                if pos < 0: pos = self.size + pos
                temp = self.head
                for i in range(pos): temp = temp.next
                return temp

        if __name__ == '__main__':
            linkedlist = LinkedList()
            linkedlist.insert_next(3, None)
            linkedlist.insert_next(7, None)
            linkedlist.insert_next(8, None)
            linkedlist.insert_next(1, linkedlist.get(0))
            linkedlist.insert_next(6, linkedlist.get(-1))
            linkedlist.insert_prev(2, None)
            linkedlist.insert_prev(5, None)
            linkedlist.insert_prev(9, None)
            linkedlist.insert_prev(0, linkedlist.get(3))
            linkedlist.insert_prev(4, linkedlist.get(-2))
            linkedlist.delete(linkedlist.get(4))
            linkedlist.delete(linkedlist.get(0))
            linkedlist.delete(linkedlist.get(-1))

            result = []
            for i in range(linkedlist.size):
                result.append(linkedlist.get(i).data)
            print(result)
    
    .. code-tab:: c++

        working

    .. code-tab:: java

        working

Stack
-----
:push: O(1)
:pop: O(1)
:get: O(1)

.. tabs::

    .. code-tab:: python

        class Stack:
            def __init__(self, size):
                self.size = size
                self.arr = [None] * size
                self.top = 0

            def push(self, data):
                self.arr[self.top] = data
                self.top += 1
            
            def pop(self):
                self.top -= 1
            
            def get(self):
                return self.arr[self.top - 1]

        if __name__ == '__main__':
            stack = Stack(5)
            stack.push(0)
            stack.push(1)
            stack.push(2)
            stack.push(3)
            stack.push(4)

            result = []
            for i in range(stack.top):
                result.append(stack.get())
                stack.pop()
            print(result)

    .. code-tab:: c++

        working

    .. code-tab:: java

        working

Queue
-----
:enqueue: O(1)
:dequeue: O(1)
:get: O(1)

.. tabs::

    .. code-tab:: python

        class Queue:
            def __init__(self, size):
                self.size = size
                self.arr = [None] * size
                self.head = 0
                self.tail = 0
                self.len = 0

            def enqueue(self, data):
                self.arr[self.tail] = data
                self.tail = (self.tail + 1) % self.size
                self.len += 1

            def dequeue(self):
                self.head = (self.head + 1) % self.size
                self.len -= 1

            def get(self):
                return self.arr[self.head]

        if __name__ == '__main__':
            queue = Queue(5)
            queue.enqueue(0)
            queue.enqueue(1)
            queue.enqueue(2)
            queue.enqueue(3)
            queue.enqueue(4)

            result = []
            for i in range(queue.len):
                result.append(queue.get())
                queue.dequeue()
            print(result)

    .. code-tab:: c++

        working

    .. code-tab:: java

        working

Heap
----
:insert: O(logN)
:delete: O(logN)
:get: O(1)

.. tabs::

    .. code-tab:: python

        class Heap:
            def __init__(self, size):
                self.size = size
                self.arr = [None] * size
                self.len = 0

            def insert(self, data):
                self.arr[self.len] = data
                self.len += 1
                i = self.len - 1
                while i > 0 and self.arr[i] > self.arr[(i-1)//2]:
                    self.arr[i], self.arr[(i-1)//2] = self.arr[(i-1)//2], self.arr[i]
                    i = (i-1)//2

            def delete(self):
                self.arr[0], self.arr[self.len-1] = self.arr[self.len-1], self.arr[0]
                self.len -= 1
                i = 0
                while (i*2+1) < self.len:
                    if (i*2+2) >= self.len: mc = i*2+1
                    else:
                        if self.arr[i*2+1] > self.arr[i*2+2]: mc = i*2+1
                        else: mc = i*2+2
                    if self.arr[i] < self.arr[mc]:
                        self.arr[i], self.arr[mc] = self.arr[mc], self.arr[i]
                    i = mc

            def get(self):
                return self.arr[0]

        if __name__ == '__main__':
            heap = Heap(10)
            heap.insert(3)
            heap.insert(7)
            heap.insert(5)
            heap.insert(2)
            heap.insert(1)
            heap.insert(0)
            heap.insert(8)
            heap.insert(9)
            heap.insert(4)
            heap.insert(6)

            result = []
            for i in range(heap.len):
                result.append(heap.get())
                heap.delete()
            print(result)

    .. code-tab:: c++

        working

    .. code-tab:: java

        working

Hash
----
:insert: O(1) on average
:delete: O(1) on average
:get: O(1) on average

.. tabs::

    .. code-tab:: python

        class Node:
            def __init__(self, key, data):
                self.key = key
                self.data = data
                self.next = None

        class Hash:
            def __init__(self, size):
                self.size = size
                self.adj = [None] * size

            def insert(self, key, data):
                h_key = key % self.size
                temp = Node(key, data)
                temp.next = self.adj[h_key]
                self.adj[h_key] = temp

            def delete(self, key):
                h_key = key % self.size
                temp = self.adj[h_key]
                prev = None
                while temp:
                    if temp.key == key:
                        if prev == None: self.adj[h_key] = temp.next
                        else: prev.next = temp.next
                    else: prev = temp
                    temp = temp.next
            
            def get(self, key):
                h_key = key % self.size
                temp = self.adj[h_key]
                while temp:
                    if temp.key == key:
                        return temp
                    temp = temp.next
                return temp

        if __name__ == '__main__':
            hash = Hash(10)
            hash.insert(1, "United States")
            hash.insert(7, "Russia")
            hash.insert(33, "France")
            hash.insert(44, "United Kingdom")
            hash.insert(49, "Germany")
            hash.insert(81, "Japan")
            hash.insert(82, "South Korea")
            hash.insert(86, "China")
            hash.insert(91, "India")
            hash.insert(886, "Taiwan")
            hash.delete(86)
            hash.delete(7)

            code = [1, 33, 44, 49, 81, 82, 91, 886]
            for c in code:
                print(c, hash.get(c).data)

    .. code-tab:: c++

        working

    .. code-tab:: java

        working

Tree
----
:insert: O(N)
:delete: O(N)
:traverse: O(N)

.. tabs::

    .. code-tab:: python

        class Node:
            def __init__(self, data):
                self.data = data
                self.left = None
                self.right = None

        class Tree:
            def __init__(self):
                self.root = None
            
            def insert(self, data, root):
                new_node = Node(data)
                if not root: self.root = new_node
                else:
                    q = []
                    q.append(root)
                    while (len(q)):
                        temp = q.pop(0)
                        if not temp.left:
                            temp.left = new_node
                            break
                        else:
                            q.append(temp.left)
                        if not temp.right:
                            temp.right = new_node
                            break
                        else:
                            q.append(temp.right)

            def delete(self, root):
                if not root: self.root = None
                else:
                    q = []
                    q.append(root)
                    last = None
                    while (len(q)):
                        last = q.pop(0)
                        if last.left: q.append(last.left)
                        if last.right: q.append(last.right)
                    q = []
                    q.append(root)
                    while (len(q)):
                        temp = q.pop(0)
                        if temp.left == last:
                            temp.left = None
                            return
                        if temp.right == last:
                            temp.right = None
                            return
                        if temp.left: q.append(temp.left)
                        if temp.right: q.append(temp.right)

            def traverse(self, root):
                left, right = [], []
                if root.left: left = self.traverse(root.left)
                if root.right: right = self.traverse(root.right)
                return left + [root] + right

        if __name__ == '__main__':
            tree = Tree()
            tree.insert(7, None)
            tree.insert(2, tree.root)
            tree.insert(1, tree.root)
            tree.insert(5, tree.root)
            tree.insert(9, tree.root)
            tree.insert(8, tree.root)
            tree.insert(3, tree.root)
            tree.insert(6, tree.root.right)
            tree.insert(4, tree.root.right)
            tree.insert(0, tree.root.right)
            tree.delete(tree.root)
            tree.delete(tree.root.left)

            result = []
            for node in tree.traverse(tree.root):
                result.append(node.data)
            print(result)

    .. code-tab:: c++

        working

    .. code-tab:: java

        working

Graph
-----
:add_edge: O(1)
:delete_edge: O(V)
:neighbor: O(V)

.. tabs::

    .. code-tab:: python

        class Node:
            def __init__(self, data):
                self.data = data
                self.next = None

        class Graph:
            def __init__(self, size):
                self.size = size
                self.adj = [None] * size

            def add_edge(self, s, d):
                temp = Node(d)
                temp.next = self.adj[s]
                self.adj[s] = temp

                temp = Node(s)
                temp.next = self.adj[d]
                self.adj[d] = temp
            
            def delete_edge(self, s, d):
                temp = self.adj[s]
                prev = None
                while temp:
                    if temp.data == d:
                        if prev == None: self.adj[s] = temp.next
                        else: prev.next = temp.next
                    else: prev = temp
                    temp = temp.next

                temp = self.adj[d]
                prev = None
                while temp:
                    if temp.data == s:
                        if prev == None: self.adj[d] = temp.next
                        else: prev.next = temp.next
                    else: prev = temp
                    temp = temp.next

            def neighbor(self, s):
                result = []
                temp = self.adj[s]
                while temp:
                    result.append(temp)
                    temp = temp.next
                return result

        if __name__ == '__main__':
            graph = Graph(5)
            graph.add_edge(0, 1)
            graph.add_edge(0, 2)
            graph.add_edge(0, 4)
            graph.add_edge(1, 2)
            graph.add_edge(1, 3)
            graph.add_edge(1, 4)
            graph.add_edge(2, 3)
            graph.add_edge(3, 4)
            graph.delete_edge(0, 4)
            graph.delete_edge(1, 3)

            result = {}
            for i in range(graph.size):
                result[i] = [v.data for v in graph.neighbor(i)]
            print(result)

    .. code-tab:: c++

        working

    .. code-tab:: java

        working