<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="85228-101">Создайте конфигурацию запуска, чтобы отладить приложение в Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="85228-101">Create a launch configuration to debug the application in Visual Studio Code.</span></span>

<span data-ttu-id="85228-102">В Visual Studio Code выберите **отладка > открытых конфигураций**.</span><span class="sxs-lookup"><span data-stu-id="85228-102">Within Visual Studio Code, select **Debug > Open Configurations**.</span></span>

  ![Демонстрационные конфигурации запуска при открытии кода VS](./images/vscode-debugapp-01.png)

<span data-ttu-id="85228-104">Когда будет предложено выбрать среду, выберите пункт **.NET Core**.</span><span class="sxs-lookup"><span data-stu-id="85228-104">When prompted to select an environment, select **.NET Core**.</span></span>

  ![Демонстрационная программа VS Code, создающая конфигурацию запуска для ядра .NET](./images/vscode-debugapp-02.png)

> [!NOTE]
> <span data-ttu-id="85228-106">По умолчанию при запуске отладчика конфигурация запуска ядра .NET будет открывать браузер и переходить к URL-адресу по умолчанию для приложения.</span><span class="sxs-lookup"><span data-stu-id="85228-106">By default, the .NET Core launch configuration will open a browser and navigate to the default URL for the application when launching the debugger.</span></span> <span data-ttu-id="85228-107">Для этого приложения вместо этого мы хотим перейти по URL-адресу NGrok.</span><span class="sxs-lookup"><span data-stu-id="85228-107">For this application, we instead want to navigate to the NGrok URL.</span></span> <span data-ttu-id="85228-108">Если вы оставляете конфигурацию запуска как есть, при каждой отладке приложения будет отображаться сломанная страница.</span><span class="sxs-lookup"><span data-stu-id="85228-108">If you leave the launch configuration as is, each time you debug the application it will display a broken page.</span></span> <span data-ttu-id="85228-109">Вы можете просто изменить URL-адрес или изменить конфигурацию запуска, чтобы не запустить браузер:</span><span class="sxs-lookup"><span data-stu-id="85228-109">You can just change the URL, or change the launch configuration to not launch the browser:</span></span>

<span data-ttu-id="85228-110">Обновите конфигурацию запуска отладчика Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="85228-110">Update the Visual Studio debugger launch configuration:</span></span>

  1. <span data-ttu-id="85228-111">В Visual Studio Code откройте файл file **. вскоде/Launch. JSON**.</span><span class="sxs-lookup"><span data-stu-id="85228-111">In Visual Studio Code, open the file **.vscode/launch.json**.</span></span>
  1. <span data-ttu-id="85228-112">В конфигурации по умолчанию откройте следующий раздел:</span><span class="sxs-lookup"><span data-stu-id="85228-112">Locate the following section in the default configuration:</span></span>

      ```json
      "launchBrowser": {
        "enabled": true
      },
      ```

  1. <span data-ttu-id="85228-113">Задайте для `enabled` `false`свойства значение.</span><span class="sxs-lookup"><span data-stu-id="85228-113">Set the `enabled` property to `false`.</span></span>
  1. <span data-ttu-id="85228-114">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="85228-114">Save your changes.</span></span>

### <a name="test-the-application"></a><span data-ttu-id="85228-115">Тестирование приложения:</span><span class="sxs-lookup"><span data-stu-id="85228-115">Test the application:</span></span>

<span data-ttu-id="85228-116">В Visual Studio Code выберите **отладка > начать отладку** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="85228-116">In Visual Studio Code, select **Debug > Start debugging** to run the application.</span></span> <span data-ttu-id="85228-117">Код VS создает приложение и создает звезду.</span><span class="sxs-lookup"><span data-stu-id="85228-117">VS Code will build and star the application.</span></span>

<span data-ttu-id="85228-118">После последующего отображения в окне **консоли отладки** ...</span><span class="sxs-lookup"><span data-stu-id="85228-118">Once you see the following in the **Debug Console** window...</span></span>

![Снимок экрана: консоль отладки кода VS](./images/vscode-debugapp-03.png)

<span data-ttu-id="85228-120">... Откройте браузер и перейдите **http://localhost:5000/api/notifications** в раздел, чтобы подписаться на уведомления об изменении.</span><span class="sxs-lookup"><span data-stu-id="85228-120">... open a browser and navigate to **http://localhost:5000/api/notifications** to subscribe to change notifications.</span></span> <span data-ttu-id="85228-121">При успешном выполнении вы увидите выходные данные, включающие идентификатор подписки, подобный показанному ниже:</span><span class="sxs-lookup"><span data-stu-id="85228-121">If successful you will see output that includes a subscription id like the one below:</span></span>

![Снимок экрана: успешная подписка](./images/vscode-debugapp-04.png)

<span data-ttu-id="85228-123">Теперь ваше приложение подписано на получение уведомлений от Microsoft Graph при обновлении пользователей в клиенте Office 365.</span><span class="sxs-lookup"><span data-stu-id="85228-123">Your application is now subscribed to receive notifications from the Microsoft Graph when an update is made on any users in the Office 365 tenant.</span></span>

<span data-ttu-id="85228-124">Инициация уведомления:</span><span class="sxs-lookup"><span data-stu-id="85228-124">Trigger a notification:</span></span>

1. <span data-ttu-id="85228-125">Откройте браузер и перейдите в [центр администрирования Microsoft 365 (https://admin.microsoft.com/AdminPortal)](https://admin.microsoft.com/AdminPortal).</span><span class="sxs-lookup"><span data-stu-id="85228-125">Open a browser and navigate to the [Microsoft 365 admin center (https://admin.microsoft.com/AdminPortal)](https://admin.microsoft.com/AdminPortal).</span></span>
1. <span data-ttu-id="85228-126">Если вам будет предложено войти, войдите с помощью учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="85228-126">If prompted to login, sign-in using an admin account.</span></span>
1. <span data-ttu-id="85228-127">Выберите **пользователи > активные пользователи**.</span><span class="sxs-lookup"><span data-stu-id="85228-127">Select **Users > Active users**.</span></span>

    ![Снимок экрана: центр администрирования Microsoft 365](./images/vscode-debugapp-05.png)

1. <span data-ttu-id="85228-129">Выберите активного пользователя и нажмите **изменить** для его **контактной информации**.</span><span class="sxs-lookup"><span data-stu-id="85228-129">Select an active user and select **Edit** for their **Contact information**.</span></span>

    ![Снимок экрана с подробными сведениями о пользователе](./images/vscode-debugapp-06.png)

1. <span data-ttu-id="85228-131">Обновите значение **номера телефона** , указав новое число и нажмите кнопку **сохранить**.</span><span class="sxs-lookup"><span data-stu-id="85228-131">Update the **Phone number** value with a new number and Select **Save**.</span></span>

    <span data-ttu-id="85228-132">В **консоли отладки**кода Visual Studio вы увидите, что уведомление получено.</span><span class="sxs-lookup"><span data-stu-id="85228-132">In the Visual Studio Code **Debug Console**, you will see a notification has been received.</span></span> <span data-ttu-id="85228-133">Иногда это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="85228-133">Sometimes this may take a few minutes to arrive.</span></span> <span data-ttu-id="85228-134">Ниже приведен пример выходных данных.</span><span class="sxs-lookup"><span data-stu-id="85228-134">An example of the output is below:</span></span>

    ```shell
    Received notification: 'Users/7a7fded6-0269-42c2-a0be-512d58da4463', 7a7fded6-0269-42c2-a0be-512d58da4463
    ```

<span data-ttu-id="85228-135">Это означает, что приложение успешно получало уведомление от Microsoft Graph для пользователя, указанного в выходных данных.</span><span class="sxs-lookup"><span data-stu-id="85228-135">This indicates the application successfully received the notification from the Microsoft Graph for the user specified in the output.</span></span> <span data-ttu-id="85228-136">Затем вы можете использовать эти сведения для получения подробных сведений о пользователях в Microsoft Graph, если вы хотите синхронизировать их с приложением.</span><span class="sxs-lookup"><span data-stu-id="85228-136">You can then use this information to query the Microsoft Graph for the users full details if you want to synchronize their details into your application.</span></span>