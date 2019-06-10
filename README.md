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
    <storm.eventhubs.version>1.1.0.3</storm.eventhubs.version>
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

### Version 1.1.0.3
===================

1. Update azure-eventhubs client SDK version to 2.3.0.
2. Bolt uses asynchronous sends for improved performance.

