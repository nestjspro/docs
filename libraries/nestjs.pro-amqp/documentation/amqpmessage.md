---
description: Message object for new messages received.
---

# AMQPMessage

## Methods

* **`ack(allUpTo?: boolean)`**: void\
  Acknowledge the message over the channel.
* **`ackAll()`**: void\
  Acknowledge the message over the channel.
* **`nack(allUpTo?: boolean, requeue? boolean)`**: void\
  Acknowledge the message over the channel.
* **`nackAll()`**: void\
  Acknowledge the message over the channel.

## Examples

After retrieving the connection you can cal `subscribe(..)` to begin listening for messages on a queue. Once the message is received from the broker you can do you magic and (optionally) call the above handler methods:

### Acknowledging (simple)

{% code lineNumbers="true" %}
```typescript
amqpService.getConnection('one').subscribe(connection => {
    connection.subscribe({ queue: 'foo.queue' }).subscribe(async message => {
        console.log(message.fromJSON());
        message.handlers.ack();
    });
});
```
{% endcode %}

### Acknowledging (allUpTo)

{% code lineNumbers="true" %}
```typescript
amqpService.getConnection('one').subscribe(connection => {
    connection.subscribe({ queue: 'foo.queue' }).subscribe(async message => {
        console.log(message.fromJSON());
        message.handlers.ack(true);
    });
});
```
{% endcode %}

### Acknowledging (all messages)

{% code lineNumbers="true" %}
```typescript
amqpService.getConnection('one').subscribe(connection => {
    connection.subscribe({ queue: 'foo.queue' }).subscribe(async message => {
        console.log(message.fromJSON());
        message.handlers.ackAll();
    });
});
```
{% endcode %}

### Negative Acknowledging (simple)

{% code lineNumbers="true" %}
```typescript
amqpService.getConnection('one').subscribe(connection => {
    connection.subscribe({ queue: 'foo.queue' }).subscribe(async message => {
        console.log(message.fromJSON());
        message.handlers.nack();
    });
});
```
{% endcode %}

### Negative Acknowledging (allUpto and requeing)

{% code lineNumbers="true" %}
```typescript
amqpService.getConnection('one').subscribe(connection => {
    connection.subscribe({ queue: 'foo.queue' }).subscribe(async message => {
        console.log(message.fromJSON());
        message.handlers.nack(true, true);
    });
});
```
{% endcode %}

### Negative Acknowledging (all messages)

```typescript
amqpService.getConnection('one').subscribe(connection => {
    connection.subscribe({ queue: 'foo.queue' }).subscribe(async message => {
        console.log(message.fromJSON());
        message.handlers.nackAll();
    });
});
```

{% hint style="info" %}
You can use <mark style="background-color:green;">**`message.fromJSON().content`**</mark>to quickly access the returned object.
{% endhint %}

