pipeline {
  agent any
  stages {
    stage ('Build backend') {
      steps {
        sh 'mvn clean package -DskipTests=true'
      }
    }
    stage ('Unit Tests') {
      steps {
        sh 'mvn test'
      }
    }
    stage ('Sonar Analysis') {
      environment {
        scannerHome = tool 'SONAR_SCANNER'
      }
      steps {
        sh "${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=DeployBack -Dsonar.host.url=http://192.168.1.157:9000 -Dsonar.login=a6b0a4ad6f009f5ae9b53ab49bf39766dd180c07 -Dsonar.java.binaries=target"
      }
    }
    stage ('Quality Gate') {
      steps {
        sh "echo foi o quality gate"
      }
    }
    stage ('Deploy Backend') {
      steps {
        deploy adapters: [tomcat8(credentialsId: 'TomcatLogin', path: '', url: 'http://192.168.1.157:8001/')], contextPath: 'tasks-backend', war: 'target/tasks-backend.war'
      }
    }
    stage ('API test') {
      steps {
        sh 'echo testes de API'
      }
    }
  }
}