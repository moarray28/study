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



pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/yourusername/jenkins-java-demo.git'
            }
        }

        stage('Compile Java') {
            steps {
                sh 'mkdir -p out'
                sh 'javac -d out Main.java'
            }
        }

        stage('Run Java App') {
            steps {
                sh 'java -cp out Main'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'out/*.class', fingerprint: true
            }
        }
    }
}


##########################################################################


give similar for java file,pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/yourusername/jenkins-cicd-demo.git'
            }
        }

        stage('Run Python Script') {
            steps {
                sh 'python3 hello.py'
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh 'python3 -m unittest test_hello.py || echo "Tests failed but continuing"'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: '*.py', fingerprint: true
            }
        }
    }
}



 Check uptime
ansible localhost -m shell -a "uptime" --connection=local

List files in /tmp
ansible localhost -m command -a "ls /tmp" --connection=local

 Create directory
ansible localhost -m file -a "path=/tmp/test_ansible state=directory mode=0755" --connection=local

 Install a package (like curl)
ansible localhost -m apt -a "name=curl state=present update_cache=true" --connection=local -b

 Check disk usage
ansible localhost -m shell -a "df -h" --connection=local

