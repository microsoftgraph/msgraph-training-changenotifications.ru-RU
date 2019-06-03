<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="6efe7-101">Подписки на уведомления истечет, и их необходимо периодически обновлять.</span><span class="sxs-lookup"><span data-stu-id="6efe7-101">Subscriptions for notifications expire and need to be renewed periodically.</span></span>

<span data-ttu-id="6efe7-102">Откройте **NotificationsController.CS** и замените `Get()` метод следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="6efe7-102">Open **NotificationsController.cs** and replace the `Get()` method with the following code:</span></span>

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

<span data-ttu-id="6efe7-103">Добавьте приведенный ниже оператор using в начало файла.</span><span class="sxs-lookup"><span data-stu-id="6efe7-103">Add the following using statement at the top of the file.</span></span>

```csharp
using System.Threading;
```

<span data-ttu-id="6efe7-104">В приведенном выше коде добавляется фоновый таймер, который будет срабатывать каждые 15 секунд, и проверьте, истек ли срок действия подписки.</span><span class="sxs-lookup"><span data-stu-id="6efe7-104">This code above adds a background timer that will fire every 15 seconds and check subscriptions to see if they have expired.</span></span>

<span data-ttu-id="6efe7-105">Добавьте следующие новые методы:</span><span class="sxs-lookup"><span data-stu-id="6efe7-105">Add the following new methods:</span></span>

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

<span data-ttu-id="6efe7-106">Этот `CheckSubscriptions` метод вызывается каждые 15 секунд с помощью таймера.</span><span class="sxs-lookup"><span data-stu-id="6efe7-106">The `CheckSubscriptions` method is called every 15 seconds by the timer.</span></span> <span data-ttu-id="6efe7-107">Для производственного использования это значение должно быть более разумным, чтобы уменьшить количество ненужных вызовов Graph.</span><span class="sxs-lookup"><span data-stu-id="6efe7-107">For production use this should be set to a more reasonable value to reduce the number of unnecessary calls to Graph.</span></span> <span data-ttu-id="6efe7-108">`RenewSubscription` Метод обновляет подписку и вызывается только в том случае, если срок действия подписки истечет в течение следующих двух минут.</span><span class="sxs-lookup"><span data-stu-id="6efe7-108">The `RenewSubscription` method renews a subscription and is only called if a subscription is going to expire in the next two minutes.</span></span>

<span data-ttu-id="6efe7-109">Чтобы запустить приложение, выберите **отладка > начать отладку** .</span><span class="sxs-lookup"><span data-stu-id="6efe7-109">Select **Debug > Start debugging** to run the application.</span></span> <span data-ttu-id="6efe7-110">Перейдите по следующему URL- `*http://localhost:5000/api/notifications` адресу, чтобы зарегистрировать новую подписку.</span><span class="sxs-lookup"><span data-stu-id="6efe7-110">Navigate to the following url `*http://localhost:5000/api/notifications` to register a new subscription.</span></span>

<span data-ttu-id="6efe7-111">В `DEBUG OUTPUT` окне Visual Studio Code отображается следующий результат приблизительно каждые 15 секунд.</span><span class="sxs-lookup"><span data-stu-id="6efe7-111">You will see the following output in the `DEBUG OUTPUT` window of Visual Studio Code approximately every 15 seconds.</span></span>  <span data-ttu-id="6efe7-112">Это таймер проверки подписки на срок действия.</span><span class="sxs-lookup"><span data-stu-id="6efe7-112">This is the timer checking the subscription for expiry.</span></span>

```shell
Checking subscriptions 12:32:51.882
Current subscription count 1
```

<span data-ttu-id="6efe7-113">Подождите несколько минут, и при необходимости обновите подписку, вы увидите следующее:</span><span class="sxs-lookup"><span data-stu-id="6efe7-113">Wait a few minutes and you will see the following when the subscription needs renewing:</span></span>

```shell
Renewed subscription: 07ca62cd-1a1b-453c-be7b-4d196b3c6b5b, New Expiration: 3/10/2019 7:43:22 PM +00:00
```

<span data-ttu-id="6efe7-114">Это означает, что подписка обновлена и показывает новое время действия.</span><span class="sxs-lookup"><span data-stu-id="6efe7-114">This indicates that the subscription was renewed and shows the new expiry time.</span></span>
