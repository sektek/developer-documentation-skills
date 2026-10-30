# Publish and consume events with RabbitMQ

Use `@sektek/synaptik-amqp` to publish an order event to a RabbitMQ queue and receive it with an `AmqpGateway`.

## Prerequisites

- Node.js and npm with support for ESM.
- A running RabbitMQ broker reachable at `amqp://localhost:5672`. For local development, you can start one with Docker:

  ```sh
  docker run --rm --name synaptik-rabbit -p 5672:5672 rabbitmq:4
  ```

- A project configured for ESM (for example, `"type": "module"` in `package.json`).

Install the integration:

```sh
npm install @sektek/synaptik-amqp amqplib
```

## 1. Start a listener

Create `listener.mjs`:

```js
import { connect } from 'amqplib';
import { AmqpGateway } from '@sektek/synaptik-amqp';

const connection = await connect('amqp://localhost:5672');

const gateway = new AmqpGateway({
  connection,
  queueName: 'orders',
  queueOptions: { durable: true },
  prefetch: 10,
  handler: async event => {
    console.log('Received order:', event.data.orderId);
  },
});

await gateway.start();
console.log('Waiting for orders...');

process.once('SIGINT', async () => {
  await gateway.stop();
  await connection.close();
});
```

Run it in one terminal:

```sh
node listener.mjs
```

Wait until it prints `Waiting for orders...` before publishing.

## 2. Publish an event

Create `publisher.mjs`:

```js
import { randomUUID } from 'node:crypto';
import { connect } from 'amqplib';
import { AmqpChannel } from '@sektek/synaptik-amqp';

const connection = await connect('amqp://localhost:5672');

const channel = new AmqpChannel({
  connectionOptions: { url: 'amqp://localhost:5672' },
  queueName: 'orders',
});

await channel.send({
  id: randomUUID(),
  type: 'order.created',
  data: { orderId: 'A-1', total: 42 },
});

console.log('Published order A-1');
await connection.close();
```

Run it in another terminal:

```sh
node publisher.mjs
```

## 3. Verify delivery

The publisher should print `Published order A-1`. The listener should print `Received order: A-1`. The gateway acknowledges a message after its handler succeeds; if the handler throws, its default behavior is to negatively acknowledge and requeue the message.

The example uses RabbitMQ's default exchange and routes by queue name. It assumes the listener has started and asserted the `orders` queue before the publisher runs. The durable queue declaration does **not** make the message persistent: persistence is a separate publish option.

## Clean up

Stop the listener with Ctrl+C, then stop the Docker container with Ctrl+C in the terminal running RabbitMQ.

## Next steps

See the [Synaptik AMQP README](https://github.com/sektek/synaptik-amqp#readme) for connection ownership, publishing options, acknowledgements, retries, and request/reply.

---

**Authoring verification:** **Inspected** against the existing `sektek/synaptik-amqp` README and public API examples. The JavaScript blocks and Docker command have **not** been executed or type-checked. Connection shutdown and end-to-end delivery should be checked before publishing this as production-ready documentation.
