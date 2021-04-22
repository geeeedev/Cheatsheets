## Purpose: Remind myself of retrieval and re-installation of the VSCode extensions  

&nbsp;  

- List the installed extensions in Terminal
```bash
code --list-extensions
```

- Export the list of installed extensions to a text file
```bash
code --list-extensions >> vs_code_extensions_list.txt
```

- Transfer the new list to the new machine where the extensions need to be installed.
- In the same directory of the list, run in Terminal
- This step should go through each extension in the file and install them (Not yet tried to see it work)
```bash
cat vs_code_extensions_list.txt | xargs -n 1 code --install-extension
```

-