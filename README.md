# Eureka Service

This repository contains the Eureka Server implementation for service discovery in a microservices architecture. The Eureka Server acts as a registry where all microservices register themselves and discover other services.

## Features

- **Service Discovery**: Centralized registry for microservices.
- **Spring Cloud Integration**: Built with Spring Cloud Netflix.
- **High Availability**: Can be scaled for fault tolerance.

## Prerequisites

- **Java 17 or higher**
- **Gradle 7.0+**
- **Spring Boot 3.0+**

## Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/Cloudinator/cloudinator-api-eureka.git
cd cloudinator-api-eureka
```

### 2. Build the project
```bash
./gradlew clean build
```

### 3. Run the application
```bash
./gradlew bootRun
```

### 4. Access the Eureka Dashboard
Open your browser and navigate to [http://localhost:8761](http://localhost:8761).

## Configuration

### application.yaml
Below is the configuration for the Eureka Server:
```yaml
spring:
  application:
    name: eureka

server:
  port: 8761

eureka:
  client:
    fetch-registry: false
    register-with-eureka: false
```

## Code

### Main Application Class
The `EurekaApplication` class enables the Eureka Server:

```java
package istad.co.eureka;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.eureka.server.EnableEurekaServer;

@SpringBootApplication
@EnableEurekaServer
public class EurekaApplication {

    public static void main(String[] args) {
        SpringApplication.run(EurekaApplication.class, args);
    }

}
```

## Build Configuration

### build.gradle
The project uses Gradle for build and dependency management:

```groovy
plugins {
    id 'java'
    id 'org.springframework.boot' version '3.3.5'
    id 'io.spring.dependency-management' version '1.1.6'
}

group = 'istad.co'
version = '0.0.1-SNAPSHOT'

java {
    toolchain {
        languageVersion = JavaLanguageVersion.of(17)
    }
}

repositories {
    mavenCentral()
}

ext {
    set('springCloudVersion', "2023.0.3")
}

dependencies {
    implementation 'org.springframework.cloud:spring-cloud-starter-netflix-eureka-server'
    testImplementation 'org.springframework.boot:spring-boot-starter-test'
    testRuntimeOnly 'org.junit.platform:junit-platform-launcher'
}

dependencyManagement {
    imports {
        mavenBom "org.springframework.cloud:spring-cloud-dependencies:${springCloudVersion}"
    }
}

tasks.named('test') {
    useJUnitPlatform()
}
```

## Testing

### Using the Eureka Dashboard
- Open [http://localhost:8761](http://localhost:8761) in your browser.
- Verify that the Eureka dashboard loads successfully.

### Unit Testing
Run the tests using Gradle:
```bash
./gradlew test
```

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

For any questions or issues, feel free to open an issue or contact the maintainer.
