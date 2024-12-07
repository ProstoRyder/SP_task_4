pipeline {
    agent any

    tools {
        msbuild 'MSBuild'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/ProstoRyder/SP_task_4.git', credentialsId: 'testid', branch: 'main'
            }
        }
        
        stage('Build') {
            steps {
                // Крок для збірки проекту з Visual Studio
                // Встановіть правильні шляхи до рішення/проекту та параметри MSBuild
                bat 'msbuild test_repos.sln /t:Build /p:Configuration=Release'
            }
        }

        stage('Test') {
            steps {
                // Команди для запуску тестів
                bat "x64\\Debug\\test_repos.exe --gtest_output=xml:test_report.xml"
            }
        }
    }

    post {
    always {
        // Publish test results using the junit step
         // Specify the path to the XML test result files
         junit 'test_report.xml'
    }
}
}