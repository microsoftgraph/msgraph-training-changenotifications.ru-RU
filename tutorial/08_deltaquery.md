<!-- markdownlint-disable MD002 MD041 -->

### <a name="query-for-changes"></a><span data-ttu-id="49fe1-101">Запрос изменений</span><span class="sxs-lookup"><span data-stu-id="49fe1-101">Query for changes</span></span>

<span data-ttu-id="49fe1-102">Microsoft Graph предоставляет возможность запрашивать изменения в определенном ресурсе с момента его последнего вызова.</span><span class="sxs-lookup"><span data-stu-id="49fe1-102">Microsoft Graph offers the ability to query for changes to a particular resource since you last called it.</span></span> <span data-ttu-id="49fe1-103">При использовании этого параметра вместе с уведомлениями об изменениях включается надежный шаблон, который не может быть проигнорированием изменений в ресурсах.</span><span class="sxs-lookup"><span data-stu-id="49fe1-103">Using this option, combined with Change Notifications, enables a robust pattern for ensuring you don't miss any changes to the resources.</span></span>

<span data-ttu-id="49fe1-104">Откройте и откройте следующий контроллер: **controllers > NotificationsController.CS**.</span><span class="sxs-lookup"><span data-stu-id="49fe1-104">Locate and open the following controller: **Controllers > NotificationsController.cs**.</span></span>
<span data-ttu-id="49fe1-105">Добавьте следующий код к существующему `NotificationsController` классу.</span><span class="sxs-lookup"><span data-stu-id="49fe1-105">Add the following code to the existing `NotificationsController` class.</span></span>

<span data-ttu-id="49fe1-106">Этот код включает новый метод `CheckForUpdates()`, который будет вызывать Microsoft Graph с использованием URL-адреса Дельта, а затем страницы по результатам до тех пор, пока не `deltalink` обнаружит новый на завершающей странице результатов.</span><span class="sxs-lookup"><span data-stu-id="49fe1-106">This code includes a new method, `CheckForUpdates()`, that will call the Microsoft Graph using the delta url and then pages through the results until it finds a new `deltalink` on the final page of results.</span></span> <span data-ttu-id="49fe1-107">URL-адрес сохраняется в памяти до тех пор, пока код не будет снова уведомлен при срабатывании другого уведомления.</span><span class="sxs-lookup"><span data-stu-id="49fe1-107">It stores the url in memory until the code is notified again when another notification is triggered.</span></span>

```csharp
private static object DeltaLink = null;

private static IUserDeltaCollectionPage lastPage = null;

private void CheckForUpdates()
{
  var graphClient = GetGraphClient();

  // get a page of users
  var users = GetUsers(graphClient, DeltaLink);

  OutputUsers(users);

  // go through all of the pages so that we can get the delta link on the last page.
  while (users.NextPageRequest != null)
  {
    users = users.NextPageRequest.GetAsync().Result;
    OutputUsers(users);
  }

  object deltaLink;

  if (users.AdditionalData.TryGetValue("@odata.deltaLink", out deltaLink))
  {
    DeltaLink = deltaLink;
  }
}

private void OutputUsers(IUserDeltaCollectionPage users)
{
  foreach(var user in users)
    {
      var message = $"User: {user.Id}, {user.GivenName} {user.Surname}";
      Console.WriteLine(message);
    }
}

private IUserDeltaCollectionPage GetUsers(GraphServiceClient graphClient, object deltaLink)
{
  IUserDeltaCollectionPage page;

  if(lastPage == null)
  {
    page = graphClient
      .Users
      .Delta()
      .Request()
      .GetAsync()
      .Result;

  }
  else
  {
    lastPage.InitializeNextPageRequest(graphClient, deltaLink.ToString());
    page = lastPage.NextPageRequest.GetAsync().Result;
  }

  lastPage = page;
  return page;
}
```

<span data-ttu-id="49fe1-108">Откройте существующий `Post()` метод и замените его следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="49fe1-108">Locate the existing `Post()` method and replace it with the following code:</span></span>

```csharp
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

  // use deltaquery to query for all updates
  CheckForUpdates();

  return Ok();
}
```

<span data-ttu-id="49fe1-109">`Post` Метод теперь будет вызываться `CheckForUpdates` при получении уведомления.</span><span class="sxs-lookup"><span data-stu-id="49fe1-109">The `Post` method will now call `CheckForUpdates` when a notification is received.</span></span> <span data-ttu-id="49fe1-110">Под `Post` методом добавьте следующие два новых метода:</span><span class="sxs-lookup"><span data-stu-id="49fe1-110">Below the `Post` method add the following two new methods:</span></span>

<span data-ttu-id="49fe1-111">**Сохраните** все файлы.</span><span class="sxs-lookup"><span data-stu-id="49fe1-111">**Save** all files.</span></span>

### <a name="test-your-changes"></a><span data-ttu-id="49fe1-112">Протестируйте изменения:</span><span class="sxs-lookup"><span data-stu-id="49fe1-112">Test your changes:</span></span>

<span data-ttu-id="49fe1-113">В Visual Studio Code выберите **отладка > начать отладку** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="49fe1-113">Within Visual Studio Code, select **Debug > Start debugging** to run the application.</span></span>
<span data-ttu-id="49fe1-114">Перейдите по следующему URL-адресу: **http://localhost:5000/api/notifications**.</span><span class="sxs-lookup"><span data-stu-id="49fe1-114">Navigate to the following url: **http://localhost:5000/api/notifications**.</span></span> <span data-ttu-id="49fe1-115">При этом будет зарегистрирована новая подписка.</span><span class="sxs-lookup"><span data-stu-id="49fe1-115">This will register a new subscription.</span></span>

<span data-ttu-id="49fe1-116">Откройте браузер и перейдите в [центр администрирования Microsoft 365 (https://admin.microsoft.com/AdminPortal)](https://admin.microsoft.com/AdminPortal).</span><span class="sxs-lookup"><span data-stu-id="49fe1-116">Open a browser and navigate to the [Microsoft 365 admin center (https://admin.microsoft.com/AdminPortal)](https://admin.microsoft.com/AdminPortal).</span></span>

1. <span data-ttu-id="49fe1-117">Если вам будет предложено войти, войдите с помощью учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="49fe1-117">If prompted to login, sign-in using an admin account.</span></span>
1. <span data-ttu-id="49fe1-118">Выберите **пользователи > активные пользователи**.</span><span class="sxs-lookup"><span data-stu-id="49fe1-118">Select **Users > Active users**.</span></span> 
1. <span data-ttu-id="49fe1-119">Выберите активного пользователя и нажмите **изменить** для его **контактной информации**.</span><span class="sxs-lookup"><span data-stu-id="49fe1-119">Select an active user and select **Edit** for their **Contact information**.</span></span> 
1. <span data-ttu-id="49fe1-120">Обновите значение **мобильного телефона** , указав новое число и нажмите кнопку **сохранить**.</span><span class="sxs-lookup"><span data-stu-id="49fe1-120">Update the **Mobile phone** value with a new number and Select **Save**.</span></span>

<span data-ttu-id="49fe1-121">Дождитесь получения уведомления, как указано в **консоли отладки**кода Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="49fe1-121">Wait for the notification to be received as indicated in the Visual Studio Code **Debug Console**:</span></span>

```shell
Received notification: 'Users/7a7fded6-0269-42c2-a0be-512d58da4463', 7a7fded6-0269-42c2-a0be-512d58da4463
```

<span data-ttu-id="49fe1-122">Теперь приложение будет инициировать разностный запрос с графом, чтобы получить всех пользователей и выйти из этих сведений в выходные данные консоли.</span><span class="sxs-lookup"><span data-stu-id="49fe1-122">The application will now initiate a delta query with the graph to get all the users and log out some of their details to the console output.</span></span>

```shell
User: 19e429d2-541a-4e0b-9873-6dff9f48fabe, Allan Deyoung
User: 05501e79-f527-4913-aabf-e535646d7ffa, Christie Cline
User: fecac4be-76e7-48ec-99df-df745854aa9c, Debra Berger
User: 4095c5c4-b960-43b9-ba53-ef806d169f3e, Diego Siciliani
User: b1246157-482f-420c-992c-fc26cbff74a5, Emily Braun
User: c2b510b7-1f76-4f75-a9c1-b3176b68d7ca, Enrico Cattaneo
User: 6ec9bd4b-fc6a-4653-a291-70d3809f2610, Grady Archie
User: b6924afe-cb7f-45a3-a904-c9d5d56e06ea, Henrietta Mueller
User: 0ee8d076-4f13-4e1a-a961-eac2b29c0ef6, Irvin Sayers
User: 31f66f05-ac9b-4723-9b5d-8f381f5a6e25, Isaiah Langer
User: 7ee95e20-247d-43ef-b368-d19d96550c81, Johanna Lorenz
User: b2fa93ac-19a0-499b-b1b6-afa76c44a301, Joni Sherman
User: 01db13c5-74fc-470a-8e45-d6d736f8a35b, Jordan Miller
User: fb0b8363-4126-4c34-8185-c998ff697a60, Lee Gu
User: ee75e249-a4c1-487b-a03a-5a170c2aa33f, Lidia Holloway
User: 5449bd61-cc63-40b9-b0a8-e83720eeefba, Lynne Robbins
User: 7ce295c3-25fa-4d79-8122-9a87d15e2438, Miriam Graham
User: 737fe0a7-0b67-47dc-b7a6-9cfc07870705, Nestor Wilke
User: a1572b58-35cd-41a0-804a-732bd978df3e, Patti Fernandez
User: 7275e1c4-5698-446c-8d1d-fa8b0503c78a, Pradeep Gupta
User: 96ab25eb-6b69-4481-9d28-7b01cf367170, Megan Bowen
User: 846327fa-e6d6-4a82-89ad-5fd313bff0cc, Alex Wilber
User: 200e4c7a-b778-436c-8690-7a6398e5fe6e, MOD Administrator
User: 7a7fded6-0269-42c2-a0be-512d58da4463, Adele Vance
User: 752f0102-90f2-4b8d-ae98-79dee995e35e,   Removed?:deleted
User: 4887248a-6b48-4ba5-bdd5-fed89d8ea6a0,   Removed?:deleted
User: e538b2d5-6481-4a90-a20a-21ad55ce4c1d,   Removed?:deleted
User: bc5994d9-4404-4a14-8fb0-46b8dccca0ad,   Removed?:deleted
User: d4e3a3e0-72e9-41a6-9538-c23e10a16122,   Removed?:deleted
Got deltalink
```

<span data-ttu-id="49fe1-123">На портале администрирования Microsoft 365 повторите процедуру редактирования пользователя и повторите попытку **сохранения** .</span><span class="sxs-lookup"><span data-stu-id="49fe1-123">In the Microsoft 365 Admin Portal, repeat the process of editing a user and **Save** again.</span></span>

<span data-ttu-id="49fe1-124">Приложение получит еще одно уведомление и запросит граф еще раз с помощью полученной последней разностной ссылки.</span><span class="sxs-lookup"><span data-stu-id="49fe1-124">The application will receive another notification and will query the graph again using the last delta link it received.</span></span> <span data-ttu-id="49fe1-125">Тем не менее, на этот раз вы заметите, что в результатах было возвращено только измененный пользователь.</span><span class="sxs-lookup"><span data-stu-id="49fe1-125">However, this time you will notice that only the modified user was returned in the results.</span></span>

```shell
User: 7a7fded6-0269-42c2-a0be-512d58da4463, Adele Vance
```

<span data-ttu-id="49fe1-126">Используя это сочетание уведомлений с разностным запросом, вы можете быть уверены, что вы не пропустите обновление ресурса.</span><span class="sxs-lookup"><span data-stu-id="49fe1-126">Using this combination of notifications with delta query you can be assured you wont miss any updates to a resource.</span></span> <span data-ttu-id="49fe1-127">Уведомления могут быть пропущены из-за проблем с временным подключением, но при следующем получении приложением уведомления все изменения, внесенные с момента последнего успешного запроса, будут извлекаться.</span><span class="sxs-lookup"><span data-stu-id="49fe1-127">Notifications may be missed due to transient connection issues, however the next time your application gets a notification it will pick up all the changes since the last successful query.</span></span>
