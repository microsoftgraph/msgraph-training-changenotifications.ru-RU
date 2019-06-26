<!-- markdownlint-disable MD002 MD041 -->

### <a name="query-for-changes"></a>Запрос изменений

Microsoft Graph предоставляет возможность запрашивать изменения в определенном ресурсе с момента его последнего вызова. При использовании этого параметра вместе с уведомлениями об изменениях включается надежный шаблон, который не может быть проигнорированием изменений в ресурсах.

Откройте и откройте следующий контроллер: **controllers > NotificationsController.CS**.
Добавьте следующий код к существующему `NotificationsController` классу.

Этот код включает новый метод `CheckForUpdates()`, который будет вызывать Microsoft Graph с использованием URL-адреса Дельта, а затем страницы по результатам до тех пор, пока не `deltalink` обнаружит новый на завершающей странице результатов. URL-адрес сохраняется в памяти до тех пор, пока код не будет снова уведомлен при срабатывании другого уведомления.

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

Откройте существующий `Post()` метод и замените его следующим кодом:

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

`Post` Метод теперь будет вызываться `CheckForUpdates` при получении уведомления. Под `Post` методом добавьте следующие два новых метода:

**Сохраните** все файлы.

### <a name="test-your-changes"></a>Протестируйте изменения:

В Visual Studio Code выберите **отладка > начать отладку** для запуска приложения.
Перейдите по следующему URL-адресу: **http://localhost:5000/api/notifications**. При этом будет зарегистрирована новая подписка.

Откройте браузер и перейдите в [центр администрирования Microsoft 365 (https://admin.microsoft.com/AdminPortal)](https://admin.microsoft.com/AdminPortal).

1. Если вам будет предложено войти, войдите с помощью учетной записи администратора.
1. Выберите **пользователи > активные пользователи**. 
1. Выберите активного пользователя и нажмите **изменить** для его **контактной информации**. 
1. Обновите значение **мобильного телефона** , указав новое число и нажмите кнопку **сохранить**.

Дождитесь получения уведомления, как указано в **консоли отладки**кода Visual Studio:

```shell
Received notification: 'Users/7a7fded6-0269-42c2-a0be-512d58da4463', 7a7fded6-0269-42c2-a0be-512d58da4463
```

Теперь приложение будет инициировать разностный запрос с графом, чтобы получить всех пользователей и выйти из этих сведений в выходные данные консоли.

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

На портале администрирования Microsoft 365 повторите процедуру редактирования пользователя и повторите попытку **сохранения** .

Приложение получит еще одно уведомление и запросит граф еще раз с помощью полученной последней разностной ссылки. Тем не менее, на этот раз вы заметите, что в результатах было возвращено только измененный пользователь.

```shell
User: 7a7fded6-0269-42c2-a0be-512d58da4463, Adele Vance
```

Используя это сочетание уведомлений с разностным запросом, вы можете быть уверены, что вы не пропустите обновление ресурса. Уведомления могут быть пропущены из-за проблем с временным подключением, но при следующем получении приложением уведомления все изменения, внесенные с момента последнего успешного запроса, будут извлекаться.
