pipeline {
    agent any
    options { skipDefaultCheckout(true) }
    stages {
        stage('Checkout') { steps { checkout scm } }
        stage('Setup') { steps { bat 'python --version' } }
        stage('Validate Application') { steps { bat 'python scripts/check_app.py' } }

        stage('Packaging Release') { steps { bat 'python scripts/build_release.py' } }

        stage('Archive Release') { steps { archiveArtifacts artifacts: 'dist/*.zip', fingerprint: true } }
        stage('Archive Build Info') { steps { archiveArtifacts artifacts: 'build/*', bat 'echo %BUILD_NUMBER% > build-info.txt' } }
    }
}
