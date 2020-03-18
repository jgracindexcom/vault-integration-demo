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

    stages {
        stage('Build') {
            steps {
                container('busybox') {
                    script {
                        // define the secrets and the env variables
                        // engine version can be defined on secret, job, folder or global.
                        // the default is engine version 2 unless otherwise specified globally.
                        def secrets = [
                            [path: 'secret/test', engineVersion: 2, secretValues: [
                                [vaultKey: 'abc']]]
                        ]
                        // inside this block your credentials will be available as env variables
                        withVault([vaultSecrets: secrets]) {
                            echo "T: $abc"
                        }

                    }
                }
            }
        }
    }
}
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

    stages {
        stage('Build') {
            steps {
                container('busybox') {
                    script {
                        // define the secrets and the env variables
                        // engine version can be defined on secret, job, folder or global.
                        // the default is engine version 2 unless otherwise specified globally.
                        def secrets = [
                            [path: 'secret/test/fortesting', engineVersion: 2, secretValues: [
                                [vaultKey: 'abc']]]
                        ]
                        // inside this block your credentials will be available as env variables
                        withVault([vaultSecrets: secrets]) {
                            echo "T: $abc"
                        }
                    }
                }
            }
        }
    }
}
