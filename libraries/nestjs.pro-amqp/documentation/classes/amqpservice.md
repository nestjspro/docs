---
description: Manages the lifecycle of all AMQP connections.
---

# AMQPService

<details>

<summary>connect</summary>



</details>

<details>

<summary>getConnection</summary>

## Arguments

1. **`call`**: AMQPRPCCall\
   RPC call configuration object.

## Returns

Observable that emits a reply of type T when it is received.

```typescript
Subject<AMQPMessage<AMQPRPCResponse<T>>>
```

</details>
