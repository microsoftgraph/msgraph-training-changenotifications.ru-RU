<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="59aaa-101">Откройте файл **Startup.CS** и закомментируйте приведенную ниже строку, чтобы отключить перенаправление SSL.</span><span class="sxs-lookup"><span data-stu-id="59aaa-101">Open the **Startup.cs** file and comment out the following line to disable ssl redirection.</span></span>

```csharp
//app.UseHttpsRedirection();
```

### <a name="add-model-classes"></a><span data-ttu-id="59aaa-102">Добавление классов модели</span><span class="sxs-lookup"><span data-stu-id="59aaa-102">Add model classes</span></span>

<span data-ttu-id="59aaa-103">Приложение использует несколько новых классов модели для (de) сериализации сообщений в Microsoft Graph или из него.</span><span class="sxs-lookup"><span data-stu-id="59aaa-103">The application uses several new model classes for (de)serialization of messages to/from the Microsoft Graph.</span></span>

<span data-ttu-id="59aaa-104">Щелкните правой кнопкой мыши дерево файлов проекта и выберите пункт **создать папку**.</span><span class="sxs-lookup"><span data-stu-id="59aaa-104">Right-click in the project file tree and select **New Folder**.</span></span> <span data-ttu-id="59aaa-105">Назовите **модели** ИТ</span><span class="sxs-lookup"><span data-stu-id="59aaa-105">Name it **Models**</span></span>

<span data-ttu-id="59aaa-106">Щелкните правой кнопкой мыши \*\*\*\* папку Models и добавьте три новых файла:</span><span class="sxs-lookup"><span data-stu-id="59aaa-106">Right-click the **Models** folder and add three new files:</span></span>

- <span data-ttu-id="59aaa-107">**Notification.cs**</span><span class="sxs-lookup"><span data-stu-id="59aaa-107">**Notification.cs**</span></span>
- <span data-ttu-id="59aaa-108">**ResourceData.cs**</span><span class="sxs-lookup"><span data-stu-id="59aaa-108">**ResourceData.cs**</span></span>
- <span data-ttu-id="59aaa-109">**MyConfig.cs**</span><span class="sxs-lookup"><span data-stu-id="59aaa-109">**MyConfig.cs**</span></span>

<span data-ttu-id="59aaa-110">Замените содержимое **Notification.CS** следующим:</span><span class="sxs-lookup"><span data-stu-id="59aaa-110">Replace the contents of **Notification.cs** with the following:</span></span>

```csharp
using Newtonsoft.Json;
using System;

namespace msgraphapp.Models
{
  public class Notifications
  {
    [JsonProperty(PropertyName = "value")]
    public Notification[] Items { get; set; }
  }

  // A change notification.
  public class Notification
  {
    // The type of change.
    [JsonProperty(PropertyName = "changeType")]
    public string ChangeType { get; set; }

    // The client state used to verify that the notification is from Microsoft Graph. Compare the value received with the notification to the value you sent with the subscription request.
    [JsonProperty(PropertyName = "clientState")]
    public string ClientState { get; set; }

    // The endpoint of the resource that changed. For example, a message uses the format ../Users/{user-id}/Messages/{message-id}
    [JsonProperty(PropertyName = "resource")]
    public string Resource { get; set; }

    // The UTC date and time when the webhooks subscription expires.
    [JsonProperty(PropertyName = "subscriptionExpirationDateTime")]
    public DateTimeOffset SubscriptionExpirationDateTime { get; set; }

    // The unique identifier for the webhooks subscription.
    [JsonProperty(PropertyName = "subscriptionId")]
    public string SubscriptionId { get; set; }

    // Properties of the changed resource.
    [JsonProperty(PropertyName = "resourceData")]
    public ResourceData ResourceData { get; set; }
  }
}
```

<span data-ttu-id="59aaa-111">Замените содержимое **ResourceData.CS** следующим:</span><span class="sxs-lookup"><span data-stu-id="59aaa-111">Replace the contents of **ResourceData.cs** with the following:</span></span>

```csharp
using Newtonsoft.Json;

namespace msgraphapp.Models
{
  public class ResourceData
  {
    // The ID of the resource.
    [JsonProperty(PropertyName = "id")]
    public string Id { get; set; }

    // The OData etag property.
    [JsonProperty(PropertyName = "@odata.etag")]
    public string ODataEtag { get; set; }

    // The OData ID of the resource. This is the same value as the resource property.
    [JsonProperty(PropertyName = "@odata.id")]
    public string ODataId { get; set; }

    // The OData type of the resource: "#Microsoft.Graph.Message", "#Microsoft.Graph.Event", or "#Microsoft.Graph.Contact".
    [JsonProperty(PropertyName = "@odata.type")]
    public string ODataType { get; set; }
  }
}
```

<span data-ttu-id="59aaa-112">Замените содержимое **MyConfig.CS** следующим:</span><span class="sxs-lookup"><span data-stu-id="59aaa-112">Replace the contents of **MyConfig.cs** with the following:</span></span>

```csharp
namespace msgraphapp
{
    public class MyConfig
    {
        public string AppId { get; set; }
        public string AppSecret { get; set; }
        public string TenantId { get; set; }
        public string Ngrok { get; set; }
    }
}
```

<span data-ttu-id="59aaa-113">Откройте файл **Startup.CS** .</span><span class="sxs-lookup"><span data-stu-id="59aaa-113">Open the **Startup.cs** file.</span></span> <span data-ttu-id="59aaa-114">Откройте метод method `ConfigureServices()` & замените его следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="59aaa-114">Locate the method `ConfigureServices()` method & replace it with the following code:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
    var config = new MyConfig();
    Configuration.Bind("MyConfig", config);
    services.AddSingleton(config);
}
```

<span data-ttu-id="59aaa-115">Откройте файл **appSettings. JSON** и замените его содержимое на приведенный ниже код.</span><span class="sxs-lookup"><span data-stu-id="59aaa-115">Open the **appsettings.json** file and replace the content the following.</span></span>

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Warning"
    }
  },
  "MyConfig":
  {
    "AppId": "<APP ID>",
    "AppSecret": "<APP SECRET>",
    "TenantId": "<TENANT ID>",
    "Ngrok": "<NGROK URL>"
  }
}
```

<span data-ttu-id="59aaa-116">Замените следующие переменные значениями, скопированными ранее:</span><span class="sxs-lookup"><span data-stu-id="59aaa-116">Replace the following variables with the values you copied earlier:</span></span>

- <span data-ttu-id="59aaa-117">`<NGROK URL>`необходимо указать URL-адрес ngrok HTTPS, скопированный ранее.</span><span class="sxs-lookup"><span data-stu-id="59aaa-117">`<NGROK URL>` should be set to the https ngrok url you copied earlier.</span></span>
- <span data-ttu-id="59aaa-118">`<TENANT ID>`Это идентификатор клиента Office 365, например: **contoso.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="59aaa-118">`<TENANT ID>` should be your Office 365 tenant id, for example: **contoso.onmicrosoft.com**.</span></span>
- <span data-ttu-id="59aaa-119">`<APP ID>`и `<APP SECRET>` он должен быть идентификатором и секретом приложения, скопированным ранее при создании регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="59aaa-119">`<APP ID>` and `<APP SECRET>` should be the application id and secret you copied earlier when you created the application registration.</span></span>

### <a name="add-notification-controller"></a><span data-ttu-id="59aaa-120">Добавление контроллера уведомлений</span><span class="sxs-lookup"><span data-stu-id="59aaa-120">Add notification controller</span></span>

<span data-ttu-id="59aaa-121">Для обработки подписки и уведомления приложению требуется новый контроллер.</span><span class="sxs-lookup"><span data-stu-id="59aaa-121">The application requires a new controller to process the subscription and notification.</span></span>

<span data-ttu-id="59aaa-122">Щелкните правой кнопкой мыши `Controllers` папку, выберите пункт **создать файл**и назовите контроллер **NotificationsController.CS**.</span><span class="sxs-lookup"><span data-stu-id="59aaa-122">Right-click the `Controllers` folder, select **New File**, and name the controller **NotificationsController.cs**.</span></span>

<span data-ttu-id="59aaa-123">Замените содержимое **NotificationController.CS** на следующий код:</span><span class="sxs-lookup"><span data-stu-id="59aaa-123">Replace the contents of **NotificationController.cs** with the following code:</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Net.Http;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using msgraphapp.Models;
using Newtonsoft.Json;
using System.Net;
using System.Net.Http.Formatting;
using System.Threading;
using Microsoft.Graph;
using Microsoft.Identity.Client;
using System.Net.Http.Headers;

namespace msgraphapp.Controllers
{
  [Route("api/[controller]")]
  [ApiController]
  public class NotificationsController : ControllerBase
  {
    private readonly MyConfig config;

    public NotificationsController(MyConfig config)
    {
      this.config = config;
    }

    [HttpGet]
    public ActionResult<string> Get()
    {
      var graphServiceClient = GetGraphClient();

      var sub = new Microsoft.Graph.Subscription();
      sub.ChangeType = "updated";
      sub.NotificationUrl = config.Ngrok + "/api/notifications";
      sub.Resource = "/users";
      sub.ExpirationDateTime = DateTime.UtcNow.AddMinutes(5);
      sub.ClientState = "SecretClientState";

      var newSubscription = graphServiceClient
        .Subscriptions
        .Request()
        .AddAsync(sub).Result;

      return $"Subscribed. Id: {newSubscription.Id}, Expiration: {newSubscription.ExpirationDateTime}";
    }

    public ActionResult<string> Post([FromQuery]string validationToken = null)
    {
      // handle validation
      if(!string.IsNullOrEmpty(validationToken))
      {
        Console.WriteLine($"Received Token: '{validationToken}'");
        return Ok(validationToken);
      }

      // handle notifications
      using (StreamReader reader = new StreamReader(Request.Body))
      {
        string content = reader.ReadToEnd();

        Console.WriteLine(content);

        var notifications = JsonConvert.DeserializeObject<Notifications>(content);

        foreach(var notification in notifications.Items)
        {
          Console.WriteLine($"Received notification: '{notification.Resource}', {notification.ResourceData?.Id}");
        }
      }

      return Ok();
    }

    private GraphServiceClient GetGraphClient()
    {
      var graphClient = new GraphServiceClient(new DelegateAuthenticationProvider((requestMessage) => {

          // get an access token for Graph
          var accessToken = GetAccessToken().Result;

          requestMessage
              .Headers
              .Authorization = new AuthenticationHeaderValue("bearer", accessToken);

          return Task.FromResult(0);
      }));

      return graphClient;
    }

    private async Task<string> GetAccessToken()
    {
      IConfidentialClientApplication app = ConfidentialClientApplicationBuilder.Create(config.AppId)
        .WithClientSecret(config.AppSecret)
        .WithAuthority($"https://login.microsoftonline.com/{config.TenantId}")
        .WithRedirectUri("https://daemon")
        .Build();

      string[] scopes = new string[] { "https://graph.microsoft.com/.default" };

      var result = await app.AcquireTokenForClient(scopes).ExecuteAsync();

      return result.AccessToken;
    }

  }
}
```

<span data-ttu-id="59aaa-124">**Сохраните** все файлы.</span><span class="sxs-lookup"><span data-stu-id="59aaa-124">**Save** all files.</span></span>