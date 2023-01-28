# AMQPRPCCall

```typescript
export interface AMQPRPCCall {

    correlationId?: string;
    queue: string;
    message: any;
    options?: Publish;
    timeout?: number;

}
```
