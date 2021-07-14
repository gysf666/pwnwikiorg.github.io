EXP
---

    # Exploit Title: Acer Updater Service 1.2.3500.0 - 'UpdaterService.exe'  Unquoted Service Path
    # Discovery by: Emmanuel Lujan
    # Discovery Date: 2020-11-26
    # Vendor Homepage: https://www.acer.com/ac/en/US/content/home
    # Tested Version: 1.2.3500.0
    # Vulnerability Type: Unquoted Service Path
    # Tested on OS: Windows 7 Home Premium x64

    # Step to discover Unquoted Service Path:

    C:\>wmic service get name, pathname, displayname, startmode | findstr /i "Auto" | findstr /i /v "C:\Windows\\" | findstr /i /v """

    Live Updater Service                                                    Live Upd
    ater Service                          C:\Program Files\Acer\Acer Updater\Updater
    Service.exe                                               Auto

    # Service info:

    C:\>sc qc "Live Updater Service"
    [SC] QueryServiceConfig SUCCESS

    SERVICE_NAME: Live updater Service
            TYPE               : 10  WIN32_OWN_PROCESS
            START_TYPE         : 2   AUTO_START
            ERROR_CONTROL      : 1   NORMAL
            BINARY_PATH_NAME   : C:\Program Files\Acer\Acer Updater\UpdaterService.exe
            LOAD_ORDER_GROUP   :
            TAG                : 0
            DISPLAY_NAME       : Live Updater Service
            DEPENDENCIES       :
            SERVICE_START_NAME : LocalSystem

    #Exploit:

    A successful attempt would require the local user to be able to insert their code in the system root path undetected by the OS or other
     security applications where it could potentially be executed during application startup or reboot. If successful, the local user's
    code would execute with the elevated privileges of the application.