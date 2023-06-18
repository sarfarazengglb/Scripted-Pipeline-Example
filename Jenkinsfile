pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/sarfarazengglb/Scripted-Pipeline-Example.git'
            }
        }

        stage('Clean') {
            steps {
                cleanWs()
            }
        }

        stage('Build') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'npm install'
                        sh 'npm run build'
                    } else {
                        bat 'npm install'
                        bat 'npm run build'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'npm run test'
                    } else {
                        bat 'npm run test'
                    }
                }
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'build/**'
            }
        }

        stage('Fingerprint') {
            steps {
                fingerprint files: 'build/**'
            }
        }
    }

    post {
        always {
            // Perform any cleanup or finalization steps here
        }

        success {
            // Actions to take when the pipeline succeeds
            echo 'Pipeline succeeded!'
        }

        failure {
            // Actions to take when the pipeline fails
            echo 'Pipeline failed!'
        }
    }
}

def isUnix() {
    return isUnixAgent() || isUnixShell()
}

def isUnixAgent() {
    return isUnix() && (agent.platform == 'unix' || agent.label == null)
}

def isUnixShell() {
    return isUnix() && (isSh() || isBash() || isGitBash())
}

def isSh() {
    return isShell('sh')
}

def isBash() {
    return isShell('bash')
}

def isGitBash() {
    return isShell('bash.exe') || isShell('gitbash.exe')
}

def isShell(shellName) {
    return env.PATH?.toLowerCase()?.contains(shellName)
}
