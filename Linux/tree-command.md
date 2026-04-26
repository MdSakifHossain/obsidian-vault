# Tailored Tree Command Guide

## Basic Tree

Display the directory structure from your current location.

```bash
tree
```

## Basic Tree to File

Display the directory structure from your current location and save it to a text file in the same directory.

```bash
tree > tree-output.txt
```

## Tree from Parent Directory

Go to the parent directory, list the specified folder, and save the output. This avoids creating a new file in the `vault` folder, which could trigger your daemon.

```bash
cd .. && tree vault > output.txt
```

## HTML Tree Output

Generate a formatted HTML file with clickable links for the `vault` directory.

```bash
tree ./vault -H ./vault -o vault_tree.html
```

The command `tree ./vault -H ./vault -o vault_tree.html` generates a self-contained HTML file with a clickable directory tree.

- **`-H ./vault`**: This flag enables **HTML output**. The `./vault` argument specifies the "base HREF" (hypertext reference). This tells the generated HTML how to create hyperlinks for the files and directories, making them clickable. You provide the path twice because the first `./vault` tells `tree` _what directory to list_, and the second `./vault` tells it _how to label the root of the HTML page_.

- **`-o vault_tree.html`**: This redirects the output to a file named `vault_tree.html` instead of printing it to the terminal.
