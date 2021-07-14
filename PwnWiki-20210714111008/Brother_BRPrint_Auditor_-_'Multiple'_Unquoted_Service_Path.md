    # Exploit Title: Brother BRPrint Auditor 3.0.7 - 'Multiple' Unquoted Service Path
    # Discovery by: Brian Rodriguez
    # Date: 14-06-2021
    # Vendor Homepage: https://support.brother.com/
    # Software Links: https://support.brother.com/g/b/downloadhowto.aspx?c=us&lang=en&prod=dcp7060d_all&os=10013&dlid=dlf102753_000&flang=4&type3=214
    # Tested Version: 3.0.7
    # Vulnerability Type: Unquoted Service Path
    # Tested on: Windows 10 Enterprise

    # Step to discover Unquoted Service Path:

    C:\>wmic service get name,displayname,pathname,startmode |findstr /i "auto"
    |findstr /i /v "c:\windows\\" |findstr /i /v """
    BrPrAuSvc     BrAuSvc      C:\Program Files
    (x86)\Brother\BRPrintAuditor\Brsvau3a.exe       Auto

    Brother BRPrintAuditor Agent     BRPA_Agent   C:\Program Files
    (x86)\Brother\BRPrintAuditor\BRAgtSrv.exe    Auto

    C:\Users\IEUser>sc qc BrAuSvc
    [SC] QueryServiceConfig CORRECTO

    NOMBRE_SERVICIO: BrAuSvc
            TIPO               : 10  WIN32_OWN_PROCESS
            TIPO_INICIO        : 2   AUTO_START
            CONTROL_ERROR      : 1   NORMAL
            NOMBRE_RUTA_BINARIO: C:\Program Files
    (x86)\Brother\BRPrintAuditor\Brsvau3a.exe
            GRUPO_ORDEN_CARGA  : BrotherSplGroup
            ETIQUETA           : 0
            NOMBRE_MOSTRAR     : BrPrAuSvc
            DEPENDENCIAS       : Spooler
            NOMBRE_INICIO_SERVICIO: LocalSystem

    C:\Users\IEUser>sc qc BRPA_Agent
    [SC] QueryServiceConfig CORRECTO

    NOMBRE_SERVICIO: BRPA_Agent
            TIPO               : 10  WIN32_OWN_PROCESS
            TIPO_INICIO        : 2   AUTO_START
            CONTROL_ERROR      : 1   NORMAL
            NOMBRE_RUTA_BINARIO: C:\Program Files
    (x86)\Brother\BRPrintAuditor\BRAgtSrv.exe
            GRUPO_ORDEN_CARGA  :
            ETIQUETA           : 0
            NOMBRE_MOSTRAR     : Brother BRPrintAuditor Agent
            DEPENDENCIAS       :
            NOMBRE_INICIO_SERVICIO: LocalSystem