# RabbitMQ Producer (Quick Revision)

1. Install
npm i amqplib

↓

2. Connect
const connection = await amqp.connect(RABBITMQ_URL);

↓

3. Create Channel
const channel = await connection.createChannel();

↓

4. Create / Assert Queue
await channel.assertQueue("queueName", {
    durable: true,
});

↓

5. Publish Message
channel.sendToQueue(
    "queueName",
    Buffer.from(JSON.stringify(message)),
    {
        persistent: true,
    }
);

------------------------------------------------

Flow

Producer
    ↓
Connect
    ↓
Create Channel
    ↓
Assert Queue
    ↓
sendToQueue()
    ↓
RabbitMQ Queue

------------------------------------------------

Keywords

Connection  → Connect to RabbitMQ
Channel     → Publish messages
assertQueue → Create queue if not exists
Buffer      → Convert JS object → Binary
persistent  → Save message to disk
durable     → Queue survives restart
