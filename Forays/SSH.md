I had added a new ssh key for github so I wouldn't have to log in every time I pushed to origin while working on my Ubuntu WSL - forgetting that I already had a ssh key (the one that I used in windows). Everything was fine until I switched back to windows and tried to push something, and got an error warning about possible man-in-the-middle attacks, because the key for github.com and the one in my known_hosts were different.

I opened known_hosts and found four keys, all identical but to slightly different IPs. I added the IPs to the first entry and deleted the later keys. Same error. At this point I read the error again and saw the line "the github.com key has changed", so I looked up how to get the current github.com key:
```ssh-keyscan -t rsa [server_ip]```
and copied the line into the file below the first line and it worked.

In the future, all I'd have to do is copy the entry from my windows /.ssh/known_hosts to my WSL one, instead of generating a new key (I suspect that `ssh-keygen` automatically adds it to that file).

### `known_hosts`:
This file lets the client authenticate the server, to check that it isn't connecting to an impersonator. It contains a list of SSH server host public keys. Each entry starts with a comma-separated list of server names and/or IP addresses which are associated with the key, followed by the type of key, and then the public key (encoded to stay with ASCII range). Then, optionally a comment.