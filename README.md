# Microsoft Orleans HelloWorld .Net8

## 1. Run Visual Studio 2022 Community Edition and create a new blank solution 

We create a new project
![image](https://github.com/luiscoco/Microsoft_Orleans_HelloWorld_dotNet8/assets/32194879/ee71b567-06d1-49db-8fea-8ee61c026c87)

We select the project template **blank solution**
![image](https://github.com/luiscoco/Microsoft_Orleans_HelloWorld_dotNet8/assets/32194879/b73f17b2-e2f0-4df0-9a1f-b59f3fa525fb)

We input the project name and location 
![image](https://github.com/luiscoco/Microsoft_Orleans_HelloWorld_dotNet8/assets/32194879/db8426a7-2bca-4086-9e01-496c84b80514)

This is the new project folders structure

![image](https://github.com/luiscoco/Microsoft_Orleans_HelloWorld_dotNet8/assets/32194879/8c5c21f4-0ddf-4508-a484-b133292e6a9d)

### 1.1. We create the GrainsInterfaces project (Classes Library app)

We right click on the solution and we add a new project 

![image](https://github.com/luiscoco/Microsoft_Orleans_HelloWorld_dotNet8/assets/32194879/13dc6688-86c4-4af0-96e0-e06995b0b1cb)

We select the project template **Classes library**

![image](https://github.com/luiscoco/Microsoft_Orleans_HelloWorld_dotNet8/assets/32194879/ceea3ead-9547-468a-919b-5ff5cfe1a0c6)

We select the project location and the project name

This is the project folders structure

![image](https://github.com/luiscoco/Microsoft_Orleans_HelloWorld_dotNet8/assets/32194879/6846b957-17e2-4f68-bbe3-86a92a3d60b4)

Do not forget to load the project dependency **Microsoft.Orleans.SDK**

This is the interface source code

**IHello.cs**

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace GrainsInterfaces
{
    public interface IHello : IGrainWithIntegerKey
    {
        ValueTask<string> SayHello(string greeting);
    }
}

```

### 1.2. We create the GrainsInterfaces project (Classes Library app)

Following the steps explained in section 1.1. we also create a new project for the Grains.

This is the new project structure

![image](https://github.com/luiscoco/Microsoft_Orleans_HelloWorld_dotNet8/assets/32194879/d6788c7a-6437-4e10-9f61-caea58be0cec)

Do not forget to load the projec dependencies/libraries: **Microsoft.Orleans.SDK**, **Microsoft.Extensions.Logging.Abstractions** and also the project reference: **GrainsInterfaces.csproj**

We also input the grains source code

**HelloGrain.cs**

```csharp
using GrainsInterfaces;
using Microsoft.Extensions.Logging;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Grains
{
    public class HelloGrain : Grain, IHello
    {
        private readonly ILogger _logger;

        public HelloGrain(ILogger<HelloGrain> logger)
        {
            _logger = logger;
        }

        public ValueTask<string> SayHello(string greeting)
        {
            _logger.LogInformation(
            "SayHello message received: greeting = '{Greeting}'", greeting);

            return ValueTask.FromResult(
                $"""
            Client said: '{greeting}', so HelloGrain says: Hello!
            """);
        }
    }
}
```

### 1.3. We create the Silo project (Console app)

We create a new Console application for defining the Silo

This is the project structure

![image](https://github.com/luiscoco/Microsoft_Orleans_HelloWorld_dotNet8/assets/32194879/a4fef97a-617d-41cc-b815-da6ec6f8ffca)

Do not forget to load the project dependencies: **Microsoft.Extensions.Hosting**, **Microsoft.Extensions.Logging.Console**, **Microsoft.Orleans.Server** and the project reference: **Grains.csproj**

**program.cs**

```csharp
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;

try
{
    using IHost host = await StartSiloAsync();
    Console.WriteLine("\n\n Press Enter to terminate...\n\n");
    Console.ReadLine();

    await host.StopAsync();

    return 0;
}
catch (Exception ex)
{
    Console.WriteLine(ex);
    return 1;
}

static async Task<IHost> StartSiloAsync()
{
    var builder = new HostBuilder()
        .UseOrleans(silo =>
        {
            silo.UseLocalhostClustering()
                .ConfigureLogging(logging => logging.AddConsole());
        });

    var host = builder.Build();
    await host.StartAsync();

    return host;
}
```

### 1.4. We create the Client project (Console app)



**program.cs**

```csharp

```

## See also this repo for more info

https://github.com/willvelida/orleans-apps/tree/main

https://github.com/willvelida?tab=repositories

https://learn.microsoft.com/es-es/dotnet/orleans/host/configuration-guide/server-configuration?pivots=orleans-7-0

https://learn.microsoft.com/es-es/dotnet/orleans/host/configuration-guide/client-configuration?pivots=orleans-7-0

