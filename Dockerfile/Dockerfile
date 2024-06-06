# Usa la imagen oficial de Jenkins LTS como base
FROM jenkins/jenkins:lts

# Copia el archivo de plugins al contenedor
COPY ../plugins.txt /usr/share/jenkins/ref/plugins.txt

# Instala los plugins listados en plugins.txt
RUN jenkins-plugin-cli --plugin-file /usr/share/jenkins/ref/plugins.txt

# Copia la configuración de JCasC al directorio de configuración de Jenkins
COPY ../jenkins.yaml /var/jenkins_home/casc_configs/jenkins.yaml

# Establece la variable de entorno para que Jenkins use el archivo de configuración JCasC
ENV CASC_JENKINS_CONFIG=/var/jenkins_home/casc_configs/jenkins.yaml
ENV JAVA_OPTS=-Djava.awt.headless=true -XX:+UseStringDeduplication

# Expone el puerto 8080 para la interfaz web de Jenkins y el puerto 50000 para agentes
EXPOSE 8080 50000

# Inicia Jenkins
CMD ["java", "-Djenkins.install.runSetupWizard=false", "-jar", "/usr/share/jenkins/jenkins.war"]
