## Purpose: Remind myself of the retrieval and re-installation of the VSCode extensions  

&nbsp;  

- List the installed extensions in Terminal
```bash
code --list-extensions
```

- Export the list of installed extensions to a text file
```bash
code --list-extensions >> vs_code_extensions_list.txt
```

- Transfer the text file list to the machine where the extensions need to be reinstalled.
- In the same directory of the list, run Terminal and execute below code
- This step should go through each extension in the file and install them (Not yet tried to see it work)
```bash
cat vs_code_extensions_list.txt | xargs -n 1 code --install-extension
```

- Remove all extensions
- Do this *after* you have exported the extensions list, just in case
- Do this if you want a clean reinstall
```bash
code --list-extensions | xargs -n 1 code --uninstall-extension
```

> Location for VSCode extensions: ~/.vscode/extensions  
> Location for VSCode user settings: $HOME/Library/ApplicationSupport/Code/User/settings.json  
> Location for VSCode snippets: ~/Library/ApplicationSupport/Code/User/snippets/  



- List of my VSCode Extensions as of Apr 2021:  
```
CoenraadS.bracket-pair-colorizer
esbenp.prettier-vscode
Gforcedev.ctrl-semicolon
ms-azuretools.vscode-docker
ms-dotnettools.csharp
ms-python.python
ms-toolsai.jupyter
oderwat.indent-rainbow
ritwickdey.LiveServer
techer.open-in-browser
tombonnike.vscode-status-bar-format-toggle
```  
  

- List of existing VSCode User setting from settings.json
```json
{
  "breadcrumbs.enabled": true,
  "window.zoomLevel": -1,
  "liveServer.settings.donotShowInfoMsg": true,
  "editor.snippetSuggestions": "top",
  "editor.tabCompletion": "on",
  "emmet.includeLanguages": {
    "javascript": "javascriptreact",
    "razor": "html",
    "aspnetcorerazor": "html"
  },
  // "files.associations":{
    //     "*.cshtml":"html"
    // },
    "extensions.ignoreRecommendations": true,
    "liveshare.presence": false,
    "[javascript]": {
      "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
  "files.autoSave": "afterDelay",
  "formattingToggle.affects": ["formatOnSave"],
  "editor.formatOnSave": true,
  "editor.formatOnPaste": false,
  "editor.formatOnType": false,
  "editor.minimap.enabled": false,
  "diffEditor.ignoreTrimWhitespace": false,
  "javascript.updateImportsOnFileMove.enabled": "always",
  "workbench.editor.wrapTabs": true,
  "workbench.editor.decorations.colors": true,
  "workbench.editor.decorations.badges": true,
  "workbench.editorAssociations": [
    {
      "viewType": "jupyter.notebook.ipynb",
      "filenamePattern": "*.ipynb"
    }
  ],
  "git.ignoreRebaseWarning": true
}
```