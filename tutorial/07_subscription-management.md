<!-- markdownlint-disable MD002 MD041 -->

Подписки на уведомления истечет, и их необходимо периодически обновлять. В следующих действиях показано, как обновлять уведомления.

Открытие **контроллеров > файл NotificationsController.CS**

Добавьте в `NotificationsController` класс следующие два объявления членов:

```csharp
private static Dictionary<string, Subscription> Subscriptions = new Dictionary<string, Subscription>();
private static Timer subscriptionTimer = null;
```

Добавьте следующие новые методы. Они реализуют фоновый таймер, который будет запускаться каждые 15 секунд, чтобы проверить, истек ли срок действия подписок. Если они есть, они будут обновлены.

```csharp
private void CheckSubscriptions(Object stateInfo)
{
  AutoResetEvent autoEvent = (AutoResetEvent)stateInfo;

  Console.WriteLine($"Checking subscriptions {DateTime.Now.ToString("h:mm:ss.fff")}");
  Console.WriteLine($"Current subscription count {Subscriptions.Count()}");

  foreach(var subscription in Subscriptions)
  {
    // if the subscription expires in the next 2 min, renew it
    if(subscription.Value.ExpirationDateTime < DateTime.UtcNow.AddMinutes(2))
    {
      RenewSubscription(subscription.Value);
    }
  }
}

private void RenewSubscription(Subscription subscription)
{
  Console.WriteLine($"Current subscription: {subscription.Id}, Expiration: {subscription.ExpirationDateTime}");

  var graphServiceClient = GetGraphClient();

  subscription.ExpirationDateTime = DateTime.UtcNow.AddMinutes(5);

  var foo = graphServiceClient
    .Subscriptions[subscription.Id]
    .Request()
    .UpdateAsync(subscription).Result;

  Console.WriteLine($"Renewed subscription: {subscription.Id}, New Expiration: {subscription.ExpirationDateTime}");
}
```

Этот `CheckSubscriptions` метод вызывается каждые 15 секунд с помощью таймера. Для производственного использования это значение должно быть более разумным, чтобы уменьшить количество ненужных звонков в Microsoft Graph.

`RenewSubscription` Метод обновляет подписку и вызывается только в том случае, если срок действия подписки истечет в течение следующих двух минут.

Укажите метод `Get()` и замените его следующим кодом:

```csharp
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

    Subscriptions[newSubscription.Id] = newSubscription;

    if(subscriptionTimer == null)
    {
        subscriptionTimer = new Timer(CheckSubscriptions, null, 5000, 15000);
    }

    return $"Subscribed. Id: {newSubscription.Id}, Expiration: {newSubscription.ExpirationDateTime}";
}
```

Добавьте следующий оператор после существующих `using` операторов в начале файла:

```csharp
using System.Threading;
```

### <a name="test-the-changes"></a>Протестируйте изменения:

В Visual Studio Code выберите **отладка > начать отладку** для запуска приложения.
Перейдите по следующему URL-адресу: **http://localhost:5000/api/notifications**. При этом будет зарегистрирована новая подписка.

В окне **консоли отладки** кода Visual Studio приблизительно каждые 15 секунд Обратите внимание на то, что время ожидания подписки проверяется следующим образом:

```shell
Checking subscriptions 12:32:51.882
Current subscription count 1
```

Подождите несколько минут, и при необходимости обновите подписку, вы увидите следующее:

```shell
Renewed subscription: 07ca62cd-1a1b-453c-be7b-4d196b3c6b5b, New Expiration: 3/10/2019 7:43:22 PM +00:00
```

Это означает, что подписка обновлена и показывает новое время действия.