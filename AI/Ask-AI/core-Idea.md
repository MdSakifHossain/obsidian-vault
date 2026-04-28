# Core Idea

user runs the script
prompt for directory it will work on. Default: `/home/<current_username>/Documents`
prompt for core file name? Default: `Core`
prompt for file name? Default: `test`
prompt for how many files? Defualt: 10

deletes everything in the prompted directory
create the core file
add `# <core-file-name>` inside the core file
add an empty line inside the core file
add `---` inside the core file
add empty line inside the core file
add `## Links` inside the core file
add empty line inside the core file

loops for the number which i gave after the the file name and add links such as:
```md
- [<prompted-file-name>-<currently-looping-number>](./<prompted-file-name>-<currently-looping-number>/<prompted-file-name>-<currently-looping-number>.md)
``` 
on new line of the core file.
loop ends for the Core file.

now it will loop again for the number of times it asked in the prompt to create directories which will look like:
```sh
mkdir <prompted-file-name>-<>
```
