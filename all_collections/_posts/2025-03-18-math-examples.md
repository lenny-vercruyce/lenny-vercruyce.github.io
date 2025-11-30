---
layout: post
title: Randomness failures
date: 2025-11-30
---

# Randomness failures

Randomness is a key part of many systems, games,security tokens and more. But what many developers realize early on is that randomness in programming isn’t truly random. Computers and programming languages are terrible at being random. However, every programming language handles randomness differently.

Here are some examples:

JavaScript uses Math.random(), which is fast but not cryptographically secure. It’s perfectly fine for animations or small UI tasks but should never be used for passwords or tokens.
Python provides the random module for general use and the secrets module for anything security-related. Mixing them up is a common beginner mistake.
Java and C# have PRNGs that are predictable if you reuse seeds, and their default implementations are not made for situations where you need great security.
Go separates its generators entirely: math/rand for general randomness and crypto/rand for security. This separation prevents accidental misuse, but only if developers know the difference.

One of the most common sources of randomness failure in any language is improper seeding. Without a good seed, the PRNG often produces the same sequence every time the program runs.
Here’s a Go example showing this issue:

```go
package main

import (
    "fmt"
    "math/rand"
)

func main() {
    for i := 0; i < 5; i++ {
        fmt.Println(rand.Intn(100))
    }
}
```
If you run this code multiple times you’ll get the same “random” numbers each time unless you explicitly set a seed. This isn’t a Go specific problem, similar behavior appears in Python, Java, C, and others.
In different languages, randomness failures usually aren’t dramatic. Instead, they cause biased data, predictable outcomes, or subtle security issues. The key is understanding which randomness tool your language provides, when to seed it, and when to switch to a cryptographically secure alternative.
Properly handling randomness ensures your application behaves reliably and remains secure.
