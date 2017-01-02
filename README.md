
# Simple File Synchronization
For simple, efficient and elegant method for file synchronization

This project is a proof of concept to my another project _**S**ync **F**ile**S**ystem_

## Features
- Sync Files between hosts
- Only transfer incremental changes
- Follow VCS ignored files rules such as `.gitignore` via **IGNORE_FILE** (See #Todo, #Bug)
- Support **KEY_FILE** for specific `ssh` tunnel

## Usage

Assume you want to sync current folder with `/var/www` at `example.com` with `ubuntu` username
```
sfs init ubuntu@example.com /var/www
```
To sync from local path to remote path
```
sfs push
```
To sync from remote path to local path
```
sfs pull
```
To go directly to remote location, which is `ssh` and `cd` to the associated path
```
sfs ssh
```
To see information about current path configuration
```
sfs info
```

## Background

As a software developer, I occasionally have to modify the code, push to test servers and run the code on them. Most of the time the old code exists on the server and I just have to overwrite old one with the new changes. It is not a one-time process, every time someone changes the source code, I have to do the process again. Transferring the whole repo is not efficient because it consumes time, bandwidth and so on. I found that `rsync` the incremental file transfer method is beneficial in this case. Thus, I sometimes include `rsync` command in the Makefile. See historical Makefile and continue reading `/history/plot.md`

## FAQ

- Why not `scp`?  
`rsync` transmits only differences of changed files, thus it saves a lot of time and resources. Also here somebody did [benchmark](http://www.digitalsanctuary.com/tech-blog/debian/rsync-is-much-faster-than-scp.html).


- Why `sfs` ?  
Why not, unless you want to
```bash
git commit -am 'your commit message'
git push origin master
ssh $REMOTE_HOST
cd $REMOTE_PATH
git pull
```

## Todo
- Check file exists for `KEY_FILE`, `IGNORE_FILE` and etc.
- Solve `rsync exclude-from` -- `IGNORE_FILE` format may differ(See #Bug)
- Add installation feature
- RC file reading security issue -- avoid use `source`
- Better RC file -- with user manual
- `autosync` when files change -- Auto monitoring file system and trigger to push
- Allow multiple hosts
- Test ... Test ... Test ... !

## Bug
- `rsync exclude-from` has different format compared to VCS ignored file like `.gitignore`
