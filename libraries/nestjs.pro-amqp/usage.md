# Usage



## Initializing

### Minimum Configuration

A minimum configuration that gets you connected to your AMQP server like RabbitMQ locally without creating any exchanges or queues:

{% code title="app.module.ts" lineNumbers="true" %}
```typescript
import { AMQPModule } from '@nestjs.pro/amqp';
import { Module } from '@nestjs/common';

@Module({
    imports: [
        AMQPModule.forRoot({
            autoConnect: true,
            connections: [
                {
                    url: 'amqp://guest:guest@localhost:5672'
                }
            ]
        })
    ]
})
export class AppModule {}
```
{% endcode %}

### Typical Configuration

Typical configuration creating an exchange and queue (if they do not already exist) including setting up bindings:

```typescript
import { AMQPModule } from '@nestjs.pro/amqp';
import { Module } from '@nestjs/common';

@Module({
    imports: [
        AMQPModule.forRoot({
            autoConnect: true,
            logLevel: AMQPLogLevel.INFO,
            connections: [
                {
                    name: 'awesome',
                    url: 'amqp://guest:guest@localhost:5672',
                    exchange: {
                        name: 'my_exchange',
                        type: 'topic',
                        options: {
                            durable: true
                        }
                    },
                    queues: [
                        {
                            name: 'send_email',
                            routingKey: 'send_email',
                            createBindings: true,
                            options: {
                                durable: true
                            }
                        }
                    ]
                }
            ]
        })
    ]    
})
export class AppModule {}
```

## The Service

## Messaging Patterns

### RPC

```typescript
amqpService.getConnection().subscribe(connection => {
    connection.rpcCall<User>({
        queue: 'rbac.rpc',
        message: {
            serviceName: 'usersService',
            methodName: 'getByEmail',
            args: [ 'matthew@matthewdavis.io' ]
        }
    }).subscribe(response => {
        const user = response.fromJSON().content;
        console.log(`User id returned from RPC call: ${ user.email }`);
    });
});
```

### Publishing

```typescript
this.amqpService.getConnection().subscribe(connection => {
    connection.reference.channel.publish(
        'my_exchange',
        'send_email',
        Buffer.from(JSON.stringify(camera))
    );
});
```

### Subscribing

```typescript
amqpService.getConnection().subscribe(connection => {
    const messages$ = connection.subscribe({ queue: 'send_email' });
    messages$.subscribe(message => {
        const email = message.fromJSON();
        try {
            MyEmailClient.send(email);
            message.ack();
        } catch(e) {
            /**
             * Handle exception, log, etc.
             * Message will be requeued if you do not call message.ack()!
             */
            logger.error(e);
        }
    });
});
```
