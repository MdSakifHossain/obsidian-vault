# Things to do after a Fresh VSCode Install

⬅️ [VSCode](VSCode.md)

## Install Extentions

> Just install it and don't select any options provided by the Extention.
> Leave the default settings as it was..

- [Aura Spirit Dracula Theme](https://marketplace.visualstudio.com/items?itemName=JoseMurilloc.aura-spirit-dracula)
- [Custom UI Style](https://marketplace.visualstudio.com/items?itemName=subframe7536.custom-ui-style)
- [Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme)
- [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

## Open settings.json

`Ctrl + Shift + P` and type: `Open User Settings Json`. Clear the file and Paste this json and you're good to go.

```json
{
  "workbench.colorTheme": "Aura Dracula Spirit (Soft)", // its value will be changed automatically when you change theme color using the command palette

  "workbench.sideBar.location": "right", // the location of the sidebar
  "workbench.activityBar.location": "hidden", // wether sidebar will be visible or not

  "workbench.editor.showTabs": "multiple", // multiple tabs are good but sometimes singular is more good looking

  "workbench.statusBar.visible": false, // very bottom Status Bar which is pretty much annoying TBH

  "workbench.tips.enabled": false, // the welcome screens keyboard tips
  "workbench.startupEditor": "none", // if there is at least one tab was opened before closing the VSCode then that one will appear else nothing will appear. else, nothing will be showed but just the VSCode icon. Usually the default option were to show a welcome screen.

  "editor.minimap.enabled": false, // the annoying minimap which is set to false so thats why it needs to be hidden

  "breadcrumbs.enabled": true, // the default breadcrumbs which visible but can be hidden

  "workbench.iconTheme": "material-icon-theme", // the icons extention which is currently used
  "material-icon-theme.hidesExplorerArrows": true, // the arrows which indicate wether the folder is open or closed. these 2 are combined together.

  "workbench.tree.enableStickyScroll": false, // by default its true and this only shows on the sidebar explorer where it gets sticky. now it wont get any sticky. it will just go normally
  "workbench.tree.renderIndentGuides": "none", // its the long line which shows how big the folder is spread. by default its usually "always" and its pretty much annoying to look at when i dont need the indentation guide.
  "workbench.tree.indent": 16, // its the indentation of the files and folders and by default its very little. i guess the default value is 8.

  "explorer.compactFolders": false, // if there is only one folder or one file under a filder then it jsut shows it as if `folder/filename.extention`. which is annoying and i just removed that.

  "git.decorations.enabled": true, // this one is for when you do a single change and git just screams with some highlights and the big filled circle and the A, U, M and other indication which is just by defautl value and i just thought why not just remove it and see how it looks

  "window.zoomLevel": 3,
  "window.titleBarStyle": "custom", // "custom" is defult and it should be the default.

  "custom-ui-style.stylesheet": {
    ".notification-toast": "box-shadow: none !important",
    ".quick-input-widget.show-file-icons": "box-shadow: none !important",
    ".quick-input-widget": "top: 25vh !important",
    ".quick-input-list .scrollbar": "display: none",
    ".monaco-action-bar.quick-input-inline-action-bar": "display: none",
    ".editor-widget.find-widget": "box-shadow: none; border-radius: 4px",
    ".monaco-scrollable-element > .shadow.top": "display: none",
    ".sidebar > div.composite.title.has-actions": "padding: 0 8px !important",
    ".sidebar": "border: none !important",
    ".monaco-list-row.focused": "outline: none !important",
    ".mocaco-editor .scroll-decoration": "display: none",
    ".title-actions": "display: none !important",
    ".monaco-scrollable-element > div.split-view-container > div > div > div.title.show-file-icons > div.label-container > div": "justify-content: center",
    ".monaco-scrollable-element > div.split-view-container > div > div > div.title": "padding-left: 40px",
    ".monaco-scrollable-element > div.split-view-container > div:nth-child(1) > div > div.pane-body > div > div > div": "padding-left: 14px"
  },
  "custom-ui-style.font.sansSerif": "Dank Mono", // this setting is responsible to change the font family of the exploreres files, folder and some other things

  // text cursor/carets styling
  "editor.cursorStyle": "block", // "line" is default. "block" is good. "underline" is not good. "DONT TRY UNDERLINE".
  "editor.cursorBlinking": "smooth", // "smooth" is good. Dont try others.
  "editor.cursorSmoothCaretAnimation": "on", // "on" is good. dont try others.
  "workbench.colorCustomizations": {
    "editorCursor.background": "#ffffff" // this is for the cursor. when the cursor is already on a letter, then the texts color will be changes accordingly.
  },

  "editor.fontFamily": "'Dank Mono', 'JetBrains Mono', monospace",
  "editor.fontSize": 16,
  "editor.fontLigatures": true, // =>, -->, === && all other symbols which morphs into other looking thing.

  "editor.codeLens": false, // dont know what this is. but dont touch until you are fully sure
  "editor.lightbulb.enabled": "off", // that stupid light bulb, sometimes it shows up while coding.

  "files.trimTrailingWhitespace": true, // this is a plug and play and never need to touch it after the setup completion
  "files.insertFinalNewline": true, // plug and play and never have to touch it again in life.

  "editor.renderLineHighlight": "none", // this is a time to time changable thing, this is the line highlight feature which just took the whole fucking line to be highlighted.

  "editor.scrollbar.horizontal": "hidden", // the x axis scrollbar of the editor
  "editor.scrollbar.vertical": "hidden", // the y axis scrollbar of the editor
  "editor.overviewRulerBorder": false, // false is better, dont change. y axis scrollbar has an annoying border which looks like a stupid shadow.

  "extensions.ignoreRecommendations": false, // When set to true, this setting stops VS Code from prompting you to install recommended extensions, though the `Show Recommended Extensions` command remains available if you wish to view them manually. It does not, however, hide the Recommended section in the Extensions view sidebar;
  "editor.formatOnSave": true, // plug and play and never to touch this sacred setting

  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
}
```
