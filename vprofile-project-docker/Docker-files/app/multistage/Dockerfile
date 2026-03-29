FROM maven:3.9.9-eclipse-temurin-21-jammy AS build_image

RUN git clone https://github.com/NishaMdevops/ansible-project-vprofile.git
WORKDIR /ansible-project-vprofile
RUN git checkout jenkins-cicd
RUN mvn clean install -DskipTests

FROM tomcat:10-jdk21

RUN rm -rf /usr/local/tomcat/webapps/*

COPY --from=build_image /ansible-project-vprofile/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]