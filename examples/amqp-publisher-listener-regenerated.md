# Publish and receive an order event with RabbitMQ

Create a listener with `AmqpGateway`, then send an event to it with `AmqpChannel`. The integration's default providers establish and manage AMQP connections; you do not need to call `amqplib.connect()`.

## Prerequisites

- Node.js with ESM support and npm.
- Docker for a local RabbitMQ broker.
- A directory for two example files.

Start RabbitMQ in a terminal:

```sh
docker run --rm --name synaptik-rabbit -p 5672:5672 rabbitmq:4
```

In another terminal, initialize an ESM project and install the integration:

```sh
npm init -y
npm pkg set type=module
npm install @sektek/synaptik-amqp
```

## 1. Create the consumer

Save this as `listener.mjs`:

```js
import { AmqpGateway, DefaultChannelProvider } from '@sektek/synaptik-amqp';

const channelProvider = new DefaultChannelProvider({
  connectionOptions: { url: 'amqp://localhost:5672' },
});

const gateway = new AmqpGateway({
  channelProvider,
  queueName: 'orders.example',
  queueOptions: { durable: false },
  prefetch: 1,
  handler: async event => {
    console.log('Received:', event.type, event.data.orderId);
  },
});

await gateway.start();
console.log('Listening on orders.example');

process.once('SIGINT', async () => {
  try {
    await gateway.stop();
  } finally {
    await channelProvider.stop();
  }
});
```

Start it:

```sh
node listener.mjs
```

Wait for `Listening on orders.example`. The gateway declares the queue and starts consuming before it returns from `start()`.

## 2. Create the publisher

Save this as `publisher.mjs`:

```js
import { randomUUID } from 'node:crypto';
import { AmqpChannel, DefaultChannelProvider } from '@sektek/synaptik-amqp';

const channelProvider = new DefaultChannelProvider({
  connectionOptions: { url: 'amqp://localhost:5672' },
});

const publisher = new AmqpChannel({
  channelProvider,
  queueName: 'orders.example',
});

try {
  await publisher.send({
    id: randomUUID(),
    type: 'order.created',
    data: { orderId: 'A-1', total: 42 },
  });
  console.log('Sent order A-1');
} finally {
  await channelProvider.stop();
}
```

In a second terminal, run:

```sh
node publisher.mjs
```

Both components use `DefaultChannelProvider`, which creates its own `DefaultConnectionProvider` from `connectionOptions`. Passing the provider explicitly makes cleanup available through `stop()` while retaining the library-managed connection path.

## 3. Check the result

The publisher should print `Sent order A-1`. The listener should print:

```text
Received: order.created A-1
```

`AmqpGateway` acknowledges a message after the handler resolves. If processing throws, its default behavior is to negatively acknowledge and requeue it. A successful `send()` is not proof that a consumer processed the event.

This example uses RabbitMQ's default exchange and a queue-name routing key. It intentionally starts the listener first so that the queue exists before publishing. The queue is non-durable for this local exercise; it does not demonstrate persistent delivery.

## Clean up

Press Ctrl+C in the listener terminal to stop consuming and close its managed channel/connection. Press Ctrl+C in the RabbitMQ terminal to remove the temporary broker container.

## Troubleshooting

If the listener cannot start, check that RabbitMQ is running and port 5672 is available. If the publisher runs but no event appears, check that the listener printed its ready message and that both scripts use `orders.example`.

## Further reading

See the [Synaptik AMQP reference](https://github.com/sektek/synaptik-amqp#readme) for routing, acknowledgements, connection providers, and request/reply.

---

**Verification record:** **Inspected** against `src/amqp-gateway.ts`, `src/amqp-channel.ts`, `src/default-channel-provider.ts`, `src/default-connection-provider.ts`, and repository guidance. Not executed or type-checked; actual broker delivery, signal handling, and process exit remain unverified.
