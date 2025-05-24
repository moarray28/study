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
