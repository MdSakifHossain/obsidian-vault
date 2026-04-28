# Core idea

## Code

```sh
#!/bin/bash

# Script name
echo "Script: $(basename "$0")"

# Prompt for number of days with default
read -p "How many days? [default: 3]: " num_days_input
num_days=${num_days_input:-3}

# Prompt for number of notes with default
read -p "How many notes per day? [default: 10]: " num_notes_input
num_notes=${num_notes_input:-10}

# Create the main file
touch Core.md

# Loop to create days and notes
for day in $(seq 1 $num_days); do
    mkdir -p "day-$day/notes"
    touch "day-$day/day-$day.md"

    for note in $(seq 1 $num_notes); do
        filename="day-$day/notes/note-$note.md"
        echo "# day $day note $note" > "$filename"
        echo "Created: $filename"
    done
done
```

## Output

```
❯ tree --gitignore --dirsfirst
.
├── day-1
│   ├── notes
│   │   ├── note-10.md
│   │   ├── note-1.md
│   │   ├── note-2.md
│   │   ├── note-3.md
│   │   ├── note-4.md
│   │   ├── note-5.md
│   │   ├── note-6.md
│   │   ├── note-7.md
│   │   ├── note-8.md
│   │   └── note-9.md
│   └── day-1.md
├── day-2
│   ├── notes
│   │   ├── note-10.md
│   │   ├── note-1.md
│   │   ├── note-2.md
│   │   ├── note-3.md
│   │   ├── note-4.md
│   │   ├── note-5.md
│   │   ├── note-6.md
│   │   ├── note-7.md
│   │   ├── note-8.md
│   │   └── note-9.md
│   └── day-2.md
├── day-3
│   ├── notes
│   │   ├── note-10.md
│   │   ├── note-1.md
│   │   ├── note-2.md
│   │   ├── note-3.md
│   │   ├── note-4.md
│   │   ├── note-5.md
│   │   ├── note-6.md
│   │   ├── note-7.md
│   │   ├── note-8.md
│   │   └── note-9.md
│   └── day-3.md
└── Core.md

7 directories, 34 files
```
