<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="e2c39-101">Подписки на уведомления истечет, и их необходимо периодически обновлять.</span><span class="sxs-lookup"><span data-stu-id="e2c39-101">Subscriptions for notifications expire and need to be renewed periodically.</span></span> <span data-ttu-id="e2c39-102">В следующих действиях показано, как обновлять уведомления.</span><span class="sxs-lookup"><span data-stu-id="e2c39-102">The following steps will demonstrate how to renew notifications</span></span>

<span data-ttu-id="e2c39-103">Открытие **контроллеров > файл NotificationsController.CS**</span><span class="sxs-lookup"><span data-stu-id="e2c39-103">Open **Controllers > NotificationsController.cs** file</span></span>

<span data-ttu-id="e2c39-104">Добавьте в `NotificationsController` класс следующие два объявления членов:</span><span class="sxs-lookup"><span data-stu-id="e2c39-104">Add the following two member declarations to the `NotificationsController` class:</span></span>

```csharp
private static Dictionary<string, Subscription> Subscriptions = new Dictionary<string, Subscription>();
private static Timer subscriptionTimer = null;
```

<span data-ttu-id="e2c39-105">Добавьте следующие новые методы.</span><span class="sxs-lookup"><span data-stu-id="e2c39-105">Add the following new methods.</span></span> <span data-ttu-id="e2c39-106">Они реализуют фоновый таймер, который будет запускаться каждые 15 секунд, чтобы проверить, истек ли срок действия подписок.</span><span class="sxs-lookup"><span data-stu-id="e2c39-106">These will implement a background timer that will run every 15 seconds to check if subscriptions have expired.</span></span> <span data-ttu-id="e2c39-107">Если они есть, они будут обновлены.</span><span class="sxs-lookup"><span data-stu-id="e2c39-107">If they have, they will be renewed.</span></span>

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

<span data-ttu-id="e2c39-108">Этот `CheckSubscriptions` метод вызывается каждые 15 секунд с помощью таймера.</span><span class="sxs-lookup"><span data-stu-id="e2c39-108">The `CheckSubscriptions` method is called every 15 seconds by the timer.</span></span> <span data-ttu-id="e2c39-109">Для производственного использования это значение должно быть более разумным, чтобы уменьшить количество ненужных звонков в Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="e2c39-109">For production use this should be set to a more reasonable value to reduce the number of unnecessary calls to Microsoft Graph.</span></span>

<span data-ttu-id="e2c39-110">`RenewSubscription` Метод обновляет подписку и вызывается только в том случае, если срок действия подписки истечет в течение следующих двух минут.</span><span class="sxs-lookup"><span data-stu-id="e2c39-110">The `RenewSubscription` method renews a subscription and is only called if a subscription is going to expire in the next two minutes.</span></span>

<span data-ttu-id="e2c39-111">Укажите метод `Get()` и замените его следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="e2c39-111">Locate the method `Get()` and replace it with the following code:</span></span>

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

<span data-ttu-id="e2c39-112">Добавьте следующий оператор после существующих `using` операторов в начале файла:</span><span class="sxs-lookup"><span data-stu-id="e2c39-112">Add the following statement after the existing `using` statements at the top of the file:</span></span>

```csharp
using System.Threading;
```

### <a name="test-the-changes"></a><span data-ttu-id="e2c39-113">Протестируйте изменения:</span><span class="sxs-lookup"><span data-stu-id="e2c39-113">Test the changes:</span></span>

<span data-ttu-id="e2c39-114">В Visual Studio Code выберите **отладка > начать отладку** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="e2c39-114">Within Visual Studio Code, select **Debug > Start debugging** to run the application.</span></span>
<span data-ttu-id="e2c39-115">Перейдите по следующему URL-адресу: **http://localhost:5000/api/notifications**.</span><span class="sxs-lookup"><span data-stu-id="e2c39-115">Navigate to the following url: **http://localhost:5000/api/notifications**.</span></span> <span data-ttu-id="e2c39-116">При этом будет зарегистрирована новая подписка.</span><span class="sxs-lookup"><span data-stu-id="e2c39-116">This will register a new subscription.</span></span>

<span data-ttu-id="e2c39-117">В окне **консоли отладки** кода Visual Studio приблизительно каждые 15 секунд Обратите внимание на то, что время ожидания подписки проверяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e2c39-117">In the Visual Studio Code **Debug Console** window, approximately every 15 seconds, notice the timer checking the subscription for expiration:</span></span>

```shell
Checking subscriptions 12:32:51.882
Current subscription count 1
```

<span data-ttu-id="e2c39-118">Подождите несколько минут, и при необходимости обновите подписку, вы увидите следующее:</span><span class="sxs-lookup"><span data-stu-id="e2c39-118">Wait a few minutes and you will see the following when the subscription needs renewing:</span></span>

```shell
Renewed subscription: 07ca62cd-1a1b-453c-be7b-4d196b3c6b5b, New Expiration: 3/10/2019 7:43:22 PM +00:00
```

<span data-ttu-id="e2c39-119">Это означает, что подписка обновлена и показывает новое время действия.</span><span class="sxs-lookup"><span data-stu-id="e2c39-119">This indicates that the subscription was renewed and shows the new expiry time.</span></span>