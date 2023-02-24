pipeline {
  agent any
  // any, none, label, node, docker, dockerfile, kubernetes
  tools{
    maven 'my_mavenh'
  }
  environment {
    gitName = 'std-yong'
    gitEmail = 'std-yong@github.com'
    gitWebaddress = 'https://github.com/std-yong/sb_code.git'
    gitSshaddress = 'git@github.com:std-yong/sb_code.git'
    gitCredential = 'git_cre' //github credential 생성시의 ID
  }

  stages {
    stage('Checkout Github') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: gitCredential, url: gitWebaddress]]])
      }
      post {
        failure {
            echo 'Repository clone failure'
        }
        success {
            echo 'Repository clone success'
        }
      }
    }
      stage('Maven Build') {
      steps {
        sh 'mvn clean install'
        // maven 플러그인이 미리 설치 되어있어야 함
        }
        post {
            failure {
                echo 'Maven build failure'
            }
            success {
                echo 'Maven build success'
            }
        }
    }

  }
}
