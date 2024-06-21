#
# Build
#
FROM maven:3.6.3-jdk-11 AS build

WORKDIR /opt/shipping

# Copy the pom.xml and resolve dependencies
COPY pom.xml .
RUN mvn dependency:resolve

# Copy the source code and package the application
COPY src ./src
RUN mvn package

#
# Run
#
FROM openjdk:8-jdk

EXPOSE 8080

WORKDIR /opt/shipping

ENV CART_ENDPOINT=cart:8080
ENV DB_HOST=mysql

COPY --from=build /opt/shipping/target/shipping-1.0.jar shipping.jar

CMD ["java", "-Xmn256m", "-Xmx768m", "-jar", "shipping.jar"]

