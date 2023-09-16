node('any') {
   
    stage('Clean') {
        cleanWs()
    }
   stage('Checkout') {
        git branch: 'main', url: 'https://github.com/sarfarazengglb/Scripted-Pipeline-Example.git'
    }

    stage('Build') {
        bat 'npm install'
        bat 'npm run build'
    }

    stage('Test') {
        bat 'npm run test'
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
