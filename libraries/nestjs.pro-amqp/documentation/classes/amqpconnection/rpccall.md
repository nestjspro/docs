# rpcCall

## Arguments

1. **`call`**: [AMQPRPCCall](../../types/amqprpccall.md)\
   RPC call configuration object.

## Returns

Observable that emits a reply of type T when it is received. `Subject<`[`AMQPMessage`](../../types/amqpmessage.md)`<`[`AMQPRPCResponse`](../../types/amqprpcresponse.md)`>>`



## Examples

This example will make an RPC call and wait for the reply to be returned by the receiver on the other side:

{% code lineNumbers="true" %}
```typescript
connection.rpcCall<User>({
    queue: 'rbac.rpc',
    message: {
        serviceName: 'usersService',
        methodName: 'getById',
        args: [ decoded['id'] ]
    }
}).subscribe(response => {
    console.log(reponse);
});
```
{% endcode %}

The receiver is subscribed to the `rbac.rpc` queue for incoming requests.&#x20;

Once a request is received, the receiver will create a special "one-to-one" queue between you and it so that the response can be sent back.

An instance of [AMQPRPCResponse](../../types/amqprpcresponse.md) is emitted on the observable. Once you've executed on your requirements, you must call **`response.ack()`** to acknowledge the message so that it drops off of the queue.

{% hint style="info" %}
You can use <mark style="background-color:green;">**`response.fromJSON().content`**</mark>to quickly access the returned object.
{% endhint %}

