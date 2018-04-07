# ASP.NET Core

* [MVC 5 or Core?](https://www.linkedin.com/pulse/mvc-5-aspnet-core-now-jani-hyyti%C3%A4inen/)
* [Differences between ASP.NET Core and ASP.NET MVC 5](http://www.mithunvp.com/difference-between-asp-net-mvc6-asp-net-mvc5/)
* [Choose between ASP.NET and ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/choose-aspnet-framework)
* [ASP.NET MVC to ASP.NET Core MVC Migration](https://docs.microsoft.com/en-us/aspnet/core/migration/mvc)
* [ASP.NET MVC Wikipedia Page](https://en.wikipedia.org/wiki/ASP.NET_MVC)
* [ASP.NET MVC 5 Udemy Course](https://www.udemy.com/the-complete-aspnet-mvc-5-course/learn/v4/content)

## Entry Points

### Routing

### ActionResult types

### Applying Action Selectors

### Using Filters

## Views

### Razor Syntax

Can be used to embed C# logic within a View, but try not to overuse it as MVC should involve seperation of concerns.

The C# can either be embeded inline: `Here's the message: @ViewBag.Message`, or in a block:

```C#
@{
    // Multiline
    // C#
    // Code
}
```

ASP.NET can deal with the use of `@` in emails, but will have issues with, for example, Twitter accounts: `@twitter` will cause issues but this can be dealt with by using a double `@` like so: `@@twitter`.

Convenience methods can also be created and called within Razor pages, a method can be created like so:

```C#
@helper formatAmount(decimal amount) {
    var color = "green";
    if (amount < 0)
    {
        color = "red";
    }
    <span style="color:@color">@String.Format("{0:c}", amount)</span>
}
```

And then used with a set of amounts:

`@{var amounts = new List<Decimal>{100, 25,50m, -40, 275.99m};}`

And then loop through and format them using the method:

```C#
<ul>
@foreach(decimal amount in amounts)
{
    <li>@formatAmount(amount)</li>
}
</ul>
```

The placement of the method doesn't appear to matter (can come first of last).

Razor comment syntax:

```C#
@*
@{var amounts = new List<Decimal>{100, 25,50m, -40, 275.99m};}

<ul>
@foreach(decimal amount in amounts)
{
    <li>@formatAmount(amount)</li>
}
</ul>

@helper formatAmount(decimal amount) {
    var color = "green";
    if (amount < 0)
    {
        color = "red";
    }
    <span style="color:@color">@String.Format("{0:c}", amount)</span>
}
*@
```

Embedded plaintext within a C# Razor block can be done using a `<text>plain text</text>` tag or `@:plain text`

### Layouts

Layouts that have common elements like the header and footer are put in the `Views/Shared/_Layout.cshtml` and the layout file is specified in the `Views/_ViewStart.cshtml` folder, a ViewStart file can also be added to specific View folders, e.g. `View/Home/_ViewStart.cshtml` to specify layout files only applicable to those Views.

### HTML Helpers

* `@Html.ActionLink("Link text", "Action Name", "Controller")` - help method for creating an anchor tag
* e.g. `@Html.ActionLink("Register", "Register", "Account", null, new {@class="btn btn-default"})`
* `@Html.Partial("_LoginPartial")` - renders a given partial view, e.g. `"_LoginPartial"`
* `using(@Html.BeginForm("LogOff", "Account", FormMethod.Post, new {id = "logoutForm", @class = "navbar-right"})){ // form stuff }` this will setup a form related to the logoff method and add an end form tag because of the `using` keyword.
* `@Html.Action()`

### Bundling and Minification

Release and Debug modes automatically switch between using the minified and normal versions of jQuery, Bootstrap, etc. This can be managed in the Web.config tag `<system.web><compilation debug="true" targetFramework="4.5.1" /></system.web>`. You can also set the bundle.config to use a CDN. Enabling optimisations will use minified scripts.