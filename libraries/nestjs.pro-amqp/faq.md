---
description: What is RPC and more...
---

# FAQ

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

<details>

<summary>What is RPC with AMQP?</summary>

Typically you publish messages as a sender (or client) and move on. On the other side of the queue, there are subscribers (or receivers) that pick up the messages and do work either immediately or at a later time (also known as working "offline").

What if we need to run a function on a remote computer and wait for the result? This pattern is commonly known as [Remote Procedure Call](https://en.wikipedia.org/wiki/Remote\_procedure\_call) or "RPC".



</details>

<details>

<summary>What is a message broker?</summary>

A message broker is an intermediary that transfers messages from sender to receiver(s).&#x20;

It is an architectural pattern for inspecting, relaying, and distributing messages, mediating between applications, and simplifying communication between them.&#x20;

The main task of a Message broker is to receive messages from applications and perform some action.

</details>

<details>

<summary>What is RabbitMQ?</summary>

RabbitMQ is the most widely deployed open-source [message broker](faq.md#what-is-a-message-broker).

It can be deployed in a few minutes locally, in docker, kubernetes, or as a standalone service on most all operating systems.

\


</details>
