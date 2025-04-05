pipeline {
    agent any

    environment {
        DOTNET_CLI_HOME = "C:\\Program Files\\dotnet"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    // Restoring dependencies
                    //bat "cd ${DOTNET_CLI_HOME} && dotnet restore"
                    bat "dotnet restore"

                    // Building the application
                    bat "dotnet build --configuration Release"
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Running tests
                    bat "dotnet test --no-restore --configuration Release"
                }
            }
        }

        stage('Publish') {
            steps {
                script {
                    // Publishing the application
                    //bat "dotnet publish --no-restore --configuration Release --output .\\publish"
                    
                    // Publishing the application to a local folder (you can change this if needed)
                    bat "dotnet publish --no-restore --configuration Release --output .\\publish"
                    
                    // Copy the published files to the desired directory (C:\inetpub\wwwroot\JenkinsDemo)
                    bat "xcopy /E /I /Y .\\publish\\* C:\\inetpub\\wwwroot\\JenkinsDemo\\"
                }
            }
        }
    }

    post {
        success {
            echo 'Build, test, and publish successful!'
        }
    }
}
