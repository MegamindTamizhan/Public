# Public


@echo off
setlocal

:: Define log file path
set "LOGFILE=C:\temp\script.log"

:: Start logging
echo Script started at %date% %time% >> "%LOGFILE%"

:: Set user-specific paths
set "USERNAME=%USERNAME%"
set "DESKTOPFOLDER=C:\Users\%USERNAME%\Desktop"
set "DOCUMENTSFOLDER=C:\Users\%USERNAME%\Documents"
set "MUSICFOLDER=C:\Users\%USERNAME%\Music"
set "PICTURESFOLDER=C:\Users\%USERNAME%\Pictures"
set "VIDEOSFOLDER=C:\Users\%USERNAME%\Videos"
set "THREEDFOLDER=C:\Users\%USERNAME%\3D Objects"
set "SAVEDGAMESFOLDER=C:\Users\%USERNAME%\Saved Games"
set "SEARCHESFOLDER=C:\Users\%USERNAME%\Searches"
set "LINKSFOLDER=C:\Users\%USERNAME%\Links"
set "FAVORITESFOLDER=C:\Users\%USERNAME%\Favorites"
set "CONTACTSFOLDER=C:\Users\%USERNAME%\Contacts"
set "DOWNLOADSFOLDER=C:\Users\%USERNAME%\Downloads"

:: Set appropriate permissions for each folder
for %%F in ("%DESKTOPFOLDER%" "%DOCUMENTSFOLDER%" "%MUSICFOLDER%" "%PICTURESFOLDER%" "%VIDEOSFOLDER%" "%THREEDFOLDER%" "%SAVEDGAMESFOLDER%" "%SEARCHESFOLDER%" "%LINKSFOLDER%" "%FAVORITESFOLDER%" "%CONTACTSFOLDER%" "%DOWNLOADSFOLDER%") do (
    icacls "%%~F" /inheritance:r >> "%LOGFILE%" 2>&1
    if errorlevel 1 (
        echo Error: Failed to disable inheritance for %%F at %date% %time% >> "%LOGFILE%"
        exit /b 1
    )

    icacls "%%~F" /grant "%USERNAME%:(RX)" >> "%LOGFILE%" 2>&1
    if errorlevel 1 (
        echo Error: Failed to grant permissions for %%F at %date% %time% >> "%LOGFILE%"
        exit /b 1
    )

    icacls "%%~F" /deny "%USERNAME%:(W)" >> "%LOGFILE%" 2>&1
    if errorlevel 1 (
        echo Error: Failed to deny write permissions for %%F at %date% %time% >> "%LOGFILE%"
        exit /b 1
    )
)

:: Example command - change directory to C:\temp
cd C:\temp >> "%LOGFILE%" 2>&1
if errorlevel 1 (
    echo Error changing directory to C:\temp at %date% %time% >> "%LOGFILE%"
    exit /b %errorlevel%
)

:: Example command - create a new file
echo Hello World > testfile.txt
if errorlevel 1 (
    echo Error creating testfile.txt at %date% %time% >> "%LOGFILE%"
    exit /b %errorlevel%
)

:: Log completion
echo Script completed successfully at %date% %time% >> "%LOGFILE%"
exit /b 0
