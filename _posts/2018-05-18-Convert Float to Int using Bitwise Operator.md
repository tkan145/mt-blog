---
layout: post
title:  "Convert Float to Int using Bitwise Operator"
date:   2018-05-18 21:24:14 +1000
categories: javascript trick
---

Recently there is a trick that I use very often, which is to use two bitwise NOT ~~ to quickly convert some floats to int, instead of using the Math.floor function:

```javascript
~~(5.43251) == 5 //true
Math.floor(5.43251) == 5 //true
```

This trick can improve the performance of your code base. So how does this work?

Essentially, all numeric types in JavaScript take up 64-bit in memory [IEEE 754] (http://speakingjs.com/es5/ch11.html#number_representation)

![markup]({{site.url}}/assets/images/javascript-float.png)

To save memory and improve performance,with most JavaScript engines (such as V8, SpiderMoney ...) if a numeric variable `x` has a small integer value (eg: −231≤x≤231), that variable will be expressed as [32-bit integer](http://speakingjs.com/es5/ch11.html#integers). If the number has large enough value, or it is not an integer, it is automatically converted to 64-bit format.

According to the ECMAScript specification, when we performing bitwise operations, the operands are automatically converted to 32-bit interger. That is when we perform any bitwise operation o a number, the result is always a 32-bit integer.

And usally, we will use nonsense bitwise operators to avoid changeing the value of intial number, for example:
```javascript
~~(5.423451) == 5 // Double not
5.423451 | 0 == 5 // Or with 0
5.423451 << 0 == 5 // Shift 0
5.423451 >> 0 == 5 // Shift 0
```

We can use this trick for a lot of situations. For example, the algorithm check for a number that is a power of 4 or not.

If an integer n∈Z is the fourth power of some `x` then `x` must also be an interger (x∈Z). In other words, the logarithmic base 4 of n must also be an integer (log4n∈Z).

The logarithm logab can be computed from the logarithms of b and a with respect to an arbitrary base k (for example log10) using the following formula:
```
logab = log10b/ log10a
```

Our algorithm will be implemented as follows:
```javascript
    var isPowerOfFour = function(num) {
    let lg4 = Math.log(num) / Math.log(4);
    return lg4 === (~~lg4);
};
```