
## Plot
Let's assume we have /home/user/myWebsite/ directory that includes the source code of your beautiful website. If you want to upload to your server, you have to use either `scp` or `rsync`. (See FAQ for why we use `rsync`)

```
# rsync [args] [source] [destination]
# so let's upload our source code to server
rsync /home/user/myWebsite user@server:/var/www

# Sometimes you make change on the server and want to update to your source code.
# so download it ...
rsync user@server:/var/www /home/user/myWebsite

# now whenever you change the code, you have to run update on the server again.
rsync /home/user/myWebsite user@server:/var/www

# See! we just switch source and destination
# the hard part is you have to remember your username, domain name or IP address of the server and the path ...
# So do you consider setting *alias* in bash ?


# notice that source and destination only depend on the action
# also if you use *alias*, how do you figure out when you have multiple projects ?
# not efficient, not portable, not scaleable

# so let's make a memo (text file) in the project directory
# local=/home/user/myWebsite
# remote=user@server:/var/www
# now it is easy to say
# download='rsync remote local'
# upload='rsync local remote'

# Here I use Makefile, where it allow me to set variable and directly call the function aka rules
# See Makefile

# But Makefile is primarily used for compiling or building.
# All my rules are nothing to do with compiling.
# Sometimes I put Makefile at Python project and the purpose is absolutely misleading.

# Here sfs born ...

```
