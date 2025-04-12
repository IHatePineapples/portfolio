---
title: Ordinary Interview/screening questions
date: 2025-04-13 23:00:00 +0000
categories: Employability
tags: [employability, cpp]  
description: Simple Interview-like QA that I have come accross.
--- 

These are generic questions that I have come accross.

List of common Interview questions+answers for candidates, as well as
recruiters. I regularly update and come back to it.

Answers are short and generic. For the whole picture, read the right book or
check documentation.

The rating is just my personal preference.

## What is an OS (Operating System) ?

> An operating system (OS) is system software that manages computer hardware and
> software resources, and provides common services for computer programs.

Source: <https://en.wikipedia.org/wiki/Operating_system>

**Rating:** ★★★★★

## Why do we need Operating Systems ?

For providing abstraction to the underlying hardware. An E-Mail server only
works by utilising abstraction layers from a kernel. The kernel handles the
tacky hardware communications, while userspace enjoys only having to issue a
`send()` to send data.

**Rating:** ★★★☆☆

## List CPU architectures

Possible answers: RISC-V, ARM, X86, etc..

**Rating:** ☆☆☆☆☆

## What is the difference between Authentication and Authorization ?

Authenticating is proving who you say you are is true.
Authorization is whether you are allowed to perform an action.

For example, at the airport, you might be able to "prove" who you are, but that
doesn't entitle you to board any plane you want. You'll only be authorized to
board your plane, but not others.

**Rating:** ★★★★☆

## How are files protected from unauthorized changes on a computer ?

Depending on the operating system, it is implemented by some kind of underlying access
control policy. Each file has an owner and a policy to enact when other users
interact with the file.

Alice owns `file1`. Bob cannot open this file, but Alice may want to give
read-only access to Bob, or even decide to let him edit it too. Bob cannot give
himself access to `file1` unless Alice allows him to.

**Rating:** ★★★★☆

## What is the difference between a function call and a syscall ?

A function call involves just incremeting/decrementing some register pointer to go read another part of
the process's memory. A `syscall` involves making use of an interrupt, giving
control to the kernel, and back. This is way slower as it
requires synchronisation and kernel-to-user space data copying.

**Rating:** ★★★★★

## What is the difference between the stack vs the heap ?

The stack is staticaly allocated memory to the process, while the heap is
dynamically allocated, on request of the process.

The amount of memory on the stack cannot be changed, while memory on the heap
can be decreased or increased. Processes must do their diligence and `free()`
memory they are not using anymore, to avoid running OOM.

**Rating:** ★★★★★

## What is the difference between a pointer and a reference ?

A reference is a C++ abstraction of a raw pointer. A reference is an "always
dereferenced" pointer, which can never be null and always points to valid
memory. Pointer-arithmetic is not allowed with references.

**Rating:** ★★★★★

## What is the use of a copy-constructor ?

A copy constructor allows for classes/structs to implement their own copying
mechanisms. This is most useful for data structures with pointers, where naive
member copying is not possible.

**Rating:** ★★★★☆

## What is the difference between TCP and UDP ?

TCP guaranties that a packet is received, as well as in the
right order. It can also "adapt" to congestion by gradually resending smaller
and smaller packets, then re-assembling at the destination.

UDP has none of these. It may as well never arrive, neither the client or server
would know. Extra userspace code is required for this, but then why not use TCP ?
;)

Due to this, "bare UDP" is considered faster but "lossy", and is more suitable for
low-latency "loss-forgiving" contexts. Examples include VPNs, Live video
streaming.

**Rating:** ★★★★☆

## How does symmetric encryption work ?

Alice wants to exchange a secret message `m` with Bob. They both have a "key" `k`.
Alice can encrypt the message `m` with `k`, transfer to Bob and he can decrypt
it using `k`.

Encryption/decryption can be performed by ciphers such as AES.

**Rating:** ★★★★★

## Explain what is SSL

SSL is the predecessor to TLS and was the basis for the HTTPS protocol.

**Rating:** ★★★☆☆

## What is an SQL injection ?

An SQL injection is an attack that can be performed on systems that do not
validate or escape user input, preventing from reaching SQL's expansion +
evaluation.

It could just be something like typing the following in a username field :
`where 1=1; --` to bypass login and login randomly.

**Rating:** ★★★★☆

## What to do if we have code that iterates over a large number of elements ?

Parallelise. If you are executing the same operation on all items, use SIMD
instructions to perform this. Consider offloading to GPU (though memory transfer
can be costly). The graal would just be using vectorizing instructions from the
CPU, and avoiding this data transfer, though, this is hardware dependent.

**Rating:** ★★★★★

## What is a virtual class for ?

Basically for generic programming where you have a Dog and Cat class, derived
from an virtual Animal. You can then call non-member function `void bark(Animal&)` with derived classes
and it will dynamically call the right functions for each type. This is because the
"correct" member functions are stored on a table, the infamous `vTable`. Another
way to achieve this, is composition, which is more usable than inheritance.

**Rating:** ★★★★☆

## What are the steps to the TCP 3-way handshake ?

SYN -> SYN-ACK -> ACK. From client to server.

**Rating:** ★★★★☆
