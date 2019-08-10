# Readme

[Electron.NET](https://github.com/ElectronNET/Electron.NET/tree/master)


# from scratch

`dotnet new mvc`

`dotnet add package ElectronNET.API`

`sudo npm install electron-builder --global`
`sudo npm install electron-packager --global`

Add the following to your csproj

```xml
<ItemGroup>
    <DotNetCliToolReference Include="ElectronNET.CLI" Version="0.0.9" />
</ItemGroup>
```

`dotnet restore`

Jetzt sollte dotnet electronize Einsatz bereit sein

`dotnet electronize help`

## Program.cs 

```csharp
public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
    WebHost.CreateDefaultBuilder(args)
        .UseStartup<Startup>()
        .UseElectron(args);
```

## StartUp.cs 

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    else
    {
        app.UseExceptionHandler("/Home/Error");
    }

    app.UseStaticFiles();

    app.UseMvc(routes =>
    {
        routes.MapRoute(
            name: "default",
            template: "{controller=Home}/{action=Index}/{id?}");
    });

    // Open the Electron-Window here
    Task.Run(async () => await Electron.WindowManager.CreateWindowAsync());
}
```

## Build und Run 

`dotnet electronize init`

`dotnet electronize start`

## Publish 

`dotnet electronize build /target osx`
`dotnet electronize build /target win`



