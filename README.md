# Jenkins + Tomcat + Jolokia (Monitoramento via JMX HTTP)

Este projeto contém orientações para criação de uma imagem Docker personalizada que executa o Jenkins em um servidor Tomcat, com o agente Jolokia habilitado para expor métricas JMX via HTTP.

## 📦 Componentes

- [Jenkins](https://www.jenkins.io/) (modo WAR)
- [Apache Tomcat 9](https://tomcat.apache.org/)
- [Jolokia Agent](https://jolokia.org/) 



##  🖥️ Como executar


### 1.  Crie um diretório e Clone o repositório

`mkdir ~/jenkins-tomcat-jolokia`\
``cd ~/jenkins-tomcat-jolokia``\
``git clone https://github.com/michel-wanderson/jenkins-tomcat-jolokia.git``



### 2. Baixe o arquivo jenkins.war
`wget -O ~/jenkins.war  https://get.jenkins.io/war/2.440/jenkins.war`
``


### 2. Construa a Imagem Docker

``docker build -t jenkins-tomcat-jolokia .``


### 3. Execute o container

``docker run -d -p 8080:8080 --name CNT-JENKINS-TOMCAT-JOLOKIA jenkins-tomcat-jolokia``


## 🌐 Acessos
- **Jenkins Web:** [http://localhost:8080/jenkins](http://localhost:8080/jenkins)
- **Jolokia API:** [http://localhost:8080/jolokia](http://localhost:8080/jolokia)


## 🔍 Verificando métricas via Jolokia
Exemplo de chamada:

`curl http://localhost:8080/jolokia/version`

`curl http://localhost:8080/jolokia/read/java.lang:type=Memory`


# Abrir o Jenkins
Para garantir que o Jenkins está configurado de forma segura pelo administrador, uma senha foi escrita no arquivo de registro, para salva-la e inserir no primeiro acesso via  [http://localhost:8080/jenkins](http://localhost:8080/jenkins)

`docker exec -it CNT-JENKINS-TOMCAT-JOLOKIA cat root/.jenkins/secrets/initialAdminPassword`



---

## 🛠️ Requisitos

- Docker
- Acesso à internet para baixar Jenkins e Jolokia
- Linux (ou compatível com Docker)

---

## 🗂️ Estrutura do projeto
.
*    **jenkins-tomcat-jolokia/**
      *    Dockerfile
      *    jenkins.war
      *    context.xml
