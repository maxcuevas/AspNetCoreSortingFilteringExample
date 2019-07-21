# AspNetCoreSortingFilteringExample

This project has the code that I created to accompany this tutorial.
It can be found [here](./AspNetCoreSortingFilterExample) and should be referenced if any issues come up when copying and pasting folders or text.

1. Create a brand new ASP.NET Core Web APP MVC project
    - Make sure the ASP.NET Core sdk version is 2.2, if it is not please install that sdk version
    - There is an sdk version for VS2017 and a different sdk version for VS2019
2. Through the Nuget Manager install the following packages:
    - Microsoft.EntityFrameworkCore (This Entity Framework is specifically for Core applications)
    - NonFactors.Grid.Mvc6 (This version Mvc6 is specifically for Core applications) 
    - I have included all the packages that were downloaded during these two installs in [this repository](./AspNetCoreSortingFilterExample) named **packages.7z**
    - I don't think every single package in that zip is needed if you don't have internet. However, I don't know what packages are included by default with VS installation 
3. I am assuming that you have a database and know how to create classes from that database using EntitiFramework
Core, if you do not please go [here](https://github.com/maxcuevas/DotNetCoreEntityFrameWorkCoreWebApp)
    - Specifically steps 4 - 7
4. Now there should be some classes that were generated for you in the **Models** folder of your ASP.Net Core Web Application
5. I am now assuming that you know how to "scaffold" the views and controller classes from those models. If you do not please go [here](https://github.com/maxcuevas/DotNetCoreEntityFrameWorkCoreWebApp)
    - Specifically steps 8 - 13
6. Now you should be able to hit some http endpoint, website, and see the data from your table(s).

The next steps are needed to get Mvc6 to work in your app. I followed the steps [here](http://mvc6-grid.azurewebsites.net/Home/Installation). They were a bit too implicit so I will be more explicit in the following steps.

1. We should already have Mvc6 Nuget package installed
2. When you install someting through NUGET it caches all of those packages somewhere on your computer. By default
that specific location is something like **"C:\Users\<your username here>\.nuget\packages"**
3. In that directory there should be a folder that looks like **"nonfactors.grid.mvc6"**
4. You are trying to get to a folder in that directory that is named **"content"**
5. The path there from **"nonfactors.grid.mvc6"** should be something like : **"nonfactors.grid.mvc6\<some version number>\content"**
    - My path is **"nonfactors.grid.mvc6\5.0.0\content"**
6. In that**"content"** directory there should be three folders:
    - css
    - js
    - Views
7. Go into the **"Views"** directory, then go into **"Shared"**.
8. There should be a folder named **"MvcGrid"**
9. Copy that **"MvcGrid"** folder into your projects **"Views\Shared"** directory
    - Do not just copy the files in the **"MvcGrid"** folder, copy the whole folder 
10. Now in your **"Views"** folder in your project there should be a **"_ViewImports.cshtml"** file
11. In that file copy the following text : 
```
@using NonFactors.Mvc.Grid;
```
    - My altered file looks like thie 
    ```
    @using deleteMe
@using deleteMe.Models
@using NonFactors.Mvc.Grid;
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
    ```
12. Go back to the **"contents"** folder in the cached **"nonfactors.grid.mvc6\<some version number>\content"**
13. Now we want to copy the folder **"mvc-grid"** from the **"css"** directory
14. Your project should have a folder named **"wwwroot"**. This is a special directory that will have its data sent to the 
browser. So any CSS or javascript files in that directory will be available to be used by the enduser's browser.
15. We want to paste the **"mvc-grid"** folder in the **"wwwroot/css"** directory
16. Now that the files are in place we have to let the project know where to find them when it creates the HTML.
17. In your project there should be a path like this **"Views/Shared/"** and afile named **"_Layout.cshtml"**
    - That layout file is used as a starting point for the HTML that is created by default.
    - Since we want all of our Views to have the Mvc6 features, I will alter that layout page
18. Copy the following text into the  **"_Layout.cshtml"** file:
```
<link href="~/css/mvc-grid/mvc-grid.css" rel="stylesheet">
```
It has to be between the <head></head> section. My chunk of HTML looks like this after the change"
```
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewData["Title"] - AspNetCoreSorti7ngFilterExample</title>

    <environment include="Development">
        <link rel="stylesheet" href="~/lib/bootstrap/dist/css/bootstrap.css" />
    </environment>
    <environment exclude="Development">
        <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css"
              asp-fallback-href="~/lib/bootstrap/dist/css/bootstrap.min.css"
              asp-fallback-test-class="sr-only" asp-fallback-test-property="position" asp-fallback-test-value="absolute"
              crossorigin="anonymous"
              integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" />
    </environment>
    <link rel="stylesheet" href="~/css/site.css" />
    <link href="~/css/mvc-grid/mvc-grid.css" rel="stylesheet">
</head>
```
19. Now go back to the **"content"** folder
20. There should be a folder named **"js"**, go into that directory
21. Now copy the folder**"mvc-grid"** 
22. That folder should be pasted in the **"wwwroot/js"** directory of your project
23. Once it the folder is pasted, we need to tell the code where to find it and how to use it
24. Copy the following text: 
```
<script src="~/js/mvc-grid/mvc-grid.js"></script>
        <script>
           [].forEach.call(document.getElementsByClassName('mvc-grid'), function (element) {
               new MvcGrid(element);
           });
        </script>
```
25. This text will be pasted into the bottom portion of the <body></body> section of the **"_Layout.cshtml"** file we used earlier in our project
The modified file for me looks something like
```
<body>
    ...bit of text ...
    <environment include="Development">
        <script src="~/lib/jquery/dist/jquery.js"></script>
        <script src="~/lib/bootstrap/dist/js/bootstrap.bundle.js"></script>
    </environment>
    <environment exclude="Development">
        <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.3.1/jquery.min.js"
                asp-fallback-src="~/lib/jquery/dist/jquery.min.js"
                asp-fallback-test="window.jQuery"
                crossorigin="anonymous"
                integrity="sha256-FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8=">
        </script>
        <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.bundle.min.js"
                asp-fallback-src="~/lib/bootstrap/dist/js/bootstrap.bundle.min.js"
                asp-fallback-test="window.jQuery && window.jQuery.fn && window.jQuery.fn.modal"
                crossorigin="anonymous"
                integrity="sha384-xrRywqdh3PHs8keKZN+8zzc5TX0GRTLCcmivcbNJWm2rs5C8PRhcEn3czEjhAO9o">
        </script>
    </environment>
    <script src="~/js/site.js" asp-append-version="true"></script>
    <script src="~/js/mvc-grid/mvc-grid.js"></script>
    <script>
        [].forEach.call(document.getElementsByClassName('mvc-grid'), function (element) {
                           new MvcGrid(element);
                       });
    </script>

    @RenderSection("Scripts", required: false)
</body>
```


Once the above is done you are ready to use the features that Mvc6 has to offer.
The following code was taken from [here](http://mvc6-grid.azurewebsites.net/)


This is an example of what your cshtml would like if using the Mvc6 library.

```
@(Html
    .Grid(Model)
    .Build(columns =>
    {
        columns.Add(model => model.Name).Titled("Name");
        columns.Add(model => model.Surname).Titled("Surname");
        columns.Add(model => model.MaritalStatus).Titled("Marital status");

        columns.Add(model => model.Age).Titled("Age");
        columns.Add(model => model.Birthday).Titled("Birthday").Formatted("{0:d}");
        columns.Add(model => model.IsWorking).Titled("Employed");
    })
    .Empty("No data found")
    .Filterable()
    .Sortable()
    .Pageable()
)
```
