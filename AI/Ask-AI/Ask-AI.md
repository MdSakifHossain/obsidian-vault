# Objective

create me a good and professional looking shell script based on the design doc.

## Flow

### Gathering Information

it will ask me for the directory where it will operate in. Default:  `/home/<current_username>/Documents`
then it will remove all the files and folder in that folder.
then it will ask me the name of the Core file. Default: `Core` (user will just write the name of the file without the extention. its the scripts job to add the extention of the file which is `.md`)

then it will create the core file
then it will ask me about the file name? Default: `test` $test_file_name
then it will ask me about how many files? Default: 10 $files_to_created

### The Actual Job

then it will add `# core-file-name` inside of the first line of the core file.
then it will add an empty line
then it will add `## Links to the $test files`
then another empty line on the core file.

then it will loop for $files_to_created times and then it will echo the links using the unordered list format.

**Example**:

```md
# core-file-name

## Links

- [$test_file_name](./$test_file_name/$test_file_name.md)
- [$test_file_name](./$test_file_name/$test_file_name.md)
- [$test_file_name](./$test_file_name/$test_file_name.md)
...
- [$test_file_name](./$test_file_name/$test_file_name.md)
```




```sh
folder_name=$test_file_name-$looping_number # example: test-1, test-2
```
