# Build stage
FROM openjdk:11 AS BUILD_IMAGE
RUN apt-get update && apt-get install -y maven git && \
    apt-get clean && rm -rf /var/lib/apt/lists/*
RUN git clone https://github.com/uzmaahammad20/vprofile-project.git
WORKDIR /vprofile-project
RUN git checkout docker && mvn install

# Final stage
FROM tomcat:9-jre11
LABEL Project="Vprofile"
LABEL Author="Imran"
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE /vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
