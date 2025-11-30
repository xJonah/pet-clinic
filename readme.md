# Pet Clinic

Spring Framework Petclinic App with .gitlab-ci.yml and docker-compose.yml integration.

Original Project - https://github.com/spring-petclinic/spring-framework-petclinic

Application deploys on http://localhost:7500

## Replicate environment

Install Java 17 - `sudo apt install openjdk-17-jre-headless`

Install Maven 3.8.4:

- `wget https://archive.apache.org/dist/maven/maven-3/3.8.4/binaries/apache-maven-3.8.4-bin.tar.gz -P /tmp`
- `sudo tar xf /tmp/apache-maven-*.tar.gz -C /opt`
- `sudo ln -s /opt/apache-maven-3.8.4 /opt/maven`


Configure Maven to use Java 17:

- `sudo nano /etc/profile.d/maven.sh`
  - Add below lines to file:
  - `export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64`
  - `export M2_HOME=/opt/maven`
  - `export MAVEN_HOME=/opt/maven`
  - `export PATH=${M2_HOME}/bin:${PATH}`
- `sudo chmod +x /etc/profile.d/maven.sh`
- `source /etc/profile.d/maven.sh`

Runner Configuration:

- Runner 1 - shell executor, Run untagged jobs.
- Runner 2 - docker executor, ruby:2.7, tags=sast-runner,sca-runner,secret-runner,container-scan-runner,unit-runner


Troubleshooting:

- Unit test stage ("java") is supposed to fail. Unit tests which would not pass were intentionally written.
- If getting "cannot connect to the server" error for GitLab CI/CD tool stages (SAST, Secret, Container, SCA):
  - Set GitLab external URL to IP and not localhost
  - Register runners with the server IP and not localhost
