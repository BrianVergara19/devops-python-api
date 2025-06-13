pipeline {
    agent any

    stages {
        stage('Clonar repositorio') {
            steps {
                git 'https://github.com/BrianVergara19/devops-python-api.git'
            }
        }

        stage('Instalar dependencias') {
            steps {
                sh 'pip install --upgrade pip'
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Ejecutar tests') {
            steps {
                sh 'pytest tests'
            }
        }

        stage('Construir imagen Docker') {
            steps {
                sh 'docker build -t devops-python-api .'
            }
        }

        stage('Ejecutar imagen local (opcional)') {
            steps {
                sh 'docker run -d -p 8000:8000 devops-python-api'
            }
        }
    }

    post {
        success {
            echo '🎉 Pipeline ejecutado con éxito!'
        }
        failure {
            echo '❌ Algo falló en el pipeline'
        }
    }
}
