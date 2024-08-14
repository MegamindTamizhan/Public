```
@echo off
setlocal

:: Define the log file path in the %TEMP% directory
set "LOGFILE=%TEMP%\permissions_log.txt"

:: Start the log
echo Script started at %date% %time% > "%LOGFILE%"

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
    if exist "%%~F" (
        echo Setting permissions for "%%~F"... >> "%LOGFILE%"
        icacls "%%~F" /inheritance:r >> "%LOGFILE%" 2>&1
        icacls "%%~F" /grant "%USERNAME%:(RX)" >> "%LOGFILE%" 2>&1
        icacls "%%~F" /deny "%USERNAME%:(W)" >> "%LOGFILE%" 2>&1

        if errorlevel 1 (
            echo Error: Failed to set permissions for %%F at %date% %time% >> "%LOGFILE%"
            exit /b 1
        )
    ) else (
        echo Warning: Folder "%%~F" does not exist. Skipping... >> "%LOGFILE%"
    )
)

echo Script completed successfully at %date% %time% >> "%LOGFILE%"

endlocal
exit /b 0
```
``
