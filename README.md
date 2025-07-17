# Jenkins Infrastruct as Code (IAC)
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

Access Jenkins at: http://localhost:8080