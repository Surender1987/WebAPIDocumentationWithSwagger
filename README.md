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
2. 
