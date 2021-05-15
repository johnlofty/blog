---
title: "ARTS Week03"
date: 2021-04-11T11:59:40+08:00
categories: ["arts"]
GHissueID: 3
draft: false
---

### Algorithm

#### 实现时间复杂度为O(1)的LRU

LRU为Least Recently Used的缩写，意思是最近最少使用，常用来作为一种热数据淘汰机制，使用很广泛。

涉及到的操作有：

1. 新的数据放入队尾
2. 队列满时，从队头淘汰数据
3. 放入已经在队列里的数据时，从原先位置取出，放入队尾。

本题的重点是要在O(1)的时间复杂度里完成所有操作，什么数据结构可以在O(1)的时间复杂度里完成上述操作呢？

答案是Double Linked List

选择好合适的数据结构后，剩下的就很简单了。

```python
class Node:
    def __init__(self, k, v):
        self.k = k
        self.v = v
        self.next = None
        self.prev = None

class LRUCache:

    def __init__(self, capacity: int):
        self.cap = capacity
        self.map = {}
        self.root = root = Node(None, None)
        root.prev = root.next = root

    def get(self, key: int) -> int:
        node = self.map.get(key)
        if not node:
            return -1
        else:
            prev_node = node.prev
            next_node = node.next
            next_node.prev = prev_node
            prev_node.next = next_node

            node.next = self.root
            node.prev = tail_node = self.root.prev
            self.root.prev = tail_node.next = node
            return node.v
        

    def put(self, key: int, value: int) -> None:
        node = self.map.get(key)
        if not node:
            node = Node(key, value)
            node.next = self.root
            node.prev = tail_node = self.root.prev
            self.root.prev = tail_node.next = node
            self.map[key] = node
            if len(self.map) > self.cap:
                self.pop()
        else:
            prev_node = node.prev
            next_node = node.next
            next_node.prev = prev_node
            prev_node.next = next_node

            node.next = self.root
            node.prev = tail_node = self.root.prev
            self.root.prev = tail_node.next = node
            node.v = value

    def pop(self):
        first_node = self.root.next
        next_node = first_node.next
        next_node.prev = self.root
        self.root.next = next_node
        self.map.pop(first_node.k)

```

需要注意的点是，在操作链表时，别让链表断开。

root节点在初始化时，可以让root节点的next, prev都指向自己，方便后面处理。

### Review

Golang Builder Pattern

通过使用不同阶段的Methods，实现对结构体数据的初始化。

[Go Builder Pattern](https://devcharmander.medium.com/design-patterns-in-golang-the-builder-dac468a71194)


### Tips

#### 如何减少docker image的体积
利用多阶段编译(multi-stage builds，可以有效缩小Docker生成image的大小.
multi-stage builds将编译环境与运行环境分开。
如果运行环境选择alpine，生成的镜像体积大约80MB左右。

```dockefile
FROM golang:1.16
WORKDIR /go/src/github.com/alexellis/href-counter/
RUN go get -d -v golang.org/x/net/html  
COPY app.go .
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .

FROM alpine:latest  
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=0 /go/src/github.com/alexellis/href-counter/app .
CMD ["./app"]  
```
#### Reference:
[multistage-build](https://docs.docker.com/develop/develop-images/multistage-build/)

### Share

测试某个主机的某个端口是否畅通的时候，可以很方便使用nc命令做到。
```bash
$ nc -z -v -w 3 baidu.com 80
Connection to baidu.com 80 port [tcp/http] succeeded!
```
-z 用来扫描端口，并不会发送任何数据

-x 用来使用代理
