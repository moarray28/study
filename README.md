@echo off
echo Starting deployment...

:: Define paths
set SOURCE=%WORKSPACE%
set DEST=C:\inetpub\wwwroot\ci-html

:: Clean old files
if exist "%DEST%" rmdir /S /Q "%DEST%"
mkdir "%DEST%"

:: Copy new files
xcopy /E /Y "%SOURCE%\*" "%DEST%\"

echo Deployment completed to %DEST%









###########################################





 pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/moarray28/study.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Running build stage'
                bat 'echo Hello World'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing complete'
            }
        }
    }
}



######################################




pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/moarray28/study.git'
            }
        }

        stage('Deploy to IIS') {
            steps {
                bat '''
                    @echo off
                    echo Starting deployment...

                    :: Define paths
                    set SOURCE=%WORKSPACE%
                    set DEST=C:\\inetpub\\wwwroot\\ci-html

                    :: Clean old files
                    if exist "%DEST%" rmdir /S /Q "%DEST%"
                    mkdir "%DEST%"

                    :: Copy new files
                    xcopy /E /Y "%SOURCE%\\*" "%DEST%"

                    echo Deployment completed to %DEST%
                '''
            }
        }
    }
}


###############################################################

