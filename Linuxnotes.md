sential Linux Commands — Cheat Sheet

*Derived and organized from your uploaded notes.* fileciteturn0file0

---

## Table of Contents
1. [Package Management (apt)](#package-management-apt)  
2. [Listing & Navigation (ls, cd, pwd)](#listing--navigation)  
3. [File Operations (cp, mv, rm)](#file-operations)  
4. [Viewing Files (less, head, tail)](#viewing-files)  
5. [Permissions & Ownership (chmod, chown, umask)](#permissions--ownership)  
6. [Process Management (ps, top, kill, uptime)](#process-management)  
7. [Disk & Memory (df, du, free)](#disk--memory)  
8. [Networking (ifconfig, netstat, ping, ssh, wget, curl)](#networking)  
9. [Finding Files (find)](#finding-files)  
10. [Quick Tips & Examples](#quick-tips--examples)  
11. [Cheat-sheet Table](#cheat-sheet-table)

---

## Package Management (apt)

```bash
# Install a package (needs admin)
sudo apt install <package_name>

# Remove a package
sudo apt remove <package_name>
```

Notes:
- `sudo` gives administrator/root permissions.
- `apt` (Advanced Package Tool) manages packages from repositories.
- Examples:
  - `sudo apt install firefox`
    - `sudo apt install git`
      - `sudo apt install python3`

      ---

      ## Listing & Navigation

      ```bash
      ls            # list files and folders
      ls -l         # detailed list (permissions, owner, size, date)
      ls -a         # include hidden files

      pwd           # print working directory
      cd ~          # go to home directory
      cd <folder>   # enter a directory
      cd ..         # move up one directory
      ```

      ---

      ## File Operations

      ```bash
      # Copy
      cp sourcefile.txt destination.txt
      cp sourcefile.txt ~/destinationfolder/

      # Move (or rename)
      mv sourcefile.txt destinationfolder/
      mv oldfile.txt newfile.txt

      # Remove
      rm filename.txt
      rm -r foldername   # recursive delete (be careful!)
      ```

      Tip: ensure you're **not inside** a directory you intend to delete with `rm -r`.

      ---

      ## Viewing Files

      ```bash
      less filename.txt         # view file one page at a time

      head filename.txt         # show first 10 lines
      head -n 5 filename.txt    # show first 5 lines

      tail filename.txt         # show last 10 lines
      tail -n 10 filename.txt   # last 10 lines
      tail -c 200 filename.txt  # last 200 characters
      ```

      ---

      ## Permissions & Ownership

      Linux permissions are shown by `ls -l`, e.g.:
      ```
      -rw-rw-r-- 1 mythra mythra 876 Sep 10 14:33 nationalA.txt
      ```

      Audiences: **owner**, **group**, **others**  
      Operators: `+` add, `-` remove, `=` set exactly

      Permissions numeric values: `r=4`, `w=2`, `x=1`

      Examples:
      ```bash
      chmod 644 file.txt   # rw- r-- r--  (owner read/write; group/others read)
      chmod 755 script.sh  # rwx r-x r-x  (owner rwx; group/others read+execute)
      chmod 700 secret/    # rwx --- ---  (only owner access)

      # Change ownership
      sudo chown user file
      sudo chown user:group file
      sudo chown :group file
      sudo chown -R user:group dir/
      ```

      ### umask
      `umask` subtracts permissions from default file creation permissions.
      - Example: `umask 022` means default file perms become `644` (owner read/write, others read).

      ---

      ## Process Management

      ```bash
      ps            # processes in current shell
      ps -e         # all processes
      ps -ef        # detailed (UNIX style)
      ps aux        # detailed (BSD style)
      ps aux | grep <process>

      top           # real-time resource usage

      # Kill processes
      sudo kill <pid>
      sudo kill -9 <pid>   # force kill
      ps -p <pid>          # check process status
      ```

      ### uptime
      ```bash
      uptime         # system running time, current time, users, load
      uptime -p      # pretty human-readable uptime
      uptime -s      # show boot time
      ```

      ---

      ## Disk & Memory

      ```bash
      df -h          # disk usage in human-readable form
      du -h          # directory/file space usage
      du -sh dir/    # size of folder only

      free -h        # memory usage in human-readable form
      ```

      ---

      ## Networking

      ```bash
      ifconfig                     # show network interfaces (may need net-tools)
      netstat                      # network connections
      netstat -tulnp               # TCP/UDP listening ports with program + PID

      ping <host>                  # check reachability and latency

      # SSH (secure remote login)
      ssh user@remote_ip

      # Generate SSH key
      ssh-keygen -t ed25519 -C "your_email@example.com"
      cat ~/.ssh/id_ed25519.pub
      ssh-copy-id user@server_ip

      # Downloading
      wget https://example.com/file.zip
      curl https://example.com/   # fetch data from web / APIs
      ```

      ---

      ## Finding Files (`find`)

      ```bash
      find /home/mythra -name "filename.txt"     # find by name
      find foldername -iname "filename.txt"      # case-insensitive
      find . -type f                             # all files in current dir tree
      find . -type d                             # all directories
      find / -size +100M                         # files larger than 100M (+ means more)
      find . -name "*.c" | wc -l                 # count .c files
      ```

      ---

      ## Quick Tips & Examples

      - Prefer `ls -lh` for readable sizes.
      - Use `tail -f logfile` to follow logs in real time.
      - When editing dotfiles (like `.vimrc`), watch for swap files (`.swp`) that indicate another instance of the file is open.
      - To copy your SSH public key to a server: `ssh-copy-id user@server_ip` then `ssh user@server_ip` for passwordless login.
      - Use `ps aux | grep <name>` to locate process IDs before killing.

      ---

      ## Cheat-sheet Table

      | Task | Command | Notes |
      |---|---:|---|
      | Install package | `sudo apt install <pkg>` | Use apt on Debian/Ubuntu |
      | Remove package | `sudo apt remove <pkg>` | |
      | List files | `ls -la` | show hidden and details |
      | Current dir | `pwd` | print working directory |
      | Copy file | `cp src dst` | |
      | Move / Rename | `mv src dst` | |
      | Delete file | `rm file` | |
      | Recursive delete | `rm -r dir` | dangerous if used wrongly |
      | View file | `less file` | pager |
      | Show first lines | `head file` | |
      | Show last lines | `tail file` | |
      | Show processes | `ps aux` | |
      | Real-time processes | `top` | |
      | Disk usage | `df -h` | |
      | Directory size | `du -sh dir` | |
      | Memory | `free -h` | |
      | Network interfaces | `ifconfig` | may require `sudo apt install net-tools` |
      | Networking ports | `netstat -tulnp` | may require `sudo` |
      | Ping | `ping host` | |
      | SSH | `ssh user@host` | |
      | Download | `wget URL` / `curl URL` | |

      ---

      ## Footer
      This markdown was generated from your uploaded `linux commands.txt`. For the original raw notes, see your uploaded file. fileciteturn0file0
      
