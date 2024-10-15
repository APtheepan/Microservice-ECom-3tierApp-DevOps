FROM openjdk:17-jdk-slim AS build

RUN apt-get update && apt-get -y install maven

WORKDIR /opt/shipping

COPY pom.xml /opt/shipping/
RUN mvn dependency:resolve
COPY src /opt/shipping/src/
RUN mvn package 


FROM gcr.io/distroless/java17-debian12


#COPY --from=build /opt/shipping .
COPY --from=build /opt/shipping/target/shipping-1.0.jar shipping-1.0.jar

EXPOSE 8080

ENV CART_ENDPOINT=cart:8080
ENV DB_HOST=mysql


CMD ["shipping-1.0.jar"]
#CMD [ "java", "-Xmn256m", "-Xmx768m", "-jar", "shipping-1.0.jar" ]
