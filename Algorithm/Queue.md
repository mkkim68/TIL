```js
class Queue {
  constructor() {
    this.q = [];
    this.head = 0;
    this.tail = 0;
  }

  enqueue(value) {
    this.q[this.tail++] = value;
  }

  dequeue() {
    return this.q[this.head++];
  }

  peek() {
    return this.q[this.head];
  }

  isEmpty() {
    return this.head === this.tail;
  }

  size() {
    return this.tail - this.head;
  }
}
```