# Bash Gists

### Finding files

Find all git repos in home directory

    $ find ~/ -name '.git' -exec echo {} \;

Recursively remove .DS_Store files

    $ find . -name '*.DS_Store' -type f -delete

Remove any log files that are more than a week old

    $ find /path/to/logs/ -type f -name '*.log' -mtime +7 -exec rm -f '{}' \;
    # or compress them
    $ find /path/to/logs/ -type f -name '*.log' -mtime +7 -exec gzip -q '{}' \;

### Searching files (GREP)

Search an entire textfile for a string

    $ grep 'my string' /path/to/file

Regex search for two patterns
    
    $ grep 'this\|that' /path/to/file

Search all files of type in directory

    $ grep 'mystring' *.txt

Search all files in directory and it's subdirectories

    $ grep -R 'mystring' /path/to/directory

Inverse search (return rows NOT containing search)

    $ grep -v 'my string' /path/to/file

Search for text and return the first 2 lines before and 5 lines after a found result

    $ grep -B 2 -A 5 'my string' /path/to/file

#### Search command output from stdout

Filter the results of a directory listing

    $ ls -l | grep foldername
    # options
    -a all (including hidden files)
    -l list
    -h human readable file sizes
    -S sort by size

### Reading log files

Display log file in stdout, continuing to watch for new log data

    $ tail -f /path/to/file.log

Display ERRORS in last 1000 lines and the 10 lines after each error

    $ tail -1000 /path/to/file.log | grep ERROR -A 10

### Copying Files

    cp -avr /path/to/source /path/to/destination
    # options
    -a archive (keeps permissions and ownership)
    -v verbose
    -r recursively copy contents of folders

### Symlinking

Create a symbolic link to another folder.

    $ ln -s /path/to/folder linkname

## Remote Server Management

### SSH

Execute a command remotely

    $ ssh username@remote.com 'ls -l /home/directory/'      #quotes optional

Execute a command on a newline delimited list of servers

    $ for i in `cat /path/to/server_list`; do echo $i && ssh $i ls -l /home/directory/; done

### Copy Files to Remote Server (SCP)

Local to Remote

    $ scp file.txt username@remote.com:/path/to/directory/
    # options
    -r recursive copy

Remote to Local

    $ scp username@remote.com:/path/to/file.txt /path/to/local/file.txt

### Syncronize Folders (RSYNC)

Sync contents of a remote folder into a local folder

    $ rsync -az username@remote.com:/path/to/folder/ /path/to/local/folder/
    # options
    -a                  archive (keep permissions and date changes)
    -z                  compress
    -v                  verbose
    -n (or --dry-run)   dry run
    --delete            delete files
    --progress          track progress
    --size-only         only check filesize, not timestamp

Preview changes for syncinc current folder with remote location deleting files that don't exist locally

    $ rsync -azv . username@remote.com:/path/to/folder/ --delete --dry-run

Make a local backup of a photo library (or other folder)

    rsync -azv /path/to/Photo\ Library/ /path/to/Photo\ Library\ backup/ --progress

When the trailing slash is absent from the source directory, a folder of that name is created inside the destination

    $ rsync -az /path/to/folder /path/to/local/
    # syncs folder /path/to/local/folder/

## Miscellaneous

### Compressing Files

Tar a directory

    $ tar -czvf filename.tar.gz /path/to/directory

Untar a tarball

    $ tar -xzvf file.tar.gz

### Current Running Processes

Current processes with "update"

    $ ps -ef | grep update

Kill process #62111

    $ kill -9 62111

### Run a command as a background process

Appending the ampersand to a command runs that command in the background which frees up your terminal to do other things

    $ long_running_command_or_script &

### OS Version

    $ cat /proc/version

### Disk Usage

Get disk usage of current folder and subfolders

    $ du -ch --max-depth=1 .

Total disk drive utilization

    $ df -h
    # options
    -h human readable filesize

### File permissions

Make file executable

    $ chmod +x /path/to/executable.sh


### Where am I?

    $ pwd

### Switch Current User

    $ su username

### SED

### Generate SSH Keys
