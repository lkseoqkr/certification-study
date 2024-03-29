# Need for Asynchronous Communication

# Synchronous Communication
- Web Server -> logging service -> DB
- What if your logging service goes down?
  - Will the applications go down too?
- What if all of sudden, there is high load and there are lot of logs coming in?
  - Log Service is not able to handle the load and goes down very o�en
# Asynchronous Communication - Decoupled
- Web Server -> MQ -> logging service -> DB
- Create a topic and have your applications put log messages on the topic
- Logging service picks them up for processing when ready
- Advantages
  - Decoupling: Publisher (Apps) don't care about who is listening
  - Availability: Publisher (Apps) up even if a subscriber (Logging Service) is down
  - Scalability: Scale consumer instances (Logging Service) under high load
  - Durability: Message is not lost even if subscriber (Logging Service) is down
# Pub/Sub
- Reliable, scalable, fully-managed asynchronous messaging service
- Backbone for Highly Available and Highly Scalable Solutions
# Pub/Sub - How does it work?
- Publisher - Sender of a message
  - Publishers send messages by making HTTPS requests to pubsub.googleapis.com
- Subscriber - Receiver of the message
  - Pull - Subscriber pulls messages when ready
    - Subscriber makes HTTPS requests to pubsub.googleapis.com
  - Push - Messages are sent to subscribers
    - Subscribers provide a web hook endpoint at the time of registration
    - When a message is received on the topic, A HTTPS POST request is sent to the web hook endpoints
  - Very Flexible Publisher(s) and Subscriber(s) Relationships
    - One to Many, Many to One, Many to Many
# Pub/Sub - Getting Ready with Topic and Subscriptions 
- (mobile/On-prem/IoT) -> (Topic -> Subscription1/Subscription2/Subscription3) -> (Datawarehouse/Microservice/Legacy-3rd party services)
- Step 1 : Topic is created
- Step 2 : Subscription(s) are created
  - Subscribers register to the topic
  - Each Subscription represents discrete pull of messages from a topic:
    - Multiple clients pull same subscription
      - => messages split between clients
    - Multiple clients create a subscription each
      - => each client will get every message
# Pub/Sub - Sending and Receiving a Message
- Publisher sends a message to Topic
- Message individually delivered to each and every subscription
- Message(s) are removed from subscriptions message queue
  - Pub/Sub ensures the message is retained per subscription until it is acknowledged

