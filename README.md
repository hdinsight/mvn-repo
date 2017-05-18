## How to use this repository

In your pom.xml file add the below section.

```  
  <repository>
      <id>hdinsight-examples</id>
      <url>http://raw.github.com/hdinsight-storm-examples/mvn-repo</url>
  </repository>
```

To use the eventhub-spout jar add the following dependency:

```
 <properties>
    <storm.eventhubs.version>1.1.0.2.6.0.3-8</storm.eventhubs.version>
 </properties>
 
 <dependencies>
 <dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-eventhubs</artifactId>
    <version>${storm.eventhubs.version}</version>
 </dependency>
 ...
```
