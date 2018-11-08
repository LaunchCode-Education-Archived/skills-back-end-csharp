---
title: 'Studio: Bonjour, ASP.NET!'
currentMenu: studios
---

In the [prep work](../../class-prep/3/) for this class, you create a basic Hello, World application using ASP.NET MVC. Open that project up in Visual Studio, and get ready to add some features!

Modify your `HelloController` class to display a form on `GET` request that asks the user for both their name and the language they would like to greeted in. It should look something like this:

![Greeting Form](form.png)

The resulting form submission should return and display the message, "Bonjour Chris".

Note that the language is presented in a dropdown, more formally known as a `select` element. If the syntax of selects is fuzzy, [quickly brush up here](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select) and [here](https://www.w3schools.com/tags/att_option_selected.asp).

When the user submits the form (a `POST` request), they should be greeted in the selected language. Your new feature should:
- Include at least 5 languages, with English being the default. If you don't speak 5 languages yourself, ask your friend [the Internet](http://pocketcultures.com/2008/10/30/say-hello-in-20-languages/).
- Include a new (`public static`) method, `CreateMessage`, in `HelloController` that takes a name string as well as a language string. Based on the language string, you'll return the proper welcome message to be displayed.

## Bonus Missions

- Instead of returning the greeting as plain text, add a bit of HTML to the response string so that the displayed message looks a bit nicer.
- Add some additional output that displays the number of times the user has been greeted. *Hint:* Use a `static` property to keep track of the count.
- The bonus mission above doesn't discriminate between requests made by you or somebody else. In other words, it counts *total* greetings rather than greetings to a specific user. Fix this by using cookies. When a user is greeted for the first time, set a cookie that has the visit count 1. On subsequent visits, check for this cookie and update its value.

    Since cookies are stored within the browser, this will tie the visit count to a specific user an a specific browser. If the same user were to go to another browser, their counter would start over at 1.

    Here are a few tips to get you going:
    - Every controller inherits the properties `Request` and `Response`, so these can be used directly in your controller code. They contain data and methods related to the current HTTP request and response being handled.
    - `Request.Cookies` is a collection with key/value data that can be used like a dictionary. The keys are the cookie names, and the values are the cookie values. If a cookie doesn't exist, then trying to access its value will give `null`. Use this fact to check for the existence of a cookie, and to set it initially on the first request.
    - The values in `Request.Cookies` are always strings, so you'll likely need to do some type conversion.
    - To set a cookie in the response, use `Response.Cookies.Append(name, value)`, where `name` and `value` are strings.
    - Don't forget to display the visit count on the screen! Or, at least check that it has been set and incremented using your browser's developer tools.
