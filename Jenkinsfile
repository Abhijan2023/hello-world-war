pipeline{
    agent tomcat-docker-agent
environment {
		DOCKER_LOGIN_CREDENTIALS=credentials('abhishekp006')
	}
    stages {
  stage('checkout') {
    steps {
      git 'https://github.com/Abhijan2023/hello-world-war.git'
    }
  }

  stage('build') {
    steps {
      sh 'mvn clean install'
      sh 'docker build -t abhishekp006/abhishek:$BUILD_NUMBER .' 

    }
  }

  stage('push') {
    steps {
      sh 'echo $DOCKER_LOGIN_CREDENTIALS_PSW | docker login -u $DOCKER_LOGIN_CREDENTIALS_USR --password-stdin'
      sh 'docker push abhishekp006/abhishek:$BUILD_NUMBER'
    }
  }

  stage('deploy') {
    steps {
      sh "docker run -itd -p 8080:8080 abhishekp006/abhishek:$BUILD_NUMBER"
    }
  }

}

}
