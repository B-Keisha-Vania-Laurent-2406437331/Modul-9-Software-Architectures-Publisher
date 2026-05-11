## Tutorial B - Reflection

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