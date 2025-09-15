🐧 Linux Command Cheatsheet
📂 File and Directory Management
📦 Package Management
Install a Package
sudo apt install <package_name>
Installs software packages in Ubuntu with administrator rights.
sudo: Super User do, grants administrative/root permissions.
apt: Advanced Package Tool, manages software from official repositories.
Example:
sudo apt install firefox
Remove a Package
sudo apt remove <package_name>
Removes a package.
📁 Navigation and Listing
List Files and Directories
ls
Lists all files and directories in the current location.
ls -l: Detailed listing (permissions, owner, date, size).
ls -a: Shows hidden files (starting with .).
Change Directory
cd
cd ~: Navigates to the home directory.
cd <directory_name>: Enters a specific directory.
cd ..: Moves up one level to the parent directory.
Print Working Directory
pwd
Prints the current working directory.
📝 File and Directory Operations
Copy Files/Directories
cp <source> <destination>
Copies a file or directory.
Example:
cp sourcefile.txt ~/destinationfolder/
Move or Rename Files/Directories
mv <source> <destination>
To move: mv sourcefile.txt destinationfolder/
To rename: mv oldfile.txt newfile.txt
Remove Files/Directories
rm <filename>
Deletes a file.
rm -r <foldername>: Recursively deletes a folder (⚠️ use with caution).
📖 File Content
View File (paged):

less <filename>
Press q to exit.

Show First Lines:

head <filename>
head -n 5 <filename>
Show Last Lines:

tail <filename>
tail -n 10 <filename>
tail -c 200 <filename>
⚙️ System Information and Processes
System Info
free -h   # Memory usage  
df -h     # Disk space  
top       # Real-time processes  
Process Management
ps        # Current shell processes
ps -e     # All processes
ps aux | grep <process_name>   # Filter process
kill <pid>       # Terminate process by PID
kill -9 <pid>    # Force kill
uptime           # System uptime
uptime -p        # Human-readable uptime
🌐 Networking
netstat -tulnp   # Show network connections
ifconfig         # Show network interfaces
ping <host>      # Check connectivity
netstat flags:
-t: TCP
-u: UDP
-l: Listening ports
-n: Numeric addresses
-p: Program name and PID
🔐 Permissions and Ownership
Change Permissions
chmod <mode> <file>
Audience: u (user), g (group), o (others), a (all).
Operators: + (add), - (remove), = (set exactly).
Numeric: r=4, w=2, x=1
Examples:

chmod 644 file.txt   # rw- r-- r--
chmod 755 script.sh  # rwx r-x r-x
Change Ownership
sudo chown <user> <file>
sudo chown <user>:<group> <file>
sudo chown -R <user>:<group> <dir/>
Default Permissions (umask)
umask 022
Results in 644 for files (666 - 022).
👤 User Management and Utilities
whoami   # Current user
id       # User and group IDs
who      # Logged-in users
🔍 Find Files
find <directory> -name "<filename.txt>"
find . -iname "<filename.txt>"   # Case-insensitive
find . -type f                   # All files
find / -size +100M               # Files larger than 100MB
🔑 Remote Access
ssh <username>@<remote_ip_address>    # Connect to remote
ssh-keygen -t ed25519                 # Generate SSH key
ssh-copy-id <user@server_ip>          # Copy key for passwordless login
⬇️ Downloading Files
wget <url>   # Download file
curl <url>   # Transfer data

