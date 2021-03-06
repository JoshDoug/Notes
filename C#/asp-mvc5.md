# ASP.NET MVC v.5

Notes on version 5 of the ASP.NET MVC Framework.

## Action Results

* Type : Helper Method
* ViewResult - View()
* PartialViewResult - PartialView()
* ContentResult - Content() - to return text (literally just return a string)
* RedirectResult - Redirect() - redirect user to a URL
* RedirectToRouteResult = RedirectToAction() - redirect to action instead of URL
* JsonResult - Json() - return a serialised JSON object
* FileResult - File() - return a file
* HttpNotFoundResult - HttpNotFound() - return a 404 error
* EmptyResult - when an action doesn't need to return any actions, like void

## Routing

### Attribute Routing

Constraints:

* `[Route("movies/released/{year}/{month:regex(\\d{2}):range(1, 12)}")]`
* regex
* range
* min
* max
* minlength
* maxlength
* int
* float
* guid
* and more...

## Views

View Model - a View Model is a model specifically built for a view which includes any data and rules specific to that view.

* View model encapsulates all the data necessary for a View in the event that multiple POCOs/Models are necessary for the View.

### Razor Views

Use `@` to write blocks of code, HTML can be used dynamically (no need to escape the C# like with PHP) within these blocks

### Partial Views

Pretty straightforward.

## Data, Databases, Entity Framework

Using the Entity Framework, an O/RM (Object/Relational Mapper) which maps an object to a tuple in a database.

* `DbContext` - gateway to the database
* LINQ is used to query DB sets

### Database-first vs Code-first

Probably easiest to go code-first, but database-first is more traditional.

* Database-first - involves designing a database and the classes can be generated from the tables
* Code-first - the database is generated from the model classes

Using code-first:

* Enable migrations using the Package Manager Console (Tools > NuGet Package Manager > Package Manager Console)
* Run `enable-migrations` from the console
* After the initial migratoin(?) run `Add-Migration MigrationName` and `Update-Database`