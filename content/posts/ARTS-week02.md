---
title: "ARTS Week02"
date: 2020-07-06T22:21:48+08:00
categories: ["arts"]
---

### Algorithm

#### 第一题

实现指数运算，pow(x, n) 计算出x的n次方。

>Implement [pow(*x*, *n*)](http://www.cplusplus.com/reference/valarray/pow/), which calculates *x* raised to the power *n* (x^n).
>
>Note: 
>
>* -100.0 < x < 100.0
>* n is a 32-bit signed integer, within the range [-2^31, 2^31 - 1]

已知指数运算的几个特性：

1， 任意数的0次方为1；

2，1的n次方依然为1；

3，x为0时，若n为0，值为1；若n不为0，则值为0；

4，当n < 0 时， x^n = 1 / x^-n；



**已知关于指数运算的知识点**

* 0的任意次方为0
* 1的任意次方为1
* 任意数的0次方1
* 如果n < 0, pow(x, n).= 1/pow(x, -n)

解法1，暴力破解

直接遍历n次即可得到，注意处理好边界条件。

```go
func myPow(x float64, n int) float64 {
    if x == 0.0{
        return 0.0
    }
    if x == 1.0{
        return 1.0
    }
    if (n == 0){
        return 1.0
    }
	  iter := n
  	if n < 0{
    	iter = -n
  	}
    val := x
    for i := 1; i < iter; i++{
      val *= x
    }
    if n > 0{
        return val
    }else{
        return  1/ val
    }
}
```

搞定提交。

![暴力法提交结果](/arts/0050-pow-1.png)

不出所料，暴力法不会通过。

但是我们从测试用例可以看到，n非常大，我们改如何改进呢？

由于n很大，想想算法里经常会提到的**divide and conquer**，我们很容易想到，可以将n分成2份

如果n是偶数pow(x, n) = pow(x, n/2) * pow(x, n/2)

如果n是奇数pow(x, n) = pow(x, n/2) * pow(x, n/2) * x

可以看到pow(x, n/2)被计算了两次，如果我们可以把计算过的结果保存下来，则可以加少计算量，减少执行时间。

那一直分到多少才算结束呢？

我们可以举例试试，

n = 1, n/2为0，任意数的0次方为1.0，pow(x, 1) = pow(x, 0) * pow(x, 0) * x = 1.0 * 1.0 * x 

n = 2, n/2 为1，任意数的1次方为它自己，pow(x, 2) = pow(x, 1) * pow(x, 1) = x * x 

n = 3, n/2为1，pow(x, 3) = pow(x, 1) * pow(x, 1) * x= x * x * x

n = 4 .n/2为2，pow(x, 4) = pow(x, 2) * pow(x, 2) 

由此我们可以看到我们已经推算了所有情况。

递归的出口条件为n = 0, n = 1，其他情况均可以分解到这两种基本情况。

解法2

```go
func myPow(x float64, n int) float64 {
    if x == 0.0{
        return 0.0
    }
    if x == 1.0{
        return 1.0
    }
    if (n == 0){
        return 1.0
    }
		iter := n
  	if n < 0{
    	iter = -n
  	}
    m := make(map[int]float64)
    val := inner(x, iter, m)
    if n > 0{
        return val
    }else{
        return  1/ val
    }
}
func inner(x float64, n int, m map[int]float64) float64{
    if n == 0{
        return 1.0
    }
    if n == 1{
        return x
    }
    val, ok := m[n]
    if ok{
        return val
    }else{
        if n % 2 == 0{
            val = inner(x, n/2, m) * inner(x, n/2, m)
        } else{
            val = inner(x, n/2, m) * inner(x, n/2, m) * x
        }
        m[n] = val
        return val
    }
}
```

![解法2结果](/arts/0050-pow-2.png)

## Review

[3 pitfalls in golang I wish to knew](https://betterprogramming.pub/3-pitfalls-in-golang-i-wish-i-knew-3f208a8402a7)

Summarize:

* Closure in Go hold a reference to variable
* `:=` in a if scope will be new variables
* Unlimited Gocoroutines can easily exceed memory limit in small momery machine, Use Work Pool



## Tips:

Why do we need ping/pong heartbeat in WebSocket when TCP has keepalive hearbeat?

**TCP's heartbeat only make sure the socket is alive, not usable**

for example: TCP heartbeat make sure the pipe is unblocked, but it doesn't care if the water plant can supply water normally.

[Do I need to heatbeat to keep a TCP connection open](https://stackoverflow.com/questions/865987/do-i-need-to-heartbeat-to-keep-a-tcp-connection-open)

## Share:

[Meet nanoQ — high-performance brokerless Pub/Sub for streaming real-time data with Golang](https://medium.com/aigent/meet-nanoq-high-performance-brokerless-pub-sub-for-streaming-real-time-data-with-golang-6630d3067f4e)

The author make serveral design decisions to make nanoQ simple to implement and fast.

* when the sub is too slow, just drop the package. There's no need to use buffer.

* Choose TCP over UDP for its congestion control built in and more stable performance.

* Simple but powerful data protocol: Wire Protocol

  ```c
  +--...---+---------...
  |<length>| payload ...
  +--...---+---------...
  ```

> The *<length>* is [Varint](https://developers.google.com/protocol-buffers/docs/encoding) 1–5 octets depending on the payload size.
>
> Varints are a method of serializing integers using one or more bytes. Smaller numbers take a smaller number of bytes.
>
> Each byte in a varint, except the last byte, has the *most significant bit* (msb) set — this indicates that there are further bytes to come. The lower 7 bits of each byte are used to store the two’s complement representation of the number in groups of 7 bits, least significant group first.

* use circular buffer instead of channel as queue, to avoid high gc rate.

