FROM openjdk:17-slim

ARG VERSION

EXPOSE 9494

ADD target/st2dce-$VERSION.jar app.jar

CMD ["java", "-jar", "app.jar"]
