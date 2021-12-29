# **docker pwnenv**

**pwnenv** is a series of docker containers that I made, which allow you to run and debug _linux binaries_ with the desired libc.

## Changelog

1. Switched out the 3 containers for 1
2. Updated vimrc and zshrc
3. Removed non privilaged user (everything happens with the root user)

This was built to run on docker with _WSL 2_ on Windows systems.

This started as a fork of [pwndocker by skysider](https://github.com/skysider/pwndocker)

### **Features**:
- zsh / tmux
- Custom **pwntools** templates for **x86**, **x86-64**, **arm**
- **gdb** with **gef**, **pwndbg**, **peda** ([Article from Andreas Pogiatzis](https://medium.com/bugbountywriteup/pwndbg-gef-peda-one-for-all-and-all-for-one-714d71bf36b8))
- one_gadget
- seccomp-tools
- reutils
- ropper
- ROPGadget
- main_arena_offset
- heap_inspect
- and many more
---
## Building the containers

```powershell
docker build -t <container-name> .
```
---

## Usage Info

### Windows (Powershell)

I set this up so the containers can be started from anywhere. The run scripts automatically mount the current directory in the container.

> I added the following code to the **$PROFILE** of powershell, so it creates this function (`pwnenv`) when I open a new PS window.

```powershell
$pwnenv = "<path-to-the-run-folder>"
function pwnenv ($arguments) {
    & $pwnenv/run.ps1 $arguments
}
```

Now just restart powershell, go to the woking directory and type `pwnenv`

### Linux

For linux the alias is much simpler just add an alias in the `.bashrc` or respective alias file.


```bash
alias pwnenv='docker run --net=host --cap-add=SYS_PTRACE --security-opt seccomp=unconfined -it --rm --name pwnenv -v `pwd`:/root/data pwnenv'
```
