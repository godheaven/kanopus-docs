FROM maven:3.9-eclipse-temurin-21-alpine

# Set the working directory
WORKDIR /app

# Expose the default port (can be overridden at runtime)
EXPOSE 8080

# Define arguments that can be passed at runtime
ENV SPRING_OUTPUT_ANSI_ENABLED=ALWAYS \
    JAVA_OPTS="" \
    SERVER_PORT=8080 \
    SERVER_FORWARD_HEADERS_STRATEGY=none \
    KTOOL_LICENSE_PATH=/kanopus/ktool-pulse/license/license.lic \
    SPRING_DATASOURCE_URL=jdbc:h2:file:/kanopus/ktool-pulse/data/jira-dashboard;DB_CLOSE_DELAY=-1 \
    SPRING_MAIL_HOST=localhost \
    SPRING_MAIL_PORT=1025 \
    SPRING_MAIL_USERNAME="" \
    SPRING_MAIL_PASSWORD=""

# Generate a minimal pom.xml on the fly that depends on the published artifact,
# and then use mvn spring-boot:run to execute it.
# This approach downloads all dependencies from Maven Central at runtime.
CMD ["sh", "-c", "echo \"<project xmlns=\\\"http://maven.apache.org/POM/4.0.0\\\" xmlns:xsi=\\\"http://www.w3.org/2001/XMLSchema-instance\\\" xsi:schemaLocation=\\\"http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd\\\"> \
    <modelVersion>4.0.0</modelVersion> \
    <parent> \
        <groupId>cl.kanopus</groupId> \
        <artifactId>kanopus-boot-parent</artifactId> \
        <version>4.05.1</version> \
    </parent> \
    <groupId>cl.kanopus.docker</groupId> \
    <artifactId>docker-runner</artifactId> \
    <version>1.0.0</version> \
    <dependencies> \
        <dependency> \
            <groupId>cl.kanopus.tool</groupId> \
            <artifactId>ktool-pulse</artifactId> \
            <version>1.0.0</version> \
        </dependency> \
        <dependency> \
            <groupId>cl.kanopus.tool</groupId> \
            <artifactId>ktool-pulse</artifactId> \
            <version>1.0.0</version> \
            <type>sha512</type> \
        </dependency> \
    </dependencies> \
    <build> \
        <plugins> \
            <plugin> \
                <groupId>org.springframework.boot</groupId> \
                <artifactId>spring-boot-maven-plugin</artifactId> \
                <configuration> \
                    <mainClass>cl.kanopus.tool.pulse.Application</mainClass> \
                </configuration> \
            </plugin> \
        </plugins> \
    </build> \
    </project>\" > /app/pom.xml && \
    exec mvn spring-boot:run \
    -Dspring-boot.run.jvmArguments=\\\"${JAVA_OPTS}\\\" \
    -Dspring-boot.run.arguments=\\\"--server.port=${SERVER_PORT} --ktool.license.path=${KTOOL_LICENSE_PATH} --spring.datasource.url=${SPRING_DATASOURCE_URL} --spring.mail.host=${SPRING_MAIL_HOST} --spring.mail.port=${SPRING_MAIL_PORT} --spring.mail.username=${SPRING_MAIL_USERNAME} --spring.mail.password=${SPRING_MAIL_PASSWORD}\\\" \
    -f /app/pom.xml"]
