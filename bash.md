## Bash Gists

### Current Running Processes

Current processes with "update"

    $ ps -ef | grep update

### Compressing Files

Tar a directory

Untar a tarball

    $ tar -xzvf file.tar.gz

### Where am I?

    $ pwd

### SED

### Symlinking

    $ ln -s /path/to/folder linkname

### Reading log files

Display log file in stdout, continuing to watch for new log data

    $ tail -f /path/to/file.log

Display ERRORS in last 1000 lines and the 10 lines after each error

    $ tail -1000 /path/to/file.log | grep ERROR -A 10

### Find

Find all git repos in home directory

    $ find ~/ -name '.git' -exec echo {} \;

Recursively remove .DS_Store files

    $ find . -name '*.DS_Store' -type f -delete

Remove any log files that are more than a week old

    $ find /path/to/logs/ -type f -name '*.log' -mtime +7 -exec rm -f '{}' \;
    # or compress them
    $ find /path/to/logs/ -type f -name '*.log' -mtime +7 -exec gzip -q '{}' \;

### SCP

Local to Remote

    $ scp file.txt username@remote.com:/path/to/directory/

Remote to Local

    $ scp username@remote.com:/path/to/file.txt /path/to/local/file.txt

### SSH

Execute a command remotely

    $ ssh username@remote.com 'ls -l /home/directory/'      #quotes optional

Execute a command on a newline delimited list of servers

    $ for i in `cat /path/to/server_list`; do echo $i && ssh $i ls -l /home/directory/ 

### Generate SSH Keys
