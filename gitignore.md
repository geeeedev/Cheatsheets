# gitignore examples:
# ignores any file named "secret.txt"
secret.txt
# ignores any directory named "secrets"
secrets/
# ignores a file named "hidden.txt" located at the root of your working directory
/hidden.txt
# ignores a directory called "node_modules" located at the root of your working directory
/node_modules/
# ignores any file with a .png extension
*.png
# ignores any file or directory that begins in "cache", such as cache-file-01, cached_assets/, etc.
cache*
# ignores any file or directory that ends in "data", such as project_data/, big_file_of_data
*data

# .gitattributes - needed to check in this extra file in GitHub for C# projects
# Reclassifies `.cshtml` files as C# instead of HTML for C# Project:
*.cshtml linguist-language=C#


# *** actual file should be named `.gitignore` placed in the root directory of project ***
# .gitignore for ALL projects - continue building up 

# VS Code
.vscode
.vscode/


# PY/Django
.DS_Store
.vscode/
venv/
veDjango/
__pycache__/
db.sqlite3
requirements.txt


# C# .NET Core
.DS_Store
.vscode/
Migrations/
bin/
obj/
#*.png
*.sql
appsettings.json
--ContinuousImprovementNotes.txt
ShowWaitList_FinalVersionShouldUseShowAll.cshtml


# MERN dependencies
/node_modules
/.pnp
.pnp.js
node_modules/

# testing
/coverage

# production
/build

# misc
.DS_Store
.env.local
.env.development.local
.env.test.local
.env.production.local

npm-debug.log*
yarn-debug.log*
yarn-error.log*


# Project Specific - not required now
config/
controllers/
models/
routes/
--ContinuousImprovementNotes.txt
ShowWaitList_FinalVersionShouldUseShowAll.cshtml




