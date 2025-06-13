pipeline {
    agent any

    stages {
        stage('Clonar repositorio') {
            steps {
                git branch: 'main', url: 'https://github.com/BrianVergara19/devops-python-api.git'
            }
        }

        stage('Instalar dependencias') {
            steps {
                bat 'python -m pip install --upgrade pip'
                bat 'pip install -r requirements.txt'
            }
        }

        stage('Ejecutar tests') {
            steps {
                bat 'set PYTHONPATH=%cd% && pytest tests'
            }
        }

        stage('Construir imagen Docker') {
            steps {
                bat 'docker build -t devops-python-api .'
            }
        }

        stage('Ejecutar imagen local (opcional)') {
            steps {
                bat 'docker run -d -p 8000:8000 devops-python-api'
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
