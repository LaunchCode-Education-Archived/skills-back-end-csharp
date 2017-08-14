---
title: "Intro to ASP.NET Core MVC: Routes"
currentMenu: videos
---

<div class="youtube-wrapper"><iframe width="776" height="437" src="https://www.youtube-nocookie.com/embed/ZAGpi88aPhw?rel=0" frameborder="0" allowfullscreen></iframe></div>

## Notes

In this video lesson we focus on routing and specifically:

* Default routing
* Customizing routes with the `[Route("..")]` attribute.
* Declaring HTTP request types with `[HttpGet]` and `[HttpPost]`
* Passing parameters:
  * Get/query parameters
  * Post parameters
  * URL segments
* Redirecting

Be sure to code along with the video! The notes to videos only include highlights of the code that is featured in each video.

### Default Routing

This is the kind of routing behavior we saw in the previous lesson. E.g. "Hello/Index" represents the default structure of "Controller/Action". And the default values for the controller and the action are, respectively, `Home` and `Index`.

### Customizing Routes

We can change the default routing behavior by using the `[Route("..")]` attribute. E.g., we can add this to the top of the `Goodbye` action method in our *HelloMVC* program: `[Route("/Hello/Aloha")]`. Now, in order to see the "Goodbye" message, we have to visit `/Hello/Aloha`.

### Query Parameters

We can add an input parameter to our action methods to enable them to accept query parameters. E.g.:

```nohighlight
public IActionResult Index(string name)
```

If you want to add a default value to the parameter you can do the following:

```nohighlight
public IActionResult Index(string name = "World")
```

### Post Parameters

After adding the string of HTML that will display a form as shown in the video, we can access post parameters in our `Display` method by adding the following lines above that method signature:

```nohighlight
[Route("/Hello/")]
[HttpPost]
```

And add `[HttpGet]` above the `Index` method.

### URL Segments

To achieve the same functionality we had above with query parameters but with a url that looks like this `/Hello/Chris`, we add the following above the appropriate method:

```nohighlight
[Route("/Hello/{name}")]
```

### Redirecting

To redirect a user we can return a `Redirect` object in an action method as follows:

```nohighlight
return Redirect("/Hello/Goodbye");
```

## References

- [Attribute Routing (docs.microsoft.com)](https://docs.microsoft.com/en-us/aspnet/core/mvc/controllers/routing#attribute-routing)
