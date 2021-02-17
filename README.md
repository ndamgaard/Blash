# Documentation

Full documentation is available at https://www.roundthecode.com/code-examples/blash

Blash
Blash is a Twitter dashboard, which displays real-time tweets from search queries of your choice.

It's written as a Blazor WebAssembly application, Microsoft's newest web framework.

Some of the benefits of using Blazor WebAssembly include being able to write client-side functionality using C#. That means that don't have to use JavaScript.

The Blazor WebAssembly application integrates with an ASP.NET Core Web API.

The Web API communicates with the Twitter API to search a list of recent tweets for a particular query.

In-order to listen to real-time tweets, the Web API connects to the filtered stream provided by the Twitter API. It then integrates those tweets into it's SQL Server database, and sends the tweet to the Blazor WebAssembly application using SignalR.

So the Twitter API knows what tweets to send as part of it's filtered stream, we have set up what is known as "rules". Rules are basically Twitter search rules, so we only get the tweets we want in real time.

Blash uses these rules and converts them into dashboards to be displayed to the end user.

Rules are specific to a particular client ID connecting to the Twitter API.

Blash is a Blazor written Twitter dashboard, that receives real-time tweets from the Twitter API.
Blash is a Blazor written Twitter dashboard, that receives real-time tweets from the Twitter API.
How It Works
When the Web API starts up, it runs a series of jobs in the background. These include:

Importing the rules from the Twitter API and stores them as dashboards in the database.
Starts listening to real-time tweets from the Twitter API.
Gets a recent search for all the rules we are using from the Twitter API, and stores them as tweets in the database.
Only when these jobs are completed does the Web API start running.

With the Blazor WebAssembly application, it calls an endpoint to get all the dashboards and the tweets that it belongs to.

In-addition, it establishes a WebSocket connection with SignalR through the Web API. The purpose of this connection is for the Blazor WebAssembly application to know when:

A dashboard is created (as another user might create the dashboard).
A dashboard is deleted (as another user might delete the dashboard).
When a tweet is created, and the dashboards it belongs to.
When a tweet is deleted from a particular dashboard.
Resync of all the dashboards and their tweets.
This is so it can update the dashboard in real-time.

Software
This is the software that will need to be installed onto your machine.

Visual Studio 2019. Version 16.8.2 or above. It will work with the free community version.
SQL Server 2017, or above.
.NET 5.0 SDK, or above.
Get The Application Working
These are the steps to get the application working.

Fill out the Download the Source Code form. We will send you an email where you can download the source code.
Create a Twitter Developer account. You can follow our guide on how to set up a Twitter project to get a client ID and secret that you will need.
Inside the source code, there is a folder called Database. Within that folder, there is a file called RoundTheCode_Blash.bak. This needs to be imported as a database into your SQL Server.
From there, you will need to update some settings to get the application working. You will need to open up the Web/RoundTheCode.Blash.Api/appsettings.json file and change the following settings.

Check the database connection is correct in ConnectionStrings > BlashDbContext.
Set the client ID that you got from your Twitter project in Api > TwitterApi > ClientId.
Set the client secret that you got from your Twitter project in Api > TwitterApi > ClientSecret.
You are now ready to go.

Open the Project in Visual Studio
Open up RoundTheCode.Blash.sln in Visual Studio.

You will need to check that both the Blash API and the Blazor WebAssembly application are set up to run on startup.

Right-click on the solution and select "Set Startup Projects...".

How to Setup Startup Projects in Visual Studio 2019
How to Setup Startup Projects in the Blash Visual Studio project.
Select Multiple startup projects, and for RoundTheCode.Blash.Api and RoundTheCode.Blash.BlazorWasm, make sure that the action is set to Start.


Make sure that the API and Blazor WebAssembly are started up.
Press OK to confirm the changes. Then start the project in Visual Studio.

You should find that the Web API runs on https://localhost:5001, and the Blazor WebAssembly runs on https://localhost:5002.

It's the Blazor WebAssembly application where you can view your Twitter Dashboard, so open up a browser and navigate to https://localhost:5002.
