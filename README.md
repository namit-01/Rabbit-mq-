````md
# RabbitMQ Producer (Quick Revision)

A simple guide to understand and implement a RabbitMQ Producer using Node.js and `amqplib`.

---

## 1. Install Dependency

```bash
npm install amqplib
````

---

## 2. Connect to RabbitMQ

```js
const connection = await amqp.connect(process.env.RABBITMQ_URL);
```

* Creates a connection between the application and RabbitMQ server.

---

## 3. Create Channel

```js
const channel = await connection.createChannel();
```

* Channel is used to communicate with RabbitMQ.
* Publishing and consuming messages happen through channels.

---

## 4. Create / Assert Queue

```js
await channel.assertQueue("queueName", {
    durable: true,
});
```

* Creates the queue if it does not exist.
* Uses the existing queue if it already exists.
* `durable: true` ensures the queue survives RabbitMQ restart.

---

## 5. Publish Message

```js
channel.sendToQueue(
    "queueName",
    Buffer.from(JSON.stringify(message)),
    {
        persistent: true,
    }
);
```

* `Buffer.from()` converts JavaScript data into binary format.
* `persistent: true` makes the message persistent.

---

# Producer Flow

```
Producer
    |
    ↓
Connect to RabbitMQ
    |
    ↓
Create Channel
    |
    ↓
Assert Queue
    |
    ↓
Convert Message to Buffer
    |
    ↓
sendToQueue()
    |
    ↓
RabbitMQ Queue
```

---

# RabbitMQ Producer Lifecycle

```
Install Package
      ↓
Connect
      ↓
Create Channel
      ↓
Create Queue
      ↓
Publish Message
```

---

# Important Keywords

| Keyword     | Meaning                                     |
| ----------- | ------------------------------------------- |
| Connection  | Connects application to RabbitMQ server     |
| Channel     | Communication path used to send messages    |
| assertQueue | Creates queue if it does not exist          |
| Buffer      | Converts JavaScript object into binary data |
| sendToQueue | Sends message to RabbitMQ queue             |
| persistent  | Saves message persistently                  |
| durable     | Queue survives RabbitMQ restart             |

---

## Quick Memory Trick

```
C → C → Q → B → P

Connect
   ↓
Channel
   ↓
Queue
   ↓
Buffer
   ↓
Publish
```

**CCQBP = RabbitMQ Producer Flow**

```
```
