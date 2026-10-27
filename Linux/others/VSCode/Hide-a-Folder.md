# Hide a Certain Folder in VSCode

⬅️ [VSCode](VSCode.md)

Well I have done it in a single project (Folder) in VSCode.

## Problem

We have to understand the scenario first. I was trying to make a VitePress Website. Well, technically i still am.

```shell
tree -a -L 1 --dirsfirst
.
├── .git
├── .vitepress
├── node_modules
├── src
├── .gitignore
├── package.json
├── package-lock.json
└── README.md

5 directories, 4 files
```

> This folder was bothering me in VSCode on a spiritual level.

Before losing my _Sanity_, i asked internet and got a solution.

## Solution

I maybe asked Leo and it said:

Create a `.vscode` folder at the `root of your folder/project` and inside that folder Create a file called `settings.json`.

Inside that `settings.json` file **Add these lines**.

```json
{
  // [!code ++]
  "files.exclude": {
    // [!code ++]
    "**/node_modules": true // [!code ++]
  } // [!code ++]
} // [!code ++]
```

And then `Save the file`. Instantly the `node_modules` folder will be hidden.

Then, also i wanted to make the `.vscode` folder to be hidden. so i also added an extra line onto the `settings.json` file. 😅

```json
{
  "files.exclude": {
    "**/node_modules": true,
    "**/.vscode": true // [!code ++]
  }
}
```

Then save it and close the `settings.json` file and close the tab of `settings.json` files. And, Boom. desired Folders got vanished. 💪
