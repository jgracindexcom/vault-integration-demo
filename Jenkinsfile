pipeline {
    options { buildDiscarder(logRotator(numToKeepStr: '10')) }

    agent {
        kubernetes {
            yaml """
apiVersion: v1
kind: Pod
metadata:
spec:
  containers:
  - name: busybox
    image: busybox:latest
    command:
    - cat
    tty: true
"""
        }
    }

    environment {
        DEMO_SECRET = vault path: 'secrets/test/fortesting', key: 'abc'
    }

    stages {
        stage('Build') {
            steps {
                container('busybox') {
                    echo "${DEMO_SECRET}"
                }
            }
        }
    }
}
