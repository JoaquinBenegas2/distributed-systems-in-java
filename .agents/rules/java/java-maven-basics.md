# Maven Basics

## Role

You are a Senior Java engineer ensuring proper Maven project structure.

## Project Structure

Follow standard Maven directory layout:

```
project/
├── pom.xml
├── src/
│   ├── main/
│   │   ├── java/
│   │   └── resources/
│   └── test/
│       ├── java/
│       └── resources/
└── README.md
```

## POM Best Practices

### Minimal POM Structure

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    
    <groupId>com.example</groupId>
    <artifactId>circuit-breaker</artifactId>
    <version>1.0.0</version>
    
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <junit.version>5.10.0</junit.version>
    </properties>
    
    <dependencies>
        <!-- Test dependencies -->
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter</artifactId>
            <version>${junit.version}</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
    
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.11.0</version>
                <configuration>
                    <source>17</source>
                    <target>17</target>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>3.1.2</version>
            </plugin>
        </plugins>
    </build>
</project>
```

## Essential Dependencies

### Testing

* `junit-jupiter` (JUnit 5) - always include for tests
* `assertj-core` - fluent assertions (optional but recommended)
* `mockito-core` - mocking (when needed)

### Logging

* `slf4j-api` - logging facade
* `logback-classic` - logging implementation

## Common Maven Commands

```bash
# Compile
mvn clean compile

# Run tests
mvn test

# Package
mvn clean package

# Run main class
mvn exec:java -Dexec.mainClass="com.example.Main"
```

## Best Practices

* **Use properties** for version management
* **Specify Java version** explicitly in compiler plugin
* **Keep dependencies minimal** - only add what's needed
* **Use appropriate scopes**: `test` for test-only dependencies
* **Document dependencies** - explain why each dependency is needed
