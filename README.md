## How to use this repository

In your pom.xml file add the below section.

```  
  <repository>
      <id>hdinsight-examples</id>
      <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
  </repository>
```

To use the eventhub-spout jar add the following dependency:

```
 <properties>
    <storm.eventhubs.version>1.1.0.2</storm.eventhubs.version>
 </properties>
 
 <dependencies>
 <dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-eventhubs</artifactId>
    <version>${storm.eventhubs.version}</version>
 </dependency>
 ...
```

## Release Notes

### Version 1.1.0.2
===================

1. Update azure-eventhubs client SDK version to the 0.14.5
2. Remove BinaryEventDataScheme, and EventDataScheme serialization schemes
3. Introduce a new EventHubMessage based EventHubMessageDataScheme that encapsulates the payload as well as AMQP and System properties.
