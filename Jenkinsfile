pipeline {
    agent any

    tools {
        maven 'Maven3'
        jdk 'Java17'
    }

    environment {
        JENKINS_HOME = "E:\\Jenkins"
    }

    stages {

        stage('Preparar ambiente') {
            steps {
                echo 'Configurando ambiente seguro para Git...'
                // %cd% é a variável 'current directory' do Windows
                bat 'git config --global --add safe.directory "%cd%"'
            }
        }

        stage('Clonar repositório') {
            steps {
                echo 'Baixando projeto do GitHub...'
                git branch: 'master', url: 'https://github.com/lucaspaiolog/projeto-jenkins-java.git'
            }
        }

        stage('Compilar, Testar e Empacotar') {
            steps {
                echo 'Iniciando build, testes e empacotamento com Maven...'
                bat 'mvn clean package'
            }
        }


        stage('Executar aplicação') {
            steps {
                echo 'Rodando aplicação Java...'
                bat 'java -jar target\\projeto-jenkins-java-0.0.1-SNAPSHOT.jar || echo Arquivo .jar não encontrado'
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

