pipeline {
  agent any

  environment {
    NODE_VERSION = '20' 
    STAGING_VM = '10.10.11.216'
    PRODUCTION_VM = '10.10.11.205' 
    PRODUCTION_PORT = '80' 
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build and Test') {
      steps {
        sh 'apt-get install -y nodejs'
        sh 'npm install express'
        sh 'node -test'
      }
    }

    stage('Deploy to Staging') {
      steps {
        withCredentials([sshUserPrivateKey(credentialsId: 'my-ssh-credentials', keyFileVariable: 'MIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQC7r1c43z6pT5Qa
3lhzB/jpUy1zxEcMkrcN19kV/5pLsn+Hd8MJTgveS6qL3ohq9qY2L/0vU0tQELkL
q4Kp7VmEs62Y/KZuUXF8Kw6m8TtnW+sdA/9hz/NPwWUrUvhhP8BqkxPRb3y/Qw0G
XUZIXkHAvxVUfEcr+DJv+Ar6qg8QbRUsr8H5ReGF9Fd6e7mQOAJgtfzRY3OAlknd
9uJJ1Pm9lnjFhItsm1RVs91KEQzFqwmO/g39t3wwnCJZ5XqNvpKDEf+k+G7JzrlH
Zl1MdsBGFIO2yLTMWfEvoznqAI4Gt+Q97VYx6wcm7rdYOZS54VR5b+ffbiQFD23T
EY1H+7E/AgMBAAECggEAFYFjUaI68wHlnaekZ57nTtY25LJQYVYsoyy+zfl9tSiC
3BX5Q3kOJ0ULzj6ZnpOZOGuSgXqnpW10VvJHGRstEq31Uq/LjYYE1zJGkAq1mjiZ
Y7zakLDe7j6yCLpUbHBjM0T/4dZKoX6Rm/GgbwOfmCS4KNR25jJZiO3BBy/bT6ut
zc2fSEJOM3bK8rX7J+4x6nFFomvDypOfHm6U0ExqlR72B1fOr28ad6aj5J12D8qS
Zbe3qQRbCobPkOHOkYp96sFJYjrtnSozsdm8MgZYNaa4jUMmZTsgin36DQeTb76n
jXNmZM0f2ejVxW6Rgn6M9NoJIBR/Yc5/EmIW6JPgrQKBgQDhGzSCATfL3em7Aw/Q
cR9noYIR1ttZ5OR3NEpECtmBqFJBFzS75JQv/m87OZ7P3oEP3nR2AN3W2SRooN2Q
VITAYy6dKYbU86S8/YvIkS8o+GLN3xRjViQF/nv/WHglwCKIPbQh/2AJU/qol7yG
/hb6J/k5M3FuXFHhfeYK6W76YwKBgQDIiZ+adV85bwDL7WmDV01eJvMX67fIMcyO
UI4WojJ3vVDYn/twARoouw7/nzQ/9ckZarqHsK9HskR2zGyf8j0hq+T/Cg4nA+Oy
1wP9t2JEDUX4KQ1tPZuslq4y8iFQFlUXn2CLaSzyal1sL0MxuxjGnogzIs3PYA3H
voPESXfTrwKBgQC33GB1J6BhFAYjmrW2Gye16DrHEpmGM4Kj1A1xCqUMwRdYOSJ+
ZPSt4v8NVTdyp89hCSC2UUMwQy/m+/9s43qDj0Oh6wEMm6TPd7GaeuLJfpn9KM+7
SXHsl+pYgyB79wR2apA68DyBJiZAsd3LCOkDq2kbo8CRKq0M07HjOHccQwKBgCcu
TlwhRCHWofZ2xUET0vfy1AbUwvMOWpQL0v0kwjX+7VUQ4XZBg0j6T6iKQ1O3gbxq
X+4iX4Gfnemk5MsBlqo1qvdP3cd8g6H4+slRk4M1DeeNU3xldSY2dUjq9BImNC2D
hFpPvnSPLb3PFv9Ih/7oyOCW2/Tz+6jQF5iWchp3AoGBAKNS42idgA4q4H/JVjKH
0LPIK6ve9ajfDB9gviGwRjtsZMiUPKJsjjE8ZDr4M7cNki4Kp97P7T2w10t8sFDZ
aRxuqAd+6GVnMaC8YKw6O9HOMC4P5JGZdjzNG5K71yMWp9/hzI+X3ziBC+o9q9Ki
7GLOr5j9GGFExKgTbdAtyzPQ', passphraseVariable: 'pass', usernameVariable: 'mcpixel')]) {
          sh 'apt-get install -y nodejs'
          sh 'npm install express'
          sh "ssh -i $SSH_PRIVATE_KEY_FILE $SSH_USERNAME@$STAGING_VM 'cd C:\Users\mrcel\Desktop\tools\staging && git pull && node index.js'"
        }
      }
    }

    stage('Deploy to Production') {
      when {
        branch 'main'
      }
      steps {
        withCredentials([sshUserPrivateKey(credentialsId: 'myid', keyFileVariable: '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
eK2UyERqRqo=', passphraseVariable: 'pass', usernameVariable: 'mcpixel2')]) {
          sh 'apt-get install -y nodejs'
          sh 'npm install express'
          sh "ssh -i $SSH_PRIVATE_KEY_FILE $SSH_USERNAME@$PRODUCTION_VM 'cd C:\Users\mrcel\Desktop\tools\production && git pull && node index.js'"
        }
      }
    }
  }

}
