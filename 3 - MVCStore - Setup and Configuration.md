# CRUD ASP.NET MVC Core Application

## Create the project
1. To create the project, select `New > Project` from the Visual Studio `File` menu and select the `Templates > Visual C# > .NET Core` section of the `New Project` dialog window. 
2. Select the ASP.NET Core Web Application (.NET Core) item, and enter `MVCStore` into the Name field.
3. Choose the `Empty` template.
3. Run the project. Why do you think that we are seeing the "Hello World!" text?

## Creating the Folder Structure

5. Add the following folders

    |Name|Description |
    | ------------- |-------------|
    Models |This folder will contain the model classes.|
    Controllers | This folder will contain the controller classes.
    Views | This folder holds everything related to views, including individual Razor files, the view start file, and the view imports file.

## Configuring the Application

6. Modify the `ConfigureServices` method in the `Startup` class as follows in order to enable the MVC framework and some related features that are useful for development.

    ``` c#
    public void ConfigureServices(IServiceCollection services)
    {
        // !!!! add this line{ 
        services.AddMvc();
        // }!!!!
    }
    ```

7. Modify the `Configure` method in the `Startup` class as follows in order to enable the MVC framework and some related features that are useful for development.

    ``` c#
    // This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        if (env.IsDevelopment())
        {
            app.UseDeveloperExceptionPage();
        }
        else
        {
            app.UseExceptionHandler("/Home/Error");
            app.UseHsts();
        }

        app.UseHttpsRedirection();
        app.UseStaticFiles();

        app.UseRouting();

        app.UseEndpoints(endpoints =>
            {
                endpoints.MapControllerRoute(
                    name: "default",
                    pattern: "{controller=Home}/{action=Index}/{id?}");
            });
    }
    ```

    |Name|Description |
    | ------------- |-------------|
    UseDeveloperExceptionPage() | This extension method displays details of exceptions that occur in the application, which is useful during the development process. It should not be enabled in deployed applications.
    UseDatabaseErrorPage() | Captures synchronous and asynchronous database related exceptions from the pipeline that may be resolved using Entity Framework migrations. When these exceptions occur an HTML response with details of possible actions to resolve the issue is generated.
    UseHsts() | Adds middleware for using HSTS, which adds the Strict-Transport-Security header.
    UseHttpsRedirection() | Adds middleware for redirecting HTTP Requests to HTTPS.
    UseStaticFiles() |This extension method enables support for serving static content from the wwwroot folder.
    UseMvcWithDefaultRoute() | This extension method enables ASP.NET Core MVC with a default configuration.

7. Add the MVC View Imports Page. 
    
    Right-click the Views folder, select Add > New Item from the pop-up menu, and select the MVC View Imports Page item from the ASP.NET Core > Web > ASP.NET category
    
    ``` c#
    @addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
    ```

    The `@using` statement will allow us to use the types in the MVCStore.Models namespace in views without needing to refer to the namespace. The @addTagHelper statement enables the built-in tag helpers.

8. Run the application. An error message is shown because there are no controllers in the application to handle requests at the moment.

## Add the Unit Test Project
9. Right-click on the solution item in the Solution Explorer and select Add > New Project from the popup menu. Select xUnit Test Project (.NET Core) from the list of project templates and set the name of the project to MVCStore.Tests. Click OK to create the unit test project.

10. Add a reference towards the `MVCStore` project.

11. Install the Moq NuGet package.