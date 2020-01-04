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
