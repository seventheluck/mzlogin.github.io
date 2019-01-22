---
layout: post
title: JVM 01 Code execution
categories: Java
description: JVM 01 Code execution
keywords: Java, JVM
---

#### Interpres and Execution compilation
Interpres and execution means translate bytecode to machine code one by one.
Advantage: don't need to wait for copilation.
#### Just-In-Time compilation(JIT)
Execution after compilation the whole method.
Advantage: run faster than above.

Hotspot use the combination of these two methods by default. It interprets the bytecode first. If part of the bytecode executed repeatedly, it will use JIT each method unit.
