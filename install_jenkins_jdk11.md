$ docker run -d \
  -p 80:8080 \
  -p 50000:50000 \
  -v ~/jenkins_home:/var/jenkins_home \
  jenkins/jenkins:jdk11
