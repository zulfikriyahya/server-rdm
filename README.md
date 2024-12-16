```bash
@REM install mariadb 11 manual

@echo off
title RDM INSTALLER By: MTs Negeri 1 Pandeglang
mode con: cols=70 lines=5
color a

@REM install git
if not exist "C:\Program Files\Git\git-bash.exe" (
    winget install --id Git.Git -e --source winget --silent
exit
)

@REM mengunduh source code server-rdm
cd \
if not exist "C:\server-rdm" (
    git clone https://github.com/zulfikriyahya/server-rdm.git
)

@REM menyembunyikan folder server-rdm
attrib +h "C:\server-rdm"

@REM menjalankan apache server
cd /server-rdm/apache24/bin
httpd -k stop
httpd -k uninstall
httpd -k install
httpd -k start
start http://localhost

@REM menginisiasi environtment variabel mariadb (optional)
setx PATH "%PATH%;C:\Program Files\MariaDB 11.6\bin"

@REM membuat autorun program rdm
if not exist "%USERPROFILE%\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\rdm.cmd" (
    echo @echo off >> "%USERPROFILE%\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\rdm.cmd"
    echo title RDM INSTALLER By: MTs Negeri 1 Pandeglang >> "%USERPROFILE%\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\rdm.cmd"
    echo mode con: cols=70 lines=5 >> "%USERPROFILE%\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\rdm.cmd"
    echo cd \server-rdm >> "%USERPROFILE%\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\rdm.cmd"
    echo start http://localhost/rdm >> "%USERPROFILE%\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\rdm.cmd"
    echo exit >> "%USERPROFILE%\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\rdm.cmd"
    )

    echo Penyiapan aplikasi selesai. Silakan simpan pekerjaan anda, komputer akan restart dalam waktu 1 menit.
    
    @REM restart komputer
    shutdown -r -t 60

    @REM menghapus file installer
    del rdm.cmd
```
