# ASP.net core web api documentation with swagger/openApi
In the world of web api and microservices, understanding web api's methods and endpoints is quite challenging. Traditional way to create documentation as file with word or PDF. But it is very difficult to maintained and keeping documentation updated as per changes. Now swagger which also known as openAPI solves the problem of web api documentation and testing.

## What is Swagger/OpenAPI?
Swagger is a language-agnostic specification for describing REST APIs. Swagger project was donated to OpenAPI Initiative where it is called as openAPI. So both these names are used interchangeably. Swagger/OpenAPI allows both human and computers to understand capabilities of web api without interacting its implementation (code, deployments etc). There are two main goals are

1. Minimize the time and effort to connect two disconnected services. 
2. Minimize time and effort for web api documentation

In this document we will went through <b>Swashbuckle.Aspnetcore</b> and <b>NSwag.net</b>

<b>Swashbuckle.Aspnetcore</b> - Swashbuckle.aspnetcore is an open source project for .net core documentation.

<b>NSwag.net</b> - NSwag.net is another open source project for .net core web api documentation, additionally provide capabilities of creating C# and TypeScript clients for web api.

## Starting with swashbuckle and aspnet core
Swashbuckle.AspNetCore mainly consists of three components

<b>Swashbuckle.AspNetCore.Swagger</b> - Swagger object and middleware to expose SwaggerDocument object as JSON.

<b>Swashbuckle.AspNetCore.SwaggerGen</b> - Swagger generator which builds SwaggerDocument directly from web api controllers and models. It typically combines swagger endpoint middleware to automatically expose swagger JSON.

<b>Swashbuckle.AspNetCore.SwaggerUI</b> - It interpret swagger json and create UI for web api.

For implementation, i am using visual studio 2019 with .Net core 3.1. Here are steps 

1. Open visual studio 2019 and create a new project with template ASP.Net core web application and select web api type project
2. Install nuget pckage "Swashbuckle.AspNetCore" for now its pre-release so i am using version 5.0.0-rc5.
   Open Solution Explorer --> Right click to dependencies folder --> select manage nuget package option --> Search for Swashbuckle.AspNetCore --> Install
3. Next step is to modify our startup class to add swagger dependencies and middlewares

Import following namespace

using Microsoft.OpenApi.Models;

Add swagger generator to the services collection by adding below code to Startup.ConfigureServices method

services.AddSwaggerGen(conf =><br />
{<br />
  conf.SwaggerDoc("v1", new OpenApiInfo {<br />
      Title="Api documentation",<br />
      Version = "1.0.0"<br />
  });<br />
});

Next enable middleware’s for serving generated swagger json and swagger ui by adding below code to startup.configure method

app.UseSwagger();

app.UseSwaggerUI(opt =><br />
{<br />
  opt.SwaggerEndpoint("/swagger/v1/swagger.json", "Web api documentation");<br />  
});

Now all should go as expected, run application with ctrl+F5 or F5 and hit URL baseurl/swagger (https://localhost:44313/swagger for my demo application). 

In all above document it's minimum and siplest way to enable openAPI/swagger to web api. We can also extend this documentation to more information like api description, contact details and licence info etc. To extend we documentation we need provide all these details to services.AddSwaggerGen method under Startup.ConfigureServices as 

services.AddSwaggerGen(conf =><br />
{
conf.SwaggerDoc("v1", new OpenApiInfo<br />
{<br />
Title = "Api documentation",<br />
Version = "1.0.0",<br />
Description = "Demo api for ducumentation",<br />
License = new OpenApiLicense<br />
{<br />
Name = "Licence name",<br />
Url = new Uri("https://licence_Terms_URL.com")<br />
},<br />
Contact = new OpenApiContact<br />
{<br />
Name = "Surender Tanwar",<br />
Email = "tanwar.mydream3010@gmail.com",<br />
Url = new Uri("https://github.com/Surender1987")<br />
}<br />
});<br />
});<br />

Addition to above we can also use XML comments for dumenation through swagger. It will automativally produce document from XML comment. To include xml comments for documentation we have to enable xml documentation file in project 

Right click to solution ---> Properties ---> Select buld tab in left ---> Under output section select checkbox forr xml documentation file ---> Save with ctrl + s

Next, add following code to services.AddSwaggerGen under startup.configureservices method 

 // Set the comments path for the Swagger JSON and UI.<br />
var xmlFile = $"{Assembly.GetEntryAssembly().GetName().Name}.xml";<br />
var xmlPath = Path.Combine(AppContext.BaseDirectory, xmlFile);<br />
conf.IncludeXmlComments(xmlPath);<br />
                
Add xml comments to controller actions as example given below

/// <summary><br />
/// Creates a TodoItem.<br />
/// </summary><br />
/// <remarks><br />
/// Sample request:<br />
///<br />
/// POST /Todo<br />
/// {<br />
/// "id": 1,<br />
/// "name": "Item1",<br />
/// "isComplete": true<br />
/// }<br />
///<br />
/// </remarks><br />
/// <param name="item"></param><br />
/// <returns>A newly created TodoItem</returns><br />
/// <response code="201">Returns the newly created item</response><br />
/// <response code="400">If the item is null</response><br />

These all comments will be added to swagger UI
