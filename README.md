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



agent any {
---
- name: Install and Start Nginx
  hosts: web
  become: true  # Run tasks as sudo

  tasks:
    - name: Install Nginx (Debian)
      apt:
        name: nginx
        state: present
      when: ansible_os_family == "Debian"

    - name: Install Nginx (RedHat)
      yum:
        name: nginx
        state: present
      when: ansible_os_family == "RedHat"

    - name: Start and Enable Nginx
      service:
        name: nginx
        state: started
        enabled: true


}


