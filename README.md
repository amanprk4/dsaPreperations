// <---------------- Data Structure ---------------->

// Linked List

class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class SinglyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }

  // Add Item

  addItemEnd(node) {
    if (!this.head) {
      this.head = node;
      this.tail = node;
    }
    this.tail.next = node;
    this.tail = node;
    this.length++;
  }

  addItemStart(node) {
    if (!this.head) {
      this.head = node;
      this.tail = node;
    }
    node.next = this.head;
    this.head = node;
    this.length++;
  }

  removeFromEnd() {
    if (this.head) {
      let curr = this.head;
      let newTail = curr;
      while (curr.next) {
        newTail = curr;
        curr = curr.next;
      }
      this.tail = newTail;
      this.tail.next = null;
      this.length--;
      return curr;
    }
  }

  removeFromStart() {
    let curr = this.head;
    this.head = this.head.next;
    this.length--;
    return curr;
  }

  getFromAPosition(idx) {
    let counter = 0;
    let curr = this.head;
    while (counter !== idx) {
      curr = curr.next;
      counter++;
    }
    return curr;
  }

  addAtNewPosition(idx, node) {
    const item = this.getFromAPosition(idx - 1);
    const currNext = item.next;
    item.next = node;
    node.next = currNext;
  }

  removeAtPosition(idx) {
    const prevItem = this.getFromAPosition(idx - 1);
    const item = prevItem.next;
    prevItem.next = item.next;
    return item;
  }

  reverseLinkedList() {
    let curr = this.head;
    this.tail = curr;
    let prev = null;
    let next;
    while (curr) {
      next = curr.next;
      curr.next = prev;
      prev = curr;
      curr = next;
    }
    this.head = prev;
  }

  // display all

  displayAll() {
    let curr = this.head;
    while (curr) {
      console.log(curr.value);
      curr = curr.next;
    }
  }
}

// let singleLinkedList = new SinglyLinkedList();

// singleLinkedList.addItemEnd(new Node('Aman'));
// singleLinkedList.addItemEnd(new Node('is'));
// singleLinkedList.addItemEnd(new Node('a'));
// singleLinkedList.addItemEnd(new Node('good'));
// singleLinkedList.addItemEnd(new Node('person'));

// singleLinkedList.addItemStart(new Node('Hello!!'))

// // singleLinkedList.removeFromEnd();
// // singleLinkedList.removeFromStart();
// // console.log(singleLinkedList.getFromAPosition(0))

// singleLinkedList.addAtNewPosition(1,new Node('Mr. '))
// singleLinkedList.removeAtPosition(1);

// singleLinkedList.reverseLinkedList()

// singleLinkedList.displayAll()

// doubly linked list

class Node2 {
  constructor(value) {
    this.value = value;
    this.next = null;
    this.prev = null;
  }
}

// Stacks and Queues

// Stacks
// LIFO principle -> JS call stack, Undo and redo, browser history
// Can be implemented using arrays as well as LinkedList
// If we are using array -> Use push and pop at the end
// If we are using a singly linked list -> use push and pop at the start

class Stack {
  constructor() {
    this.first = null;
    this.last = null;
    this.size = 0;
  }

  // Adding and removing to begin of the list
  push(node) {
    if (!this.first) {
      this.first = node;
      this.last = node;
    } else {
      node.next = this.first;
      this.first = node;
    }
    this.size++;
  }

  pop() {
    if (!this.first) {
      return null;
    }
    if (this.first == this.last) {
      this.first = null;
      this.last = null;
      this.size = 0;
      return null;
    } else {
      const val = this.first;
      this.first = val.next;
      val.next = null;
      this.size++;
      return val;
    }
  }

  displayAll() {
    let curr = this.first;
    while (curr) {
      console.log(curr.value);
      curr = curr.next;
    }
  }
}

// let stack = new Stack();

// stack.push(new Node(1))
// stack.push(new Node(2))
// stack.push(new Node(3))
// stack.push(new Node(4))
// stack.push(new Node(5))
// stack.push(new Node(6))

// console.log(stack.pop())
// console.log(stack.pop())

// stack.displayAll();

// Queue

// FIFO principle
// -> use case: background tasks, printing
// for arrays, use push and shift or unshift and pop
// for linkedList, push at the end and pop from the start

class Queue {
  constructor() {
    this.head = null;
    this.tail = null;
    this.size = 0;
  }

  enqueue(node) {
    if (!this.head) {
      this.head = node;
      this.tail = node;
    } else {
      this.tail.next = node;
      this.tail = node;
    }
    this.size++;
  }

  dequeue() {
    if (!this.head) {
      return null;
    }
    if (this.head === this.tail) {
      this.head = null;
      this.tail = null;
      this.size = 0;
      return this.head;
    }
    const item = this.head;
    this.head = this.head.next;
    this.size--;
    return item;
  }

  displayAll() {
    let curr = this.head;
    while (curr) {
      console.log(curr.value);
      curr = curr.next;
    }
  }
}

// const queue = new Queue();

// queue.enqueue(new Node(1))
// queue.enqueue(new Node(2))
// queue.enqueue(new Node(3))
// queue.enqueue(new Node(4))
// queue.enqueue(new Node(5))

// console.log(queue.dequeue());

// queue.displayAll()

// Binary search trees

// Non linear data structure
// Linked list is a special case of a tree
// HTML is a tree kinda structure
// Network routing
// Abstract syntax tree
// AI

class BSTNode {
  constructor(value) {
    this.left = null;
    this.right = null;
    this.value = value;
  }
}

class BinarySearchTree {
  constructor() {
    this.root = null;
  }

  insert(newNode) {
    if (!this.root) {
      this.root = newNode;
      return;
    }
    const getCorrectPlace = (node, newNode) => {
      if (newNode.value < node.value) {
        if (node.left) {
          return getCorrectPlace(node.left, newNode);
        } else {
          node.left = newNode;
          return;
        }
      } else {
        if (node.right) {
          return getCorrectPlace(node.right, newNode);
        } else {
          node.right = newNode;
          return;
        }
      }
    };
    getCorrectPlace(this.root, newNode);
  }

  find(node) {
    const findNode = (root, node) => {
      if (root.value === node.value) {
        return true;
      } else {
        if (node.value < root.value) {
          if (root.left) {
            return findNode(root.left, node);
          } else {
            return false;
          }
        } else {
          if (root.right) {
            return findNode(root.right, node);
          } else {
            return false;
          }
        }
      }
    };
    return findNode(this.root, node);
  }

  //   Tree traversal

  traverseBFS() {
    const queue = [this.root];
    const visited = [];
    let currNode;
    while (queue.length) {
      currNode = queue.pop();
      if (currNode.left) {
        queue.unshift(currNode.left);
      }
      visited.push(currNode.value);
      if (currNode.right) {
        queue.unshift(currNode.right);
      }
    }
    return visited;
  }
  traverseInOrder() {
    let curr = this.root;
    const visited = [];
    const visitTree = (curr) => {
      if (curr.left) {
        visitTree(curr.left);
      }
      if (curr.right) {
        visitTree(curr.right);
      }
      visited.push(curr.value);
    };
    visitTree(curr);
    return visited;
  }
  traversePreOrder() {
    let curr = this.root;
    const visited = [];
    const visitTree = (curr) => {
      visited.push(curr.value);
      if (curr.left) {
        visitTree(curr.left);
      }
      if (curr.right) {
        visitTree(curr.right);
      }
    };
    visitTree(curr);
    return visited;
  }
  traversePostOrder() {
    let curr = this.root;
    const visited = [];
    const visitTree = (curr) => {
      if (curr.right) {
        visitTree(curr.right);
      }
      if (curr.left) {
        visitTree(curr.left);
      }
      visited.push(curr.value);
    };
    visitTree(curr);
    return visited;
  }
}

const myBST = new BinarySearchTree();

myBST.insert(new BSTNode(23));
myBST.insert(new BSTNode(343));
myBST.insert(new BSTNode(33));
myBST.insert(new BSTNode(87));
myBST.insert(new BSTNode(4));
myBST.insert(new BSTNode(15));

// console.log(myBST.find(new BSTNode(135)));

// console.log(myBST);
// console.log('BFS',myBST.traverseBFS());
// console.log('DFS Preorder',myBST.traversePreOrder());
// console.log('DFS Postorder',myBST.traversePostOrder());
// console.log('DFS InOrder',myBST.traverseInOrder());
/*
Tree traversals

First one is breadth first search
Second one is depth first


3 types of DFS
1. In Order
2. Pre Order
3. Post Order


Pre Order is Node -> Left -> Right
Post order is Left -> Right -> Node
In Order is Left -> Node -> Right

When to use which?
Depends on the tree structure


*/

// Binary heaps

/*
Max children are 2
Max heap -> All the children are less than parent
Min heap -> All children are greater than parent
Left child is added first


Children = ParentIdx*2 + 1, ParentIdx*2 + 2
Parent = Math.floor((Child - 1)/2)

*/

class MaxHeap {
  heap = [];
  constructor() {
    this.heap = [];
  }

  getParentIdx = (childIdx) => Math.floor((childIdx - 1) / 2);
  getChildrenIdx = (parentIdx) => [2 * parentIdx + 1, 2 * parentIdx + 2];
  swap = (idx1, idx2) => {
    [this.heap[idx1], this.heap[idx2]] = [this.heap[idx2], this.heap[idx1]];
  };
  bubbleUp = () => {
    let currIdx = this.heap.length - 1;
    while (currIdx >= 0) {
      const parentIdx = this.getParentIdx(currIdx);
      if (parentIdx < 0) return;
      if (this.heap[parentIdx] > this.heap[currIdx]) {
        return;
      }
      this.swap(parentIdx, currIdx);
      currIdx = parentIdx;
    }
  };

  sinkDown = () => {
    let currIdx = 0;
    while (currIdx < this.heap.length) {
      const [childIdx1, childIdx2] = this.getChildrenIdx(currIdx);
      if (
        childIdx1 &&
        childIdx2 &&
        this.heap[childIdx1] > this.heap[currIdx] &&
        this.heap[childIdx2] > this.heap[currIdx]
      ) {
        if (this.heap[childIdx1] > this.heap[childIdx2]) {
          this.swap(childIdx1, currIdx);
          currIdx = childIdx1;
          continue;
        } else {
          this.swap(childIdx2, currIdx);
          currIdx = childIdx2;
          continue;
        }
      }
      if (childIdx1 && this.heap[childIdx1] > this.heap[currIdx]) {
        this.swap(childIdx1, currIdx);
        currIdx = childIdx1;
        continue;
      }
      if (childIdx2 && this.heap[childIdx2] > this.heap[currIdx]) {
        this.swap(childIdx2, currIdx);
        currIdx = childIdx2;
        continue;
      }
      break;
    }
  };

  addItem(item) {
    this.heap.push(item);
    let last = this.heap.pop();
    this.heap.unshift(last);
    this.sinkDown();
  }

  removeMax() {
    return this.heap.shift();
  }
}

// let maxHeap = new MaxHeap();

// maxHeap.addItem(23);
// // maxHeap.addItem(223);
// maxHeap.addItem(3);
// maxHeap.addItem(87);
// maxHeap.addItem(82);
// maxHeap.addItem(9);
// maxHeap.addItem(84);
// maxHeap.addItem(72);

// console.log(maxHeap.heap)
// console.log(maxHeap.removeMax());
// console.log(maxHeap.removeMax());
// console.log(maxHeap.removeMax());
// console.log(maxHeap.removeMax());
// console.log(maxHeap.removeMax());
// console.log(maxHeap.removeMax());
// console.log(maxHeap.heap)

// Priority Queue

/* 

data structure where each element has a priority associated with it
It is a type of min heap only (since mostly P0 is considered more priority)

*/

class PriorityNode {
  constructor(data, priority) {
    this.data = data;
    this.priority = priority;
  }
}

class PriorityQueue {
  constructor() {
    this.queue = [];
  }

  swap = (idx1, idx2) => {
    [this.queue[idx1], this.queue[idx2]] = [this.queue[idx2], this.queue[idx1]];
  };

  getChildren = (parentIdx) => [2 * parentIdx + 1, 2 * parentIdx + 2];
  getParent = (childIdx) => Math.floor((childIdx - 1) / 2);

  bubbleUp = () => {
    let currIdx = this.queue.length - 1;
    while (currIdx >= 0) {
      const parentIdx = this.getParent(currIdx);
      if (parentIdx < 0) {
        return;
      }
      if (this.queue[parentIdx].priority < this.queue[currIdx].priority) {
        return;
      }
      this.swap(parentIdx, currIdx);
      currIdx = parentIdx;
    }
  };

  enqueueItem(node) {
    this.queue.push(node);
    this.bubbleUp();
  }
}

// const hospitalQueue = new PriorityQueue();

// hospitalQueue.enqueueItem(new PriorityNode('Fracture',1))
// hospitalQueue.enqueueItem(new PriorityNode('TB',4))
// hospitalQueue.enqueueItem(new PriorityNode('fever',20))
// hospitalQueue.enqueueItem(new PriorityNode('Cancer',0))
// hospitalQueue.enqueueItem(new PriorityNode('back pain',15))

// console.log(hospitalQueue.queue);

// Graphs

// Any node with connection between them
// use case -> social network, map, google maps, recommendations

// Two ways to store it. Adjacency matrix and Adjacency list

class Graph {
  constructor() {
    this.adjacencyList = {};
  }

  addVertex(vertexName) {
    this.adjacencyList[vertexName] = [];
  }

  addEdge(v1, v2) {
    this.adjacencyList[v1].push(v2);
    this.adjacencyList[v2].push(v1);
  }

  removeVertex(v) {
    const vertexConnections = this.adjacencyList[v];
    vertexConnections.forEach((vert) => {
      this.adjacencyList[vert] = this.adjacencyList[vert].filter(
        (arr) => arr !== v
      );
    });
    delete this.adjacencyList[v];
  }

  removeEdge(v1, v2) {
    this.adjacencyList[v1] = this.adjacencyList[v1].filter((x) => x !== v2);
    this.adjacencyList[v2] = this.adjacencyList[v2].filter((x) => x !== v1);
  }

  // Graph traversals

  // DFS

  traverseDFS(startPoint) {
    let vertices = []
    const visit = (start,visited={}) => {
      if(visited[start]){
        return;
      }
        visited[start] = true;
        vertices.push(start)
        const neighbors = this.adjacencyList[start];
        for(let neighbor of neighbors){
          visit(neighbor,visited);
        }
    }
    visit(startPoint);
    return vertices;
  }

  traverseDFSIterative(startPoint){
    let stack = [startPoint];
    let visited = {};
    let res = [];
    while(stack.length){
      let curr = stack.pop();
      if(!visited[curr]){
        visited[curr] = true;
        res.push(curr);
        const neighbors = this.adjacencyList[curr];
        for(let neighbor of neighbors){
          if(!visited[neighbor]){
            stack.push(neighbor)
          }
        }
      }
    }
    return res;
  }

  // BFS

  traverseBFS(startPoint) {
    let res = [];
    let visited = {};
    let queue = [startPoint];
    while(queue.length){
      const curr = queue.pop();
      if(!visited[curr]){
        res.push(curr);
        visited[curr] = true;
        const neighbors = this.adjacencyList[curr];
        for(let neighbor of neighbors){
          if(!visited[neighbor]){
            queue.unshift(neighbor);
          }
        }
      }
    }
    return res;
  }
}

const graph = new Graph();

// graph.addVertex('India')
// graph.addVertex('Pakistan')
// graph.addVertex('Germany')
// graph.addVertex('Europe')
// graph.addVertex('Dublin')
// graph.addVertex('Spain')
// graph.addVertex('Sweden')

// graph.addEdge('India','Spain');
// graph.addEdge('Dublin','Pakistan');
// graph.addEdge('Europe','Germany');
// graph.addEdge('Sweden','Europe');

// console.log(graph.adjacencyList);
// graph.removeVertex('Pakistan')
// graph.removeEdge('Germany','Europe')
// console.log(graph.adjacencyList);

// graph.addVertex("A");
// graph.addVertex("B");
// graph.addVertex("C");
// graph.addVertex("D");
// graph.addVertex("E");
// graph.addVertex("F");

// graph.addEdge("A", "B");
// graph.addEdge("D", "B");
// graph.addEdge("D", "F");
// graph.addEdge("D", "E");
// graph.addEdge("F", "E");
// graph.addEdge("C", "E");
// graph.addEdge("A", "C");

// console.log(graph.adjacencyList);
// console.log(graph.traverseDFS('E'))
// console.log(graph.traverseDFSIterative('E'))
// console.log(graph.traverseBFS('E'))





/* 
Dijkstra's Algorithm

Uses priority queue section
Works on a weighted graph
Finds shortest distance between two nodes


*/
