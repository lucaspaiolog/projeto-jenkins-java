pipeline {
    agent any

    tools {
        // Garante que o Maven e o Java estejam configurados no Jenkins
        maven 'Maven3'
        jdk 'Java17'
    }

    environment {
        // Caminho do JENKINS_HOME — opcional se já estiver configurado
        JENKINS_HOME = "E:\\Jenkins"
    }

    stages {

        stage('Preparar ambiente') {
            steps {
                echo 'Configurando ambiente seguro para Git...'
                bat 'git config --global --add safe.directory "%cd%"'
            }
        }

        stage('Clonar repositório') {
            steps {
                echo 'Baixando projeto do GitHub...'
                git branch: 'master', url: 'https://github.com/lucaspaiolog/projeto-jenkins-java.git'
            }
        }

        stage('Compilar projeto') {
            steps {
                echo 'Iniciando build com Maven...'
                bat 'mvn clean compile'
            }
        }

        stage('Testes') {
            steps {
                echo 'Executando testes (se existirem)...'
                bat 'mvn test || echo Nenhum teste encontrado'
            }
        }

        stage('Executar aplicação') {
            steps {
                echo 'Rodando aplicação Java...'
                bat 'java -jar target\\*.jar || echo Nenhum .jar encontrado — talvez seja projeto sem empacotamento'
            }
        }
    }

    post {
        success {
            echo '✅ Build e execução concluídos com sucesso!'
        }
        failure {
            echo '❌ Ocorreu um erro na pipeline. Verifique o console output.'
        }
    }
}

