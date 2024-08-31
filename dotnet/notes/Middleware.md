# Midddlware

- ASP.NET Core Middleware Components are the basic building blocks of the Request Processing Pipeline in ASP.NET Core Applications. The pipeline determines how the HTTP Requests and Responses will be processed in the ASP.NET Core Application. Middleware components are used to implement various functionalities like authentication, error handling, routing, and logging.

* The most important point you need to remember is that a given Middleware component should only have a specific purpose, i.e., a single responsibility.

![MiddleWare request processing](/Assets/image.png "MiddleWare request processing")

```js
 namespace FirstCoreWebApplication
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // Initializes the configuration for the web application
            var builder = WebApplication.CreateBuilder(args);
            
            // Builds the web application based on the configured settings
            var app = builder.Build();

            // Middleware configuration section:
            // Activates the Developer Exception Page in Development environment to show detailed error messages
            if (app.Environment.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }

            // Adds the routing middleware to the request processing pipeline which is required to use the routing capabilities
            app.UseRouting();

            // Endpoint configuration section:
            // Maps HTTP GET requests to the root URL "/" to a method returning "Hello World!"
            app.Map("/", () => "Hello World!");

            // Maps HTTP GET requests to "/greet" URL to a method returning a greeting message
            app.Map("/greet", () => "Hello from the /greet endpoint!");

            // Maps HTTP GET requests to "/greet/{name}" URL to a method that uses a route parameter
            app.Map("/greet/{name}", (string name) => $"Hello, {name}!");

            // Starts the web application which begins listening for incoming requests
            app.Run();
        }
    }
}
```