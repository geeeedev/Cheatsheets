# Purpose: Reminder myself how to get started with a C# project.

C# commands:

- `dotnet —-version` - Display .NET Core SDK version in use (eg. 2.2.107)
- `dotnet --info` - Display .NET Core information
- `dotnet --list-runtimes` - Display the installed runtimes
- `dotnet --list-sdks` - Display the installed SDKs
- `dotnet new` - show key options, boiler plates code / scaffold
- `dotnet build` - build/compile program once, no running
- `dotnet run` - build/compile and run program once, no auto update per modification
- `dotnet watch run` - constantly restarting/resetting server when changes are detected, auto reloading happens like Django
- `dotnet bin/debug/netcoreapp2.2/CSProjectName.dll` - run through debug .dll directly - which is the already compiled code.  
   If you just edited your code, it will not be in this .dll version until after you “build” again

> To run my C# project, first open C# project folder in VSCode

> Dotnet watch run is the most helpful in our development!


## Installations & Dependencies

- C# .Net Core 2.2 Installation

  Download SDK Installer from [MS repositories](https://github.com/dotnet/core/blob/master/release-notes/2.2/2.2.5/2.2.5-download.md)

- C# OmniSharp (VSCode extension) Installation

  The one trick with the C# OmniSharp extension is that its tools will only work correctly when you open your C# project's folder into a new window of VS Code! If you open a container directory and then try to work on files from a subproject within it, IntelliSense, Debugging, and other benefits will not appear.

  Debugging is another tool that requires the folder you're working in to be the top-level folder you have open in VS Code, just like IntelliSense.

  > When you open your project in VS Code you should see a prompt drop down from the top of the editor offering to create files necessary for debugging; Accept, and you'll see the .vscode folder appear.

  > Do not copy the .vscode folder from previous projects! It contains references to the specific project it was generated for and will not work with others! Take a moment to browse through the launch.json file inside and you'll notice it has several different configurations listed.



* packages/dependencies by project

  ```CSharp
  dotnet add package ...
  dotnet add package Pomelo.EntityFrameworkCore.MySql -v 2.2.0    //example: adding EF package as dependency
  ```

* after adding/removing packages, must run:

  ```CSharp
  dotnet restore
  ```

  > This command initiates a script that reads the .csproj file and triggers NuGet to download the appropriate packages. Acutely run for initial creation of a project

* Password Hashing (similiar to bcrypt)

  from ASP.Net Core's built-in encryption tool, part of MS's Identity suite

    ```CSharp
    using Microsoft.AspNetCore.Identity;
    ...
    ...
    
    // Initializing a PasswordHasher object, providing our User class as its type
    PasswordHasher<User> Hasher = new PasswordHasher<User>();
    user.Password = Hasher.HashPassword(user, user.Password);
    ```

* nuGet - Pkg Mgr for .Net
  - Pkg mgr for .Net = nuGet
  - Pkg mgr for PY = pip
  - Pkg mgr for JS = npm (node pkg mgr for Node.js framework)

## Create C# Project

- Scaffold (frame) a console app
  ```CSharp
  dotnet new console -o newProjName //dotnet new console app, output to newProjName folder
  ```

- Scaffold a new ASP.NET Web app
  ```CSharp
  dotnet new web --no-https -o newProjName
  cd newProjName
  code .
  ```

- Scaffold a new ASP.NET MVC Web app
  ```CSharp
  dotnet new mvc --no-https -o newProjName
  cd newProjName
  code .
  dotnet run //==> localhost:5000
  ````

  ```CSharp
  //Configure/add middleware @ Startup.cs for MVC Web app

  public void ConfigureServices(IServiceCollection services)
  {
      services.AddMvc();      //add middleware
  }

  public void Configure(IApplicationBuilder app, IHostingEnvironment env)
  {
      ...
      app.UseMvc();           //add this middleware as last item, replacing the app.run lines of code
  }
  ````

- Scaffold a MVC Web app with EFCore

  - same as MVC Web app, plus adding MySQL package and more configurations
    <small>See [CheatSheet-C#EntityFrmwkCoreSetup.md](CheatSheet-C#EntityFrmwkCoreSetup.md) for complete setup</small>

  * Context — db
  * DbSet — table (convention plural)
  * Model — Entity (convention single)

## Execute C# Project

- run

  ```CSharp
  dotnet run                      //build/compile and run program once, no auto update per modification
  dotnet run --"arg1" "arg2"      //if arguments exist
  ```

  ```CSharp
  dotnet watch run                //constantly restarting/resetting server when changes are detected
  ```

  ```CSharp
  dotnet build                    //build/compile program once, no running
  dotnet bin/debug/netcoreapp2.2/CSProjectName.dll    //run through debug .dll directly - which is the already compiled code.
                                                      //new changes do not reflect in this .dll version until after you “build” again
  ```

- stop - `cltr-C`

## Migration

- Model Creation

  ```CSharp
  dotnet build                                            //make sure no errors before generating migration
  dotnet ef migrations add ProvideAMigrationNameHere      //this step takes a long while until "Done" response - be patient
  dotnet ef database update                               //this step takes a long while until "Done" response - be patient
  ```

- Model Modification/Corruption

  - Drop ALL tables in MySQL (just tables, not database, for a clean start)
  - Delete all migrations (scripts) in Migrations folder
  - Re-generate a new migration
    > Note: This will wipe out existing data - only do this during development

    <img src="Screenshots/CsDropTable1-Roles.png" width="20%"/> 
    <img src="Screenshots/CsDropTable2-Users.png" width="20%"/> 
    <img src="Screenshots/CsDropTable3-MigrationsHistoryAlso.png" width="20%"/> 
    <img src="Screenshots/CsDeleteMigrationsFolder.png" width="20%"/>

    
    <!-- ![](./ScreenshotsCs/CsDropTable1-Roles.png)
  
    ![](./ScreenshotsCs/CsDropTable2-Users.png)
  
    ![](./ScreenshotsCs/CsDropTable3-MigrationsHistoryAlso.png)
  
    ![](./ScreenshotsCs/CsDeleteMigrationsFolder.png) 
    -->
