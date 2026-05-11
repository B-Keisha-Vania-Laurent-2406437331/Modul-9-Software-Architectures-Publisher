## Tutorial A - Reflection

**a. How much data will the publisher send to the message broker in one run?**

In one run, the publisher program sends exactly 5 messages to the message broker. Each message
is a `UserCreatedEventMessage` struct that contains two fields: a `user_id` and a `user_name`.
The five messages represent five different users: Amir, Budi, Cica, Dira, and Emir, each with a
unique user ID from 1 to 5. All five messages are published to the same queue called
`user_created` through the RabbitMQ message broker. So in total, the publisher sends 5 event
messages in a single execution of the program.

**b. What does it mean that the publisher uses the same URL `amqp://guest:guest@localhost:5672`?**

The fact that both the publisher and subscriber use the same URL means they are both connected
to the exact same RabbitMQ message broker instance. The publisher uses this URL to send
messages into the broker, while the subscriber uses the same URL to listen and receive those
messages from the broker. This is the core concept of event-driven architecture, where the
publisher and subscriber do not communicate directly with each other. Instead, they are
decoupled and only interact through the message broker as the middleman. As long as both
programs point to the same broker URL, messages will be delivered correctly from publisher to
subscriber.

### Running RabbitMQ

![RabbitMQ](assets/images/rabbitmq.png)

### Sending and Processing Event

![Publisher](assets/images/publisher.png)
![Subscriber](assets/images/subscriber.png)

When the publisher runs with `cargo run`, it immediately sends 5 event messages to the RabbitMQ
message broker. Each message contains a `UserCreatedEventMessage` with a unique `user_id` and
`user_name`. The publisher does not communicate directly with the subscriber — it simply pushes
the messages into the broker and exits. On the other side, the subscriber is constantly listening
to the `user_created` queue on the same RabbitMQ broker. Once the messages arrive in the
queue, the subscriber picks them up one by one and processes each message by printing it to
the console. This demonstrates the core concept of event-driven architecture, where the
publisher and subscriber are fully decoupled and only interact through the message broker as
the middleman.

### Monitoring Chart Based on Publisher

![RabbitMQ_Spike](assets/images/rabbitmq_spike.png)

The second chart in the RabbitMQ Overview page shows the message rates over the last minute.
Every time the publisher is run with `cargo run`, it sends 5 messages to the broker at once,
which causes a visible spike on the "Message rates" chart. The spike represents the sudden burst
of publish activity hitting the broker in a very short time. After the publisher finishes sending all
5 messages and exits, the rate immediately drops back to 0.0/s, which explains why the spikes
are sharp and narrow. The more times the publisher is run, the more spikes appear on the chart.
This clearly shows the direct correlation between running the publisher and the activity seen on
the RabbitMQ monitoring dashboard.