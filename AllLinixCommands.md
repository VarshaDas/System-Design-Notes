# Essential Linux Skills for Backend Developers

## 1. File System Navigation

**Commands:**
- `ls` - List directory contents
- `cd` - Change directory
- `pwd` - Print working directory
- `mkdir` - Make a new directory
- `rmdir` - Remove an empty directory
- `cp` - Copy files or directories
- `mv` - Move or rename files or directories
- `rm` - Remove files or directories

**Example:**

```bash
# List files and directories
ls

# Change to a directory
cd /path/to/directory

# Print the current directory
pwd

# Create a new directory
mkdir new_directory

# Remove an empty directory
rmdir old_directory

# Copy a file
cp file.txt /path/to/destination/

# Move a file
mv file.txt /path/to/destination/

# Remove a file
rm file.txt


Commands:

cat - Concatenate and display file contents
more - View file contents one screen at a time
less - View file contents with scroll functionality
head - Display the beginning of a file
tail - Display the end of a file
grep - Search for patterns in files
find - Search for files and directories
locate - Find files by name


# Display file contents
cat file.txt

# View file contents page by page
more file.txt

# View file contents with scrolling
less file.txt

# Show the first 10 lines of a file
head file.txt

# Show the last 10 lines of a file
tail file.txt

# Search for a pattern in a file
grep 'pattern' file.txt

# Find files by name
find /path/to/search -name 'filename.txt'

# Locate files by name
locate filename.txt
