```js
class Deque {
  constructor() {
    this.q = [];
    this.head = 0;
    this.tail = 0;
  }

  pushFront(value) {
    this.head--;
    this.q[this.head] = value;
  }

  pushBack(value) {
    this.q[this.tail++] = value;
  }

  popFront() {
    return this.q[this.head++];
  }

  popBack() {
    return this.q[--this.tail];
  }

  front() {
    return this.q[this.head];
  }

  back() {
    return this.q[this.tail - 1];
  }

  isEmpty() {
    return this.head === this.tail;
  }

  size() {
    return this.tail - this.head;
  }
}
```