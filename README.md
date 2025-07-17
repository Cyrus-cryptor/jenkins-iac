# Jenkins Infrastructure as Code (IAC)
  - configuration as code (``casc``)
  - manager plugins with ``plugins.txt``

## Running Jenkins with Docker

To run Jenkins with the Configuration as Code setup:

```bash
docker run -p 8080:8080 -p 50000:50000 \
  -v "$(pwd)/config":/var/jenkins_home/casc_configs \
  -v "$(pwd)/plugins.txt":/usr/share/jenkins/ref/plugins.txt \
  -e CASC_JENKINS_CONFIG=/var/jenkins_home/casc_configs \
  jenkins/jenkins:lts
```

This will:
- Mount your local `config/` directory to the Jenkins container
- Mount `plugins.txt` to install specified plugins
- Set the CASC configuration path
- Expose Jenkins on port 8080
- Expose Jenkins agent port on 50000

## Plugin Installation

The Jenkins Docker image automatically runs `jenkins-plugin-cli --plugin-file /usr/share/jenkins/ref/plugins.txt` during container startup when it finds a `plugins.txt` file. You don't need to run this command manually - Jenkins will automatically install all plugins listed in `plugins.txt` during initialization.

Access Jenkins at: http://localhost:8080