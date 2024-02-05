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

```csharp

```

### 1.3. We create the Silo project (Console app)

```csharp

```

### 1.4. We create the Client project (Console app)

```csharp

```

## See also this repo for more info

https://github.com/willvelida/orleans-apps/tree/main

https://github.com/willvelida?tab=repositories

https://learn.microsoft.com/es-es/dotnet/orleans/host/configuration-guide/server-configuration?pivots=orleans-7-0

https://learn.microsoft.com/es-es/dotnet/orleans/host/configuration-guide/client-configuration?pivots=orleans-7-0

