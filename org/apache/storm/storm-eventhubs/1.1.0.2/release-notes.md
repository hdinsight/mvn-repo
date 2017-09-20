## EventHubMessageDataScheme

Release 1.1.0.2 introduces 
1. a new EventHubMessageDataScheme.
    This scheme produces a Tuple with a single object of type '''EventHubMessage'''.

    The EventHubMessage encapsulates the payload of EventData received from EventHub 
    and exposes the AMQP application properties, and System properties for each event
    as first class properties.
2. Configuration property on EventHubSpoutConfig to control the number of events to 
    receive in a single call
    
3. Configuration property to control the number of events pre-fetched by the eventhub
   client.

### Using the new EventHubMessage scheme.

    In the Topology builder:
        EventHubSpoutConfig spoutConfig = new EventHubSpoutConfig(...);
        spoutConfig.setEventDataScheme(new EventHubMessageDataScheme());

    In the bolt:
        public void execute(Tuple tuple, BasicOutputCollector collector) {
            EventHubMessage msg = (EventHubMessage) tuple.getValue(0);
            ///
        }

With this the tuple from the EventHubSpout will have a single object in it.
The object will be of type org.apache.storm.eventhubs.core.EventHubMessage.
    
EventHubMessage supports the following methods:

| Method | Description |
| --- | ---|
| getContent | Returns the EventHub message payload as a byte array |
| readAsString | Returns the EventHub message payload as a String (using Java's default string encoding scheme, which is machine dependant) |
| readAsUtf8String | Returns the EventHub message payload as a UTF8 encoded string |
| readAsUtf16String | Returns the EventHub message payload as a UTF16 encoded string |
| readAsString(Charset ...) | Returns the EventHub message payload as a string encoded using the specified character set |
| getPartitionKey | Returns the partition key for the EventHub message |
| getPartitionId | Returns the partition id in EventHub from which the message was read |
| getEnqueuedTime | Returns the Enqueue time (time at which message entered EventHub) |
| getSequenceNumber | Returns sequence number for the message |
| getApplicationProperties | Returns a Map containtaing application specific AMQP properties set on the message |
| getSystemProperties | Returns a Map containtaing message's system properties (partition key, offset, enqueue time) |

### Specifying number of events to recieve per receive call.
    spoutConfig.setReceiveEventsMaxCount(batchSize);
The above will configure the EventHubSpout to request at most the specified batchsize messages with each receive call.
The received messages are held in a pending buffer and fed to the spout with each nextTuple call.
The idea is to reduce the number of receive calls (1 per event if the batch size is set to 1) made to EventHub.

### Specifying prefetch count on EventHubClient
    spoutConfig.setPrefetchCount(batchSize);
Prefetch value dictates the upper limit of events an EventHub receiver will actively receive regardless of whether a receive operation is pending.
    