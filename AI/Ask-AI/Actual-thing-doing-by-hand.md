# Steps

go to the directory:

```sh
cd Documents
```

Create core Document:

```sh
touch Core.md
```

Create Directories:

```sh
for i in {1..10}; do mkdir "day-$i"; done
```

Output:

```sh
tree --gitignore --dirsfirst
.
├── day-1
├── day-10
├── day-2
├── day-3
├── day-4
├── day-5
├── day-6
├── day-7
├── day-8
├── day-9
└── Core.md

11 directories, 1 file
```

Create the file for the directory:

```sh
❯ for i in {1..10}; do touch "day-$i/day-$i.md"; done
❯ tree --gitignore --dirsfirst
.
├── day-1
│   └── day-1.md
├── day-10
│   └── day-10.md
├── day-2
│   └── day-2.md
├── day-3
│   └── day-3.md
├── day-4
│   └── day-4.md
├── day-5
│   └── day-5.md
├── day-6
│   └── day-6.md
├── day-7
│   └── day-7.md
├── day-8
│   └── day-8.md
├── day-9
│   └── day-9.md
└── Core.md

11 directories, 11 files

```

create the `notes` sub-directory inside the `directoryes`:

```sh
❯ for i in {1..10}; do mkdir "day-$i/notes"; done
❯ tree --gitignore --dirsfirst
.
├── day-1
│   ├── notes
│   └── day-1.md
├── day-10
│   ├── notes
│   └── day-10.md
├── day-2
│   ├── notes
│   └── day-2.md
├── day-3
│   ├── notes
│   └── day-3.md
├── day-4
│   ├── notes
│   └── day-4.md
├── day-5
│   ├── notes
│   └── day-5.md
├── day-6
│   ├── notes
│   └── day-6.md
├── day-7
│   ├── notes
│   └── day-7.md
├── day-8
│   ├── notes
│   └── day-8.md
├── day-9
│   ├── notes
│   └── day-9.md
└── Core.md

21 directories, 11 files
```
