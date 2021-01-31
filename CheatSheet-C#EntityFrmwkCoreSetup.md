# Entity Framework (EF) Setup 

> **REMEMBER: C# cshtml is easy; it is the LINQ part, the way it gets to data, that I need to get used to get good at. Review CSSportORM Level3 for the more complicated version**  
>- how to create a ModelView.cs out of your model
>- how to retrieve NULL data in joint set - essentially, doing a L/R JOIN using LINQ
>- drilling in deeper to retrieve data [see here](https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.theninclude?view=efcore-3.1)
>- DefaultIfEmpty(), SelectMany(), Select() - how to use these? [come back to these](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.defaultifempty?view=netcore-3.1)

&nbsp;  

## Create New Project & Install Dependencies

Open terminal:
 ```CSharp
 dotnet new mvc --no-https -o ProjName
 cd ProjName
 dotnet add package Pomelo.EntityFrameworkCore.MySql -v 2.2.0     //this will add an installed package line to your `.csproj` file
 code .
 ```
> [Learn platform version number reference](http://learn.codingdojo.com/m/25/5675/40112)

---

## Set up DB Connections

### 1. Set up Connection String `appsettings.json`
- add "DBInfo" property (don't forget `,` that's needed before/after this new property)
  ```json
  ,
  "DBInfo": {
    "Name": "MySQLConnection",
    "ConnectionString": "server=localhost;userid=root;password=root;port=3306;database=dbName;SslMode=None"
  },
  ```

### 2. Create `DbContext` model
- rename `dbNameContext` to something relevant to your project
- create a new `dbNameContext.cs` file in Models directory
- use your own model name and namespace
  ```csharp
  using Microsoft.EntityFrameworkCore;

  namespace ProjName.Models
  {
    public class dbNameContext : DbContext
    {
      // context constructor using base constructor
      public dbNameContext(DbContextOptions options) : base(options) { }
      // tables in db
      public DbSet<User> Users { get; set; }
    //public DbSet<TableEntityModelSingular> TableNamePlural { get; set; } 
    }
  }
  ```
---

## Setup Configurations

### 3. `Startup.cs` - `ConfigureServices` method
- add the below lines using your own context name instead of `dbNameContext`
- addDbContext to bind appsettings.json `DBInfo` connection sting to the new DB Contet object 
- also add Session and HttpContextAccessor services
  ```csharp
  public void ConfigureServices(IServiceCollection services)
  {
    ...
    services.AddDbContext<dbNameContext>(options => options.UseMySql(Configuration["DBInfo:ConnectionString"]));
    services.AddSession();
    services.AddHttpContextAccessor();
    services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
  }
  ```
- Cookies Policy Removal
  - [delete following lines](http://learn.codingdojo.com/m/25/5671/39759) inside `ConfigureServices(IServiceCollection services)` method 
    ```csharp
    services.Configure<CookiePolicyOptions>(options =>
    {
      // This lambda determines whether user consent for non-essential cookies is needed for a given request.
      options.CheckConsentNeeded = context => true;
      options.MinimumSameSitePolicy = SameSiteMode.None;
    });
    ```

### 4. `Startup.cs` - `Configure` method

- add Session service
- add below lines above `app.UseMvc`
  ```csharp
  public void Configure(IApplicationBuilder app, IHostingEnvironment env)
  {
      ...
    app.UseStaticFiles();
    app.UseSession();
  
    app.UseMvc(routes => 
      ...
    );
  }
  ```

- Cookies Policy Removal
  - delete following lines
    ```csharp
    app.UseHttpsRedirection();
    app.UseCookiePolicy();
    ```
  - also delete `<partial name="_CookieConsentPartial"></partial>` from `_Layout.cs`

---

### 5. Check `Views/_ViewImports.cshtml`
- .Models and TagHelper should be already added by MVC Framework Template

- Optional: access Session from all Views directly
  - this is helpful if you are repeatedly adding the same thing from session into the `ViewBag` for many actions
  - add `services.AddHttpContextAccessor();` in `ConfigureServices` in `Startup.cs`
  - add `@using Microsoft.AspNetCore.Http` in `Views/_ViewImports.cshtml`
     ```csharp
    @using ProjName
    @using ProjName.Models
    @addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
    @using Microsoft.AspNetCore.Http
    ```
  - Access in a view: `<p>@Context.Session.GetString("UserFullName")</p>`

---

### 6. Add Controller Constructor to Receive DbContext

- inside your controller class, at the top
  ```csharp
  public class HomeController : Controller
  {
      private dbNameContext db;
      public HomeController(dbNameContext dbContext)
      {
          db = dbContext;
      }

      public IActionResult Index()
      ...
  ```

---

### 7. Create models in Models directory

- Create DB (Migrate)
  ```CSharp
  dotnet build        //make sure no errors before generating migration 
  dotnet ef migrations add GiveANameToThisMigration
  dotnet ef database update
  ```
  > If db is not yet built in MySQL, run migrations now

  > should see Migrations folder added between Controller and Model folders

  > Check MySQL should see DB showing up

---

### 8. Verify DB & Tables in workbench / mysql Shell

---

### 9. Set up Custom Validations

- add a Validations folder directory parallel to Controllers, Models, and Views folder
- add custom validation class `yourCustomValidation.cs` in Validations directory
- make sure to wrap the custom validation in namespace so models can reference this atop: `using ProjName.Validations;`
  ```csharp
  using System;
  using System.ComponentModel.DataAnnotations;

  namespace ProjName.Validations          
  {
      public class FutureDateOnlyAttribute : ValidationAttribute
      {
          protected override ValidationResult IsValid(object value, ValidationContext validationContext)
          {
              if ((DateTime)value < DateTime.Now)
                  return new ValidationResult("...Date must be in the FUTURE.");
              return ValidationResult.Success;
          }
      }
  }
  ```
- add in model class using validations
  ```csharp
  using System.ComponentModel.DataAnnotations;
  using System.ComponentModel.DataAnnotations.Schema;
  using CSWeddingPlanner.Validations;
  ```

---
---

## Request Response Cycle Review (if you can't explain this effortlessly when asked to, keep re-reading it)

1. the **_client_** makes a **_request_** by visiting a URL
   - a URL is usually visited by the **_client_** clicking on an anchor tag (GET request), typing a URL into the address bar (GET), submitting a form (POST)
2. the **_server_** receives the **_request_** and runs the method (action) that has the matching URL
3. the **_server_** **_responds_** to the request by **_serving_** up an HTML page (rendering), or redirecting to another action method which has it's own URL
4. the request response cycle is complete
   - a redirect triggers an additional request response cycle, the **_response_** is a redirect which triggers a **_request_** for the URL that the client was redirected to

---

## Routing Review

---

### Route Parameters

- read the Request Response Cycle Review
- a route parameter is a placeholder in a URL that is given a name when the route is set up in the controller
  - just like a parameter in a function, it is a placeholder name that will be given a value later on (when function is called / route is visited)
  - the controller method (action) needs a corresponding parameter with a matching name for every parameter in the URL
  - when redirecting to a controller method (action), if that action has parameters, they need to be provided when redirecting

---

### Where are the route parameter placeholders given an actual value

- this happens either in the HTML files or when redirecting in the controller
  - `<a>` tags and `<form>` tags need to have actual parameter values added to them using razor
    - the values are inserted either directly into the `<a>` tag's `href` and the `<form>` tag's `action` attributes or using ASP.NET tag helpers

---

#### Route Parameter Example

  ```html
  <a href="/Quotes/@Model.QuoteId">
    View Quote
  </a>
  ```

- OR

    ```html
    <a
      asp-controller="Quotes"
      asp-action="Details"
      asp-route-quoteId="@Model.QuoteId"
    >
      View Quote
    </a>
    ```

- the above `<a>` tags would create an `href` that looks like this with some id value inserted: `href="/Quotes/5"`
- these URLS would match / connect to a URL pattern in the `QuotesController`

    ```csharp
    // the parameter in the method has to have the same name as the route parameter in the URL
    // and the same name as the asp-route-paramName tag helper if using that
    [HttpGet("Quotes/{quoteId}")]
    public IActionResult Details(int quoteId)
    ```

---

### Routing with a `<form>`

- a form needs a way for the **_client_** to **_request_** it to be displayed (rendered), therefore a URL / route is needed for displaying / rendering the HTML page that has the `<form>` in it
  - GET **_request_** to GET the page that displays the `<form>`
  - there will be a controller method (action) with matching URL to handle the **_request_** that will **_respond_** with `return View()` to display the HTML page with the `<form>` in it
- the form needs a DIFFERENT URL / route to submit to so the submission can be processed, this URL is specified in the `<form>` `action` attribute or the ASP.NET tag helpers on the `<form>` tag
  - the URL / route that the `<form>` submits to (POST **_request_**) needs a corresponding controller method (action) with a matching URL
    - this method (action) will **_respond_** with either a `return RedirectToAction` if successful or a `return View("NameOfView")` if there was a validation error to display the `<form>` again with error messages

---

#### `<form>` routing example

- handle the _request_ for the `<form>` to be displayed

    ```csharp
    [HttpGet("/Quotes/New")]
    public IActionResult New()
    {
      return View();
    }
    ```

- ```html
  <form asp-controller="Quotes" asp-action="Create" method="POST"></form>
  ```

- OR

    ```html
    <form action="/Quotes/Create" method="POST"></form>
    ```

- form submits to the route that matches the `action` attribute or the `asp-controller` and `asp-action`, MAY NEED TO ADD A ROUTE PARAMETER TO THE FORM if the controller method (action) that the `<form>` submits to needs more information

  ```csharp
  [HttpPost("/Quotes/Create")]
  public IActionResult Create(Quote newQuote)
  {
    if (ModelState.IsValid == false)
    {
        // to display validation error messages
        return View("New");
    }

    // no validation errors: save to database then redirect
    // if action redirecting to has parameters, must provide them here as well
    return RedirectToAction("NameOfControllerMethod");
  }
  ```

---

## ViewModel Review

- if you have a view that needs to be sent more than one model, create a new model specifically for that view which contains all of the models it needs as properties
- OR use one of the models as the View Model and put the other(s) into `ViewBag`

---

### Display AND create on same page

- if you have a view whose model (for displaying) is `EntityA`
- and the same view is used to create `EntityB`
- and `EntityB` needs a foreign key (FK) from `EntityA`, e.g., `EntityB.EntityAId`
- you can make the view model: `EntityA`

  - INSIDE the view, write a razor code block to instantiate a new empty `EntityB`
  - assign the foreign key: `newEntityB.EntityAId = Model.EntityAId`
  - pass the `newEntityB` to a partial view that displays the form `<partial name="_partialViewName" model="@newEntityB></partial>`
  - the partial has it's own view model which is `EntityB` used for creating a new `EntityB` when form submitted
  - alternatively, instead of instantiating in the view to add the FK, you can use `ViewBag` to store the FK and put the FK as a route param on the form

---

#### Intantiate in view method

  ```csharp
  @model FoodTruck

  @* HTML displaying the @Model *@

  @{
    Review newReview = new Review();
    newReview.FoodTruckId = Model.FoodTruckId;
  }

  <partial name="_NewReview" model="@newReview"></partial>
  ```

  - the form in the partial view:

    - ```csharp
      @model Review

      <form asp-controller="FoodTrucks" asp-action="ReviewTruck" method="POST">
      ```

      - the action that this form submits to receives a `Review` that already has the food truck FK added to it

---

#### `ViewBag` method instead of instantiating in view

  ```csharp
  @model FoodTruck

  @* HTML displaying the @Model *@

  @{
    Review newReview = new Review();
    newReview.FoodTruckId = Model.FoodTruckId;
  }

  <partial name="_NewReview"></partial>
  ```

  - the form in the partial view:

    - ```csharp
      @model Review

      <form
        asp-controller="FoodTrucks"
        asp-action="ReviewTruck"
        asp-route-foodTruckId="@ViewBag.FoodTruckId"
        method="POST"
      >
      ```

      - the model doesn't need to be passed to the partial view
      - the action that this form submits to receives a `Review` that DOES NOT have the food truck FK added
      - the action has URL / route parameter with the food truck FK in it that will then be added to the `Review` in the controller instead

---

## [Troubleshooting](https://github.com/TheCodingDojo/student_md_docs/blob/master/CA-OC/csharp/troubleshooting.md)

---

## [Relationship Advice](https://github.com/TheCodingDojo/student_md_docs/blob/master/CA-OC/csharp/relationships.md)

---

## Old stuff

- `dotnet add package MySql.Data.EntityFrameworkCore -v 8.0.11`