# Core Idea

1. user runs the script
2. prompt for directory it will work on. Default: `/home/<current_username>/Documents`
3. prompt for core file name? Default: `Core`
4. prompt for file name? Default: `test`
5. prompt for how many files? Defualt: 10
6. create the core file
7. add `# <core-file-name>` inside the core file
8. add an empty line inside the core file
9. add `---` inside the core file
10. add empty line inside the core file
11. add `## Links` inside the core file
12. add empty line inside the core file
13. loops for the number which i gave after the the file name and add links such as `- [<prompted-file-name>-<currently-looping-number](./<prompted-file-name>-<currently-looping-number>/<prompted-file-name>-<currently-looping-number>.md)` on new line
14. loop ends for the Core file
15. now it will loop again for the number of times it asked 
