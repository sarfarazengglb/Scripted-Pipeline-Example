node {
    def nodejs = tool name: 'NodeJS', type: 'Tool'
    env.PATH = "${nodejs}/bin:${env.PATH}"
    stage('Clean') {
        cleanWs()
    }
    stage('Checkout') {
        git branch: 'main', url: 'https://github.com/sarfarazengglb/Scripted-Pipeline-Example.git'
    }

    stage('Build') {
        // Use the appropriate shell based on the operating system
        if (isUnix()) {
            sh 'npm install'
            sh 'npm run build'
        } else {
            bat 'npm install'
            bat 'npm run build'
        }
    }

    stage('Test') {
        // Use the appropriate shell based on the operating system
        if (isUnix()) {
            sh 'npm run test'
        } else {
            bat 'npm run test'
        }
    }

    stage('Archive') {
        archiveArtifacts artifacts: 'build/**'
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
