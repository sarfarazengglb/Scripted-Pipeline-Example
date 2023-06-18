node {
    stage('Checkout') {
        git branch: 'main', url: 'https://github.com/sarfarazengglb/Scripted-Pipeline-Example.git'
    }
    
    stage('Clean') {
        cleanWs()
    }
    
    stage('Build') {
        if (isUnix()) {
            sh 'npm install'
            sh 'npm run build'
        } else {
            bat 'npm install'
            bat 'npm run build'
        }
    }
    
    stage('Test') {
        if (isUnix()) {
            sh 'npm run test'
        } else {
            bat 'npm run test'
        }
    }
    
    stage('Archive') {
        archiveArtifacts artifacts: 'build/**'
    }
    
    stage('Fingerprint') {
        fingerprint files: 'build/**'
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

def isUnix() {
    return isUnixAgent() || isUnixShell()
}

def isUnixAgent() {
    return agent.platform == 'unix' || agent.label == null
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
