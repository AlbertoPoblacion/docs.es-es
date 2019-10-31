---
title: Implementación de puertas de enlace de API con Ocelot
description: Obtenga información sobre cómo implementar puertas de enlace de API con Ocelot y cómo usar Ocelot en un entorno basado en contenedores.
ms.date: 10/02/2018
ms.openlocfilehash: cb452c330712ecf536cdf09f41fdbf828a4e9314
ms.sourcegitcommit: 559259da2738a7b33a46c0130e51d336091c2097
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/22/2019
ms.locfileid: "72771183"
---
# <a name="implement-api-gateways-with-ocelot"></a>Implementación de puertas de enlace de API con Ocelot

En la aplicación de microservicio de referencia [eShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers) se usa [Ocelot](https://github.com/ThreeMammals/Ocelot), una puerta de enlace de API simple y ligera que se puede implementar en cualquier lugar junto con los microservicios y contenedores, como en cualquiera de los entornos siguientes que se usan en eShopOnContainers.

- Host de Docker, en el equipo PC de desarrollo local, en el entorno local o en la nube.
- Clúster de Kubernetes, de forma local o en la nube administrada como Azure Kubernetes Service (AKS).
- Clúster de Service Fabric local o en la nube.
- Malla de Service Fabric, como PaaS o sin servidor en Azure.

## <a name="architect-and-design-your-api-gateways"></a>Arquitectura y diseño de las puertas de enlace de API

En el diagrama de arquitectura siguiente se muestra cómo se implementan las puertas de enlace de API con Ocelot en eShopOnContainers.

![Diagrama de arquitectura de eShopOnContainers en el que se muestran aplicaciones cliente, microservicios y las puertas de enlace de API intermedias](./media/image28.png)

**Figura 6-28**. Arquitectura de eShopOnContainers con puertas de enlace de API

En ese diagrama se muestra cómo se implementa toda la aplicación en un único host de Docker o PC de desarrollo con "Docker para Windows" o "Docker para Mac". Pero la implementación en cualquier orquestador sería bastante similar y cualquiera de los contenedores del diagrama se podría escalar horizontalmente en el orquestador.

Además, los recursos de infraestructura como bases de datos, caché y agentes de mensajes se deberían descargar del orquestador e implementarse en sistemas de alta disponibilidad para la infraestructura, como Azure SQL Database, Azure Cosmos DB, Azure Redis, Azure Service Bus o cualquier solución de agrupación en clústeres de alta disponibilidad local.

Como también se puede observar en el diagrama, tener varias puertas de enlace de API permite que varios equipos de desarrollo sean autónomos (en este caso, las características de Marketing frente a las de Shopping) al desarrollar e implementar sus microservicios además de sus propias puertas de enlace de API relacionadas.

Si tuviera una sola puerta de enlace de API monolítica, sería un único punto para actualizar por varios equipos de desarrollo, que podrían acoplar todos los microservicios con un único elemento de la aplicación.

Ampliando mucho más el diseño, en ocasiones una puerta de enlace de API específica también se puede limitar a un microservicio empresarial individual en función de la arquitectura elegida. El tener los límites de la puerta de enlace de API dictados por el negocio o el dominio le ayudará a lograr un mejor diseño.

Por ejemplo, la especificidad del nivel de puerta de enlace de API puede ser especialmente útil para aplicaciones de interfaz de usuario compuesta más avanzadas que se basan en microservicios, dado que el concepto de una puerta de enlace de API específica es similar a un servicio de composición de interfaz de usuario.

Nos adentramos en más detalles en la sección anterior, [Creación de interfaz de usuario compuesta basada en microservicios](../architect-microservice-container-applications/microservice-based-composite-ui-shape-layout.md).

Como punto clave, para muchas aplicaciones de tamaño medio y grande, el uso de una puerta de enlace de API personalizada suele ser un enfoque adecuado, pero no como un único agregador monolítico ni una única puerta de enlace de API personalizada central, a menos que esa puerta de enlace de API permita varias áreas de configuración independientes para que los diferentes equipos de desarrollo creen microservicios autónomos.

### <a name="sample-microservicescontainers-to-re-route-through-the-api-gateways"></a>Microservicios y contenedores de ejemplo para redistribuir entre las puertas de enlace de API

Como ejemplo, eShopOnContainers tiene aproximadamente seis tipos de microservicio internos que se tienen que publicar entre las puertas de enlace de API, como se muestra en la imagen siguiente.

![Solo los microservicios Basket, Catalog, Location, Marketing, Ordering y Payment se publican a través de la puerta de enlace de API.](./media/image29.png)

**Figura 6-29**. Carpetas de microservicio en la solución eShopOnContainers en Visual Studio

En cuanto al servicio Identity, en el diseño se excluye del enrutamiento de puerta de enlace de API, porque es el único interés transversal del sistema, aunque con Ocelot también es posible incluirlo como parte de las listas de reenrutamiento.

Todos estos servicios se implementan actualmente como servicios de API web de ASP.NET Core, como se desprende del código. Centrémonos en uno de los microservicios, como el código del microservicio Catalog.

![Vista del Explorador de soluciones del proyecto Catalog.API.](./media/image30.png)

**Figura 6-30**. Microservicio de API web de ejemplo (microservicio Catalog)

Puede ver que el microservicio Catalog es un proyecto de API web de ASP.NET Core típico con varios controladores y métodos, como en el código siguiente.

```csharp
[HttpGet]
[Route("items/{id:int}")]
[ProducesResponseType((int)HttpStatusCode.BadRequest)]
[ProducesResponseType((int)HttpStatusCode.NotFound)]
[ProducesResponseType(typeof(CatalogItem),(int)HttpStatusCode.OK)]
public async Task<IActionResult> GetItemById(int id)
{
    if (id <= 0)
    {
        return BadRequest();
    }
    var item = await _catalogContext.CatalogItems.
                                          SingleOrDefaultAsync(ci => ci.Id == id);
    //…

    if (item != null)
    {
        return Ok(item);
    }
    return NotFound();
}
```

La solicitud HTTP terminará ejecutando ese tipo de código de C# que accede a la base de datos de microservicios además de cualquier otra acción requerida.

En lo que respecta a la dirección URL del microservicio, cuando los contenedores se implementan en el equipo de desarrollo local (el host de Docker local), el contenedor de cada microservicio siempre tiene un puerto interno (normalmente el puerto 80) que se especifica en su Dockerfile, como se muestra en el Dockerfile siguiente:

```Dockerfile
FROM microsoft/aspnetcore:2.0.5 AS base
WORKDIR /app
EXPOSE 80
```

El puerto 80 que se muestra en el código es interno dentro del host de Docker, por lo que las aplicaciones cliente no pueden acceder a él.

Las aplicaciones cliente solo pueden acceder a los puertos externos (si existen) publicados al implementar con `docker-compose`.

Esos puertos externos no se deben publicar al implementar en un entorno de producción. Por esto precisamente se va a usar la puerta de enlace de API, para evitar la comunicación directa entre las aplicaciones cliente y los microservicios.

Pero durante el desarrollo, le interesa acceder directamente al contenedor o microservicio, y ejecutarlo a través de Swagger. Por eso en eShopOnContainers se siguen especificando los puertos externos, aunque la puerta de enlace de API o las aplicaciones cliente no los vayan a usar.

Este es un ejemplo del archivo `docker-compose.override.yml` para el microservicio Catalog:

```yml
catalog.api:
  environment:
    - ASPNETCORE_ENVIRONMENT=Development
    - ASPNETCORE_URLS=http://0.0.0.0:80
    - ConnectionString=YOUR_VALUE
    - ... Other Environment Variables
  ports:
    - "5101:80"   # Important: In a production environment you should remove the external port (5101) kept here for microservice debugging purposes.
                  # The API Gateway redirects and access through the internal port (80).
```

Puede ver cómo en la configuración de docker-compose.override.yml el puerto interno del contenedor Catalog es el puerto 80, pero el puerto para el acceso externo es 5101. Pero la aplicación no debería usar este puerto cuando se utiliza una puerta de enlace de API, solo para depurar, ejecutar y probar el microservicio Catalog.

Normalmente, no se puede implementar con docker-compose en un entorno de producción porque el entorno de implementación de producción correcto para los microservicios es un orquestador como Kubernetes o Service Fabric. Cuando se implementa en esos entornos, se usan otros archivos de configuración en los que no se publica directamente ningún puerto externo para los microservicios, pero siempre se usa al proxy inverso de la puerta de enlace de API.

Ejecute el microservicio Catalog en el host de Docker local ya sea mediante la ejecución de la solución eShopOnContainers completa desde Visual Studio (ejecutará todos los servicios de los archivos docker-compose) o iniciando el microservicio con el comando docker-compose siguiente en CMD o PowerShell desde la carpeta donde están `docker-compose.yml` y docker-compose.override.yml.

```console
docker-compose run --service-ports catalog.api
```

Este comando solo ejecuta el contenedor del servicio catalog.api además de las dependencias que se especifican en el archivo docker-compose.yml. En este caso, el contenedor de SQL Server y el contenedor de RabbitMQ.

Después, puede acceder directamente al microservicio Catalog y ver sus métodos a través de la interfaz de usuario de Swagger, a la que se accede directamente a través de ese puerto "externo", en este caso `http://localhost:5101/swagger`:

![Vista del explorador de la edad de la interfaz de usuario de Swagger para la API REST Catalog.API.](./media/image31.png)

**Figura 6-31**. Probar el microservicio Catalog con su interfaz de usuario de Swagger

En este momento, podría establecer un punto de interrupción en el código de C# en Visual Studio, probar el microservicio con los métodos expuestos en la interfaz de usuario de Swagger y, por último, limpiar todo con el comando `docker-compose down`.

Pero la comunicación de acceso directo al microservicio, en este caso a través del puerto externo 5101, es precisamente lo que se quiere evitar en la aplicación. Y se puede evitar si se establece el nivel adicional de direccionamiento indirecto de la puerta de enlace de API (en este caso, Ocelot). De ese modo, la aplicación cliente no accederá directamente al microservicio.

## <a name="implementing-your-api-gateways-with-ocelot"></a>Implementación de las puertas de enlace de API con Ocelot

Ocelot es básicamente un conjunto de software intermedio que se puede aplicar en un orden específico.

Ocelot está diseñado para trabajar solamente con ASP.NET Core. Está destinado a .NET Standard 2.0, por lo que se puede usar en cualquier lugar donde se admita .NET Standard 2.0, incluido el runtime de .NET Core 2.0 y el de .NET Framework 4.6.1 o superior.

Ocelot y sus dependencias se instalan en el proyecto de ASP.NET Core con el [paquete NuGet de Ocelot](https://www.nuget.org/packages/Ocelot/), desde Visual Studio.

```powershell
Install-Package Ocelot
```

En eShopOnContainers, su implementación de puerta de enlace de API es un proyecto ASP.NET Core WebHost simple, y el software intermedio de Ocelot controla todas las características de la puerta de enlace de API, como se muestra en la imagen siguiente:

![Vista del Explorador de soluciones del proyecto de puerta de enlace de API Ocelot.](./media/image32.png)

**Figura 6-32**. El proyecto base de OcelotApiGw en eShopOnContainers

Este proyecto ASP.NET Core WebHost se compila básicamente con dos archivos sencillos: `Program.cs` y `Startup.cs`.

El archivo Program.cs solo tiene que crear y configurar el típico BuildWebHost de ASP.NET Core.

```csharp
namespace OcelotApiGw
{
    public class Program
    {
        public static void Main(string[] args)
        {
            BuildWebHost(args).Run();
        }

        public static IWebHost BuildWebHost(string[] args)
        {
            var builder = WebHost.CreateDefaultBuilder(args);

            builder.ConfigureServices(s => s.AddSingleton(builder))
                    .ConfigureAppConfiguration(
                          ic => ic.AddJsonFile(Path.Combine("configuration",
                                                            "configuration.json")))
                    .UseStartup<Startup>();
            var host = builder.Build();
            return host;
        }
    }
}
```

Aquí, lo importante para Ocelot es el archivo `configuration.json` que se debe proporcionar al generador a través del método `AddJsonFile()`. Ese archivo `configuration.json` es donde se especifican todas las redistribuciones de la puerta de enlace de API, es decir, los puntos de conexión externos con puertos específicos y los puntos de conexión internos correlacionados, que normalmente usan otros puertos.

```json
{
    "ReRoutes": [],
    "GlobalConfiguration": {}
}
```

En la configuración hay dos secciones. Una matriz de redistribuciones y GlobalConfiguration. Las redistribuciones son los objetos que indican a Ocelot cómo procesar una solicitud de nivel superior. La configuración Global permite reemplazos de la configuración específica de redistribución. Es útil si no quiere administrar una gran cantidad de configuración específica de redistribución.

Este es un ejemplo simplificado del [archivo de configuración de redistribución](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/ApiGateways/Web.Bff.Shopping/apigw/configuration.json) de una de las puertas de enlace de API de eShopOnContainers.

```json
{
  "ReRoutes": [
    {
      "DownstreamPathTemplate": "/api/{version}/{everything}",
      "DownstreamScheme": "http",
      "DownstreamHostAndPorts": [
        {
          "Host": "catalog.api",
          "Port": 80
        }
      ],
      "UpstreamPathTemplate": "/api/{version}/c/{everything}",
      "UpstreamHttpMethod": [ "POST", "PUT", "GET" ]
    },
    {
      "DownstreamPathTemplate": "/api/{version}/{everything}",
      "DownstreamScheme": "http",
      "DownstreamHostAndPorts": [
        {
          "Host": "basket.api",
          "Port": 80
        }
      ],
      "UpstreamPathTemplate": "/api/{version}/b/{everything}",
      "UpstreamHttpMethod": [ "POST", "PUT", "GET" ],
      "AuthenticationOptions": {
        "AuthenticationProviderKey": "IdentityApiKey",
        "AllowedScopes": []
      }
    }

  ],
    "GlobalConfiguration": {
      "RequestIdKey": "OcRequestId",
      "AdministrationPath": "/administration"
    }
  }
```

La funcionalidad principal de una puerta de enlace de API de Ocelot consiste en aceptar solicitudes HTTP entrantes y reenviarlas a un servicio de nivel inferior, actualmente como otra solicitud HTTP. Ocelot describe el enrutamiento de una solicitud a otra como una redistribución.

Por ejemplo, vamos a centrarnos en una de las redistribuciones del archivo configuration.json anterior, la configuración para el microservicio Basket.

```json
{
      "DownstreamPathTemplate": "/api/{version}/{everything}",
      "DownstreamScheme": "http",
      "DownstreamHostAndPorts": [
        {
          "Host": "basket.api",
          "Port": 80
        }
      ],
      "UpstreamPathTemplate": "/api/{version}/b/{everything}",
      "UpstreamHttpMethod": [ "POST", "PUT", "GET" ],
      "AuthenticationOptions": {
        "AuthenticationProviderKey": "IdentityApiKey",
        "AllowedScopes": []
      }
}
```

DownstreamPathTemplate, Scheme y DownstreamHostAndPorts forman la dirección URL de microservicio interna a la que se va a reenviar esta solicitud.

El puerto es el puerto interno que usa el servicio. Al usar contenedores, el puerto se especifica en su Dockerfile.

`Host` es un nombre de servicio que depende de la resolución de nombres de servicio que se use. Cuando se usa docker-compose, los nombres de los servicios los proporciona el host de Docker, que usa los nombres de servicio proporcionados en los archivos docker-compose. Si se usa un orquestador como Kubernetes o Service Fabric, ese nombre se debe resolver mediante DNS o la resolución de nombres proporcionada por cada orquestador.

DownstreamHostAndPorts es una matriz que contiene el host y el puerto de los servicios de nivel inferior a los que se quieren reenviar las solicitudes. Normalmente esto solo contendrá una entrada, pero a veces es posible que quiera equilibrar la carga de las solicitudes a los servicios de nivel inferior y Ocelot permite agregar más de una entrada y después seleccionar un equilibrador de carga. Pero si se usa Azure y un orquestador, probablemente una idea mejor sea equilibrar la carga con la infraestructura de nube y de orquestador.

UpstreamPathTemplate es la dirección URL que Ocelot usará para identificar qué DownstreamPathTemplate se va a usar para una solicitud determinada desde el cliente. Por último, se usa UpstreamHttpMethod para que Ocelot pueda distinguir entre diferentes solicitudes (GET, POST, PUT) a la misma dirección URL.

En este momento, podría tener una única puerta de enlace de API de Ocelot (ASP.NET Core WebHost) con uno o [varios archivos configuration.json combinados](https://ocelot.readthedocs.io/en/latest/features/configuration.html#merging-configuration-files), o bien almacenar la [configuración en un almacén de Consul KV](https://ocelot.readthedocs.io/en/latest/features/configuration.html#store-configuration-in-consul).

Pero como se mencionó en las secciones de arquitectura y diseño, si realmente quiere tener microservicios autónomos, podría ser mejor dividir esa única puerta de enlace de API monolítica en varias puertas de enlace de API o BFF (back-end para front-end). Para ello, vamos a ver cómo se implementa este enfoque con contenedores de Docker.

### <a name="using-a-single-docker-container-image-to-run-multiple-different-api-gateway--bff-container-types"></a>Uso de una sola imagen de contenedor de Docker para ejecutar varios tipos de contenedor de puerta de enlace de API y BFF

En eShopOnContainers, se usa una sola imagen de contenedor de Docker con la puerta de enlace de API de Ocelot pero después, en tiempo de ejecución, se crean otros contenedores y servicios para cada tipo de puerta de enlace de API o BFF proporcionando otro archivo configuration.json, mediante un volumen de Docker para acceder a una carpeta distinta del equipo para cada servicio.

![En el caso de la puerta de enlace API de Ocelot, para las cuatro puertas de enlace de la API se usa una sola imagen de Docker.](./media/image33.png)

**Figura 6-33**. Volver a usar una única imagen de Docker de Ocelot entre varios tipos de puerta de enlace de API

En eShopOnContainers, la "imagen de Docker de puerta de enlace de API genérica" se crea con el proyecto "OcelotApiGw" y el nombre de imagen "eshop/ocelotapigw" que se especifica en el archivo docker-compose.yml. Después, al implementar en Docker, habrá cuatro contenedores de puerta de enlace de API que se crean a partir de esa misma imagen de Docker, como se muestra en el extracto siguiente del archivo docker-compose.yml.

```yml
  mobileshoppingapigw:
    image: eshop/ocelotapigw:${TAG:-latest}
    build:
      context: .
      dockerfile: src/ApiGateways/ApiGw-Base/Dockerfile

  mobilemarketingapigw:
    image: eshop/ocelotapigw:${TAG:-latest}
    build:
      context: .
      dockerfile: src/ApiGateways/ApiGw-Base/Dockerfile

  webshoppingapigw:
    image: eshop/ocelotapigw:${TAG:-latest}
    build:
      context: .
      dockerfile: src/ApiGateways/ApiGw-Base/Dockerfile

  webmarketingapigw:
    image: eshop/ocelotapigw:${TAG:-latest}
    build:
      context: .
      dockerfile: src/ApiGateways/ApiGw-Base/Dockerfile
```

Además, como se puede ver en el archivo docker-compose.override.yml siguiente, la única diferencia entre esos contenedores de puerta de enlace de API es el archivo de configuración de Ocelot, que es diferente para cada contenedor de servicios y que se especifica en tiempo de ejecución a través de un volumen de Docker.

```yml
mobileshoppingapigw:
  environment:
    - ASPNETCORE_ENVIRONMENT=Development
    - IdentityUrl=http://identity.api
  ports:
    - "5200:80"
  volumes:
    - ./src/ApiGateways/Mobile.Bff.Shopping/apigw:/app/configuration

mobilemarketingapigw:
  environment:
    - ASPNETCORE_ENVIRONMENT=Development
    - IdentityUrl=http://identity.api
  ports:
    - "5201:80"
  volumes:
    - ./src/ApiGateways/Mobile.Bff.Marketing/apigw:/app/configuration

webshoppingapigw:
  environment:
    - ASPNETCORE_ENVIRONMENT=Development
    - IdentityUrl=http://identity.api
  ports:
    - "5202:80"
  volumes:
    - ./src/ApiGateways/Web.Bff.Shopping/apigw:/app/configuration

webmarketingapigw:
  environment:
    - ASPNETCORE_ENVIRONMENT=Development
    - IdentityUrl=http://identity.api
  ports:
    - "5203:80"
  volumes:
    - ./src/ApiGateways/Web.Bff.Marketing/apigw:/app/configuration
```

Debido al código anterior, y como se muestra en el Explorador de Visual Studio a continuación, el único archivo necesario para definir cada puerta de enlace de API empresarial específica o BFF es simplemente un archivo configuration.json, dado que las cuatro puertas de enlace de API se basan en la misma imagen de Docker.

![La única diferencia entre las puertas de enlace de API es un archivo configuration.json en cada una de ellas.](./media/image34.png)

**Figura 6-34**. El único archivo necesario para definir cada puerta de enlace de API y BFF con Ocelot es un archivo de configuración

Al dividir la puerta de enlace de API en varias, cada equipo de desarrollo centrado en otros subconjuntos de microservicios puede administrar sus propias puertas de enlace de API mediante archivos de configuración de Ocelot independientes. Además, al mismo tiempo pueden reutilizar la misma imagen de Docker de Ocelot.

Ahora, si ejecuta eShopOnContainers con las puertas de enlace de API (incluidas de forma predeterminada en Visual Studio al abrir la solución eShopOnContainers ServicesAndWebApps.sln o al ejecutar "docker-compose up"), se ejecutarán las rutas de ejemplo siguientes.

Por ejemplo, cuando se visita la dirección URL de nivel superior `http://localhost:5202/api/v1/c/catalog/items/2/` que proporciona la puerta de enlace de API webshoppingapigw, se obtiene el mismo resultado de la dirección URL de nivel inferior interna `http://catalog.api/api/v1/2` dentro del host de Docker, como se muestra en el explorador siguiente.

![Vista del explorador de una respuesta de Catalog.api que pasa por la puerta de enlace de API.](./media/image35.png)

**Figura 6-35**. Acceso a un microservicio a través de una dirección URL proporcionada por la puerta de enlace de API

Por motivos de pruebas o depuración, si quiere acceder directamente al contenedor de Docker Catalog (solo en el entorno de desarrollo) sin pasar por la puerta de enlace de API, ya que "catalog.api" es una resolución DNS interna para el host de Docker (la detección de servicios la controlan los nombres de servicio de docker-compose), la única manera de tener acceso directo al contenedor es a través del puerto externo publicado en el archivo docker-compose.override.yml, que solo se proporciona para pruebas de desarrollo, como `http://localhost:5101/api/v1/Catalog/items/1` en el explorador siguiente.

![Vista del explorador de una respuesta de Catalog.api que va directamente a Catalog.api, idéntica a la que pasa a través de la puerta de enlace de API.](./media/image36.png)

**Figura 6-36**. Acceso directo a un microservicio con fines de prueba

Pero la aplicación está configurada para que acceda a todos los microservicios a través de las puertas de enlace de API, no a través de "atajos" de puerto directos.

### <a name="the-gateway-aggregation-pattern-in-eshoponcontainers"></a>El patrón de agregación de puertas de enlace en eShopOnContainers

Como se mencionó anteriormente, una manera flexible de implementar la agregación de solicitudes consiste en usar servicios personalizados, mediante código. También se podría implementar la agregación de solicitudes con la [característica de agregación de solicitudes en Ocelot](https://ocelot.readthedocs.io/en/latest/features/requestaggregation.html#request-aggregation), pero es posible que no sea tan flexible como se necesita. Por tanto, el método seleccionado para implementar la agregación en eShopOnContainers es mediante un servicio de API web de ASP.NET Core explícito para cada agregador.

Según ese enfoque, el diagrama de composición de las puertas de enlace de API es en realidad más amplio si se tienen en cuenta los servicios de agregador que no se mostraron en el diagrama de arquitectura global simplificado anterior.

En el diagrama siguiente, también se puede ver cómo funcionan los servicios de agregador con sus puertas de enlace de API relacionadas.

![Arquitectura de eShopOnContainers, en la que se muestran los servicios de agregador.](./media/image37.png)

**Figura 6-37**. Arquitectura de eShopOnContainers con los servicios de agregador

Al ampliar más el área empresarial "Shopping" de la imagen siguiente, se puede ver que al usar los servicios agregadores de las puertas de enlace de API se reduce el intercambio de mensajes entre las aplicaciones cliente y los microservicios.

![Acercar la arquitectura de eShopOnContainers, en la que se muestran los servicios de agregador y en la que se "construye" una respuesta que "combina" la respuesta de varios microservicios para reducir el intercambio de mensajes con el cliente final.](./media/image38.png)

**Figura 6-38**. Visión ampliada de los servicios de agregador

Se puede observar la complejidad del diagrama cuando se muestran las posibles solicitudes procedentes de las puertas de enlace de API. Aunque se puede ver cómo se simplificarían las flechas de color azul, desde la perspectiva de las aplicaciones cliente, al usar el patrón de agregadores mediante la reducción del intercambio de mensajes y la latencia de la comunicación, en última instancia se mejora de forma significativa la experiencia del usuario, especialmente para las aplicaciones remotas (aplicaciones móviles y SPA).

El caso del área empresarial "Marketing" y los microservicios es un caso de uso muy simple, por lo que no hubo necesidad de usar agregadores, pero podría ser posible, si fuera necesario.

### <a name="authentication-and-authorization-in-ocelot-api-gateways"></a>Autenticación y autorización en las puertas de enlace de API de Ocelot

En una puerta de enlace de API de Ocelot se puede ubicar el servicio de autenticación, como un servicio de API web de ASP.NET Core con [IdentityServer](https://identityserver.io/) para proporcionar el token de autenticación, fuera o dentro de la puerta de enlace de API.

Dado que en eShopOnContainers se usan varias puertas de enlace de API con límites basados en BFF y áreas de negocio, el servicio Identity/Auth se excluye de las puertas de enlace de API, como se resalta en color amarillo en el diagrama siguiente.

![Diagrama de arquitectura de eShopOnContainers en el que se muestra el microservicio Identity debajo de la puerta de enlace de API.](./media/image39.png)

**Figura 6-39**. Posición del servicio Identity en eShopOnContainers

Pero Ocelot también admite que el microservicio Identity/Auth se sitúe dentro de los límites de la puerta de enlace de API, como se muestra en este otro diagrama.

![Autenticación con el microservicio Identity debajo de la puerta de enlace de API (AG): 1) AG solicita un token de autenticación del microservicio Identity, 2) el microservicio devuelve el token a AG, 3-4) solicitudes de AG de los microservicios mediante el token de autenticación.](./media/image40.png)

**Figura 6-40**. Autenticación en Ocelot

Como en la aplicación eShopOnContainers se ha dividido la puerta de enlace de API en varios BFF (back-end para front-end) y puertas de enlace de API de áreas de negocio, otra opción habría sido crear una puerta de enlace de API adicional para los intereses transversales. Esa opción sería razonable en una arquitectura basada en microservicios más compleja con varios microservicios de intereses transversales. Como en eShopOnContainers solo hay un interés transversal, se decidió controlar solamente el servicio de seguridad fuera del territorio de la puerta de enlace de API, por motivos de simplicidad.

En cualquier caso, si la aplicación está protegida en el nivel de puerta de enlace de API, el módulo de autenticación de la puerta de enlace de API de Ocelot se visita en primer lugar cuando se intenta usar cualquier microservicio protegido. Eso redirige la solicitud HTTP al microservicio Identity o de autenticación para obtener el token de acceso para que los servicios protegidos se puedan visitar con el token de acceso.

La forma de proteger con autenticación cualquier servicio en el nivel de la puerta de enlace de API consiste en establecer AuthenticationProviderKey en su configuración relacionada en el archivo configuration.json.

```json
    {
      "DownstreamPathTemplate": "/api/{version}/{everything}",
      "DownstreamScheme": "http",
      "DownstreamHostAndPorts": [
        {
          "Host": "basket.api",
          "Port": 80
        }
      ],
      "UpstreamPathTemplate": "/api/{version}/b/{everything}",
      "UpstreamHttpMethod": [],
      "AuthenticationOptions": {
        "AuthenticationProviderKey": "IdentityApiKey",
        "AllowedScopes": []
      }
    }
```

Cuando se ejecuta Ocelot, consultará la redistribución AuthenticationOptions.AuthenticationProviderKey y comprobará que hay que un proveedor de autenticación registrado con la clave especificada. Si no lo hay, Ocelot no se iniciará. Si lo hay, la redistribución usará ese proveedor cuando se ejecute.

Como el WebHost de Ocelot está configurado con `authenticationProviderKey = "IdentityApiKey"`, eso requerirá la autenticación cada vez que el servicio tenga alguna solicitud sin ningún token de autenticación.

```csharp
namespace OcelotApiGw
{
    public class Startup
    {
        private readonly IConfiguration _cfg;

        public Startup(IConfiguration configuration) => _cfg = configuration;

        public void ConfigureServices(IServiceCollection services)
        {
            var identityUrl = _cfg.GetValue<string>("IdentityUrl");
            var authenticationProviderKey = "IdentityApiKey";
                         //…
            services.AddAuthentication()
                .AddJwtBearer(authenticationProviderKey, x =>
                {
                    x.Authority = identityUrl;
                    x.RequireHttpsMetadata = false;
                    x.TokenValidationParameters = new Microsoft.IdentityModel.Tokens.TokenValidationParameters()
                    {
                        ValidAudiences = new[] { "orders", "basket", "locations", "marketing", "mobileshoppingagg", "webshoppingagg" }
                    };
                });
            //...
        }
    }
}
```

Después, también tendrá que establecer la autorización con el atributo [Authorize] en cualquier recurso al que se vaya a acceder como los microservicios, como en el siguiente controlador del microservicio Basket.

```csharp
namespace Microsoft.eShopOnContainers.Services.Basket.API.Controllers
{
    [Route("api/v1/[controller]")]
    [Authorize]
    public class BasketController : Controller
    {
      //...
    }
}
```

ValidAudiences como "basket" se ponen en correlación con el público definido en cada microservicio con `AddJwtBearer()` en el método ConfigureServices() de la clase Startup, como se muestra en el código siguiente.

```csharp
// prevent from mapping "sub" claim to nameidentifier.
JwtSecurityTokenHandler.DefaultInboundClaimTypeMap.Clear();

var identityUrl = Configuration.GetValue<string>("IdentityUrl");

services.AddAuthentication(options =>
{
    options.DefaultAuthenticateScheme = JwtBearerDefaults.AuthenticationScheme;
    options.DefaultChallengeScheme = JwtBearerDefaults.AuthenticationScheme;

}).AddJwtBearer(options =>
{
    options.Authority = identityUrl;
    options.RequireHttpsMetadata = false;
    options.Audience = "basket";
});
```

Si intenta acceder a cualquier microservicio protegido (como Basket) con una dirección URL de redistribución basada en la puerta de enlace de API como `http://localhost:5202/api/v1/b/basket/1`, obtendrá un error "401 No autorizado" a menos que proporcione un token válido. Por otro lado, si una dirección URL de redistribución está autenticada, Ocelot invocará cualquier esquema de nivel inferior con el que esté asociada (la dirección URL de microservicio interna).

**Autorización en el nivel de redistribuciones de Ocelot.**  Ocelot admite la autorización basada en notificaciones que se evalúa después de la autenticación. La autorización se establece en un nivel de ruta mediante la adición de las líneas siguientes a la configuración de redistribución.

```json
"RouteClaimsRequirement": {
    "UserType": "employee"
}
```

En ese ejemplo, cuando se llama al software intermedio de autorización, Ocelot comprobará si el usuario tiene el tipo de notificación "UserType" en el token y si el valor de esa notificación es "employee". En caso contrario, el usuario no tendrá autorización y la respuesta será el error "403 Prohibido".

## <a name="using-kubernetes-ingress-plus-ocelot-api-gateways"></a>Uso de entrada de Kubernetes con las puertas de enlace de API de Ocelot

Al usar Kubernetes (como en un clúster de Azure Kubernetes Service) normalmente todas las solicitudes HTTP se unifican a través de la [capa de entrada de Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/) basada en *Nginx*.

En Kubernetes, si no se usa ningún enfoque de entrada, los servicios y pods tienen direcciones IP que solo son enrutables por la red de clústeres.

Pero si usa un enfoque de entrada, tendrá una capa intermedia entre Internet y los servicios (incluidas las puertas de enlace de API), que actúa como un proxy inverso.

Como definición, una entrada es una colección de reglas que permiten que las conexiones entrantes lleguen a los servicios de clúster. Normalmente, una entrada se configura para proporcionar a los servicios direcciones URL accesibles de forma externa, tráfico con equilibrio de carga, terminación SSL y mucho más. Los usuarios solicitan la entrada mediante la publicación del recurso de entrada en el servidor de API.

En eShopOnContainers, al desarrollar de forma local y usar solamente el equipo de desarrollo como el host de Docker, no se usa ninguna entrada, solo las diferentes puertas de enlace de API.

Pero cuando el destino es un entorno de "producción" basado en Kubernetes, en eShopOnContainers se usa una entrada delante de las puertas de enlace de API. De este modo, los clientes pueden seguir llamando a la misma dirección URL base, pero las solicitudes se enrutan a varias puertas de enlace de API o BFF.

Tenga en cuenta que las puertas de enlace de API actúan de front-end o fachadas en las que solo se exponen los servicios, pero no las aplicaciones web que suelen estar fuera de su ámbito. Además, es posible que las puertas de enlace de API oculten ciertos microservicios internos.

Pero la entrada simplemente redirige las solicitudes HTTP pero no intenta ocultar ningún microservicio ni aplicación web.

Tener un nivel Nginx de entrada en Kubernetes delante de las aplicaciones web además de las distintas puertas de enlace de API de Ocelot o BFF es la arquitectura ideal, como se muestra en el diagrama siguiente.

![Una entrada de Kubernetes actúa como un proxy inverso para todo el tráfico a la aplicación, incluidas las aplicaciones web, que normalmente están fuera del ámbito de la puerta de enlace de la API.](./media/image41.png)

**Figura 6-41**. El nivel de entrada en eShopOnContainers cuando se implementa en Kubernetes

Al implementar eShopOnContainers en Kubernetes, solo expone algunos servicios o puntos de conexión a través de la _entrada_, básicamente la lista siguiente de postfijos en las direcciones URL:

- `/` para la aplicación web SPA cliente
- `/webmvc` para la aplicación web MVC cliente
- `/webstatus` para la aplicación web cliente en la que se muestra el estado o las comprobaciones de estado
- `/webshoppingapigw` para el BFF web y los procesos empresariales de compra
- `/webmarketingapigw` para el BFF web y los procesos empresariales de marketing
- `/mobileshoppingapigw` para el BFF para dispositivos móviles y los procesos empresariales de compra
- `/mobilemarketingapigw` para el BFF para dispositivos móviles y los procesos empresariales de marketing

Al implementar en Kubernetes, cada puerta de enlace de API Ocelot usa un archivo "configuration.json" diferente para cada _pod_ en el que se ejecutan las puertas de enlace de API. Dichos archivos "configuration.json" se proporcionan mediante el montaje (originalmente con el script deploy.ps1) de un volumen creado en función de un _mapa de configuración_ de Kubernetes denominado "ocelot". Cada contenedor monta su archivo de configuración relacionado en la carpeta `/app/configuration` del contenedor.

En los archivos de código fuente de eShopOnContainers, los archivos "configuration.json" originales se encuentran en la carpeta `k8s/ocelot/`. Hay un archivo para cada BFF o puerta de enlace de API.

## <a name="additional-cross-cutting-features-in-an-ocelot-api-gateway"></a>Características transversales adicionales en una puerta de enlace de API de Ocelot

Cuando se usa una puerta de enlace de API de Ocelot hay otras características importantes para investigar y utilizar, como se describe en los vínculos siguientes.

- **Detección de servicios en el lado cliente mediante la integración de Ocelot con Consul o Eureka** \
  <https://ocelot.readthedocs.io/en/latest/features/servicediscovery.html>

- **Almacenamiento en caché en el nivel de puerta de enlace de API** \
  <https://ocelot.readthedocs.io/en/latest/features/caching.html>

- **Registro en el nivel de puerta de enlace de API)**  \
  <https://ocelot.readthedocs.io/en/latest/features/logging.html>

- **Calidad de servicio (reintentos e interruptores) en el nivel de puerta de enlace de API** \
  <https://ocelot.readthedocs.io/en/latest/features/qualityofservice.html>

- **Limitación de velocidad** \
  [https://ocelot.readthedocs.io/en/latest/features/ratelimiting.html](https://ocelot.readthedocs.io/en/latest/features/ratelimiting.html )

> [!div class="step-by-step"]
> [Anterior](background-tasks-with-ihostedservice.md)
> [Siguiente](../microservice-ddd-cqrs-patterns/index.md)
