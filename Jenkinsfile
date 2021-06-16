def remote = [:]
remote.name = 'test'
remote.host = '<remote IP>'
remote.port = 22
remote.allowAnyHosts = true

pipeline {
    agent any
     stages {
        stage('Git Clone') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', credentialsId: '4af18a21-3317-4da0-85bc-1fbffb60821b', url: ''
            }
        }
     stage('Deployment'){
        steps {
            script {
             // move the new changed 
             withCredentials([usernamePassword(credentialsId: 'remoteuserID', passwordVariable: 'pass', usernameVariable: 'user')]) {
             remote.user = user
             remote.password = pass
             sshPut remote: remote, from: "deploy.yml", into: "/home/akash"
             sshCommand remote: remote, command: "kubectl apply -f deploy.yml"
             }
           }
          }
        }
      }
    }
