def remote = [:]
remote.name = 'test'
remote.host = '54.153.107.132'
remote.port = 22
remote.allowAnyHosts = true

pipeline {
    agent any
     stages {
        stage('Git Clone') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', credentialsId: 'githubID', url: 'https://github.com/akashmukh/Remote-k8s-deployment.git'
            }
        }
     stage('Deployment'){
        steps {
            script {
             // move the new changed 
             withCredentials([usernamePassword(credentialsId: 'new', passwordVariable: 'pass', usernameVariable: 'user')]) {
    // some block
             remote.user = user
             remote.password = pass
             sshPut remote: remote, from: "deploy.yml", into: "."
             sshCommand remote: remote, command: "kubectl apply -f deploy.yml"
             }
           }
          }
        }
      }
    }
