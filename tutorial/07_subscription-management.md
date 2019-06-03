<!-- markdownlint-disable MD002 MD041 -->

Подписки на уведомления истечет, и их необходимо периодически обновлять.

Откройте **NotificationsController.CS** и замените `Get()` метод следующим кодом:

```csharp
private static Dictionary<string, Subscription> Subscriptions = new Dictionary<string, Subscription>();
private static Timer subscriptionTimer = null;

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

Добавьте приведенный ниже оператор using в начало файла.

```csharp
using System.Threading;
```

В приведенном выше коде добавляется фоновый таймер, который будет срабатывать каждые 15 секунд, и проверьте, истек ли срок действия подписки.

Добавьте следующие новые методы:

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

Этот `CheckSubscriptions` метод вызывается каждые 15 секунд с помощью таймера. Для производственного использования это значение должно быть более разумным, чтобы уменьшить количество ненужных вызовов Graph. `RenewSubscription` Метод обновляет подписку и вызывается только в том случае, если срок действия подписки истечет в течение следующих двух минут.

Чтобы запустить приложение, выберите **отладка > начать отладку** . Перейдите по следующему URL- `*http://localhost:5000/api/notifications` адресу, чтобы зарегистрировать новую подписку.

В `DEBUG OUTPUT` окне Visual Studio Code отображается следующий результат приблизительно каждые 15 секунд.  Это таймер проверки подписки на срок действия.

```shell
Checking subscriptions 12:32:51.882
Current subscription count 1
```

Подождите несколько минут, и при необходимости обновите подписку, вы увидите следующее:

```shell
Renewed subscription: 07ca62cd-1a1b-453c-be7b-4d196b3c6b5b, New Expiration: 3/10/2019 7:43:22 PM +00:00
```

Это означает, что подписка обновлена и показывает новое время действия.
