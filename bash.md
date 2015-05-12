## Bash Gists

### Finding files

Find all git repos in home directory

    $ find ~/ -name '.git' -exec echo {} \;

Recursively remove .DS_Store files

    $ find . -name '*.DS_Store' -type f -delete

Remove any log files that are more than a week old

    $ find /path/to/logs/ -type f -name '*.log' -mtime +7 -exec rm -f '{}' \;
    # or compress them
    $ find /path/to/logs/ -type f -name '*.log' -mtime +7 -exec gzip -q '{}' \;

### Symlinking

    $ ln -s /path/to/folder linkname

### Reading log files

Display log file in stdout, continuing to watch for new log data

    $ tail -f /path/to/file.log

Display ERRORS in last 1000 lines and the 10 lines after each error

    $ tail -1000 /path/to/file.log | grep ERROR -A 10

### Compressing Files

Tar a directory

Untar a tarball

    $ tar -xzvf file.tar.gz

### Current Running Processes

Current processes with "update"

    $ ps -ef | grep update

Kill process #62111

    $ kill -9 62111


### Where am I?

    $ pwd

### SED


### SCP

Local to Remote

    $ scp file.txt username@remote.com:/path/to/directory/

Remote to Local

    $ scp username@remote.com:/path/to/file.txt /path/to/local/file.txt

### Syncronize Folders (RSYNC)

Contents of remote folder to local folder

    $ rsync -az username@remote.com:/path/to/folder/ /path/to/local/folder/
    # options
    -v                  verbose
    -n (or --dry-run)   dry run
    --delete            delete files

Preview changes for syncinc current folder with remote location deleting files that don't exist locally

    $ rsync -azv . username@remote.com:/path/to/folder/ --delete --dry-run

### SSH

Execute a command remotely

    $ ssh username@remote.com 'ls -l /home/directory/'      #quotes optional

Execute a command on a newline delimited list of servers

    $ for i in `cat /path/to/server_list`; do echo $i && ssh $i ls -l /home/directory/; done

### Generate SSH Keys
