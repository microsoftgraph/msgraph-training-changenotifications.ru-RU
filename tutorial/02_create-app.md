<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="2145f-101">В этом упражнении вы создадите регистрацию нового веб-приложения Azure AD с помощью центра администрирования Azure Active Directory и выдасте согласие администратора для требуемых областей разрешений.</span><span class="sxs-lookup"><span data-stu-id="2145f-101">In this exercise, you will create a new Azure AD web application registration using the Azure Active Directory admin center and grant administrator consent to the required permission scopes.</span></span>

1. <span data-ttu-id="2145f-102">Откройте браузер и перейдите к [Центру администрирования Azure Active Directory](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2145f-102">Open a browser and navigate to the [Azure Active Directory admin center](https://portal.azure.com).</span></span> <span data-ttu-id="2145f-103">Войдите с помощью **рабочей или учебной учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="2145f-103">Login using a **Work or School Account**.</span></span>

1. <span data-ttu-id="2145f-104">Выберите **Azure Active Directory** на панели навигации слева, затем выберите **Регистрация приложения (предварительная версия)** в разделе **Управление**.</span><span class="sxs-lookup"><span data-stu-id="2145f-104">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations (Preview)** under **Manage**.</span></span>

    ![<span data-ttu-id="2145f-105">Снимок экрана с регистрациями приложений</span><span class="sxs-lookup"><span data-stu-id="2145f-105">A screenshot of the App registrations</span></span> ](./images/01.png)

1. <span data-ttu-id="2145f-106">Выберите **Новая регистрация**.</span><span class="sxs-lookup"><span data-stu-id="2145f-106">Select **New registration**.</span></span> <span data-ttu-id="2145f-107">На странице**Зарегистрировать приложение** задайте необходимые значения следующим образом.</span><span class="sxs-lookup"><span data-stu-id="2145f-107">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="2145f-108">Введите **имя** `GraphNotificationTutorial`.</span><span class="sxs-lookup"><span data-stu-id="2145f-108">Set **Name** to `GraphNotificationTutorial`.</span></span>
    - <span data-ttu-id="2145f-109">Введите **поддерживаемые типы учетных записей** для **учетных записей в любом каталоге организаций и личных учетных записей Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="2145f-109">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="2145f-110">В разделе **URI адрес перенаправления** введите значение в первом раскрывающемся списке `Web` и задайте значение `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="2145f-110">Under **Redirect URI**, set the first drop-down to `Web` and set the value to `http://localhost`.</span></span>

    ![Снимок страницы "регистрация приложения"](./images/02.png)

1. <span data-ttu-id="2145f-112">Выберите **регистр**.</span><span class="sxs-lookup"><span data-stu-id="2145f-112">Select **Register**.</span></span> <span data-ttu-id="2145f-113">На странице **графнотификатионтуториал** скопируйте значение ID **Application (Client) ID** и **Directory (Client) ID (идентификатор клиента)** , чтобы они потребуются на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="2145f-113">On the **GraphNotificationTutorial** page, copy the value of the **Application (client) ID** and **Directory (tenant) ID** save it, you will need them in the next step.</span></span>

    ![Снимок экрана с ИДЕНТИФИКАТОРом приложения для новой регистрации приложения](./images/03.png)

1. <span data-ttu-id="2145f-115">Выберите **Сертификаты и секреты** в разделе **Управление**.</span><span class="sxs-lookup"><span data-stu-id="2145f-115">Select **Certificates & secrets** under **Manage**.</span></span> <span data-ttu-id="2145f-116">Выберите **новый секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="2145f-116">Select **New client secret**.</span></span> <span data-ttu-id="2145f-117">Введите значение в поле **Описание** и выберите один из вариантов истечения **срока действия** , а затем нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="2145f-117">Enter a value in **Description** and select one of the options for **Expires** and select **Add**.</span></span>

    ![Снимок экрана: диалоговое окно добавления секрета клиента](./images/04.png)

1. <span data-ttu-id="2145f-119">Скопируйте значение секрета клиента, а затем покиньте эту страницу.</span><span class="sxs-lookup"><span data-stu-id="2145f-119">Copy the client secret value before you leave this page.</span></span> <span data-ttu-id="2145f-120">Оно вам понадобится на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="2145f-120">You will need it in the next step.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2145f-121">Это секрет клиента, он никогда не отображается еще раз, поэтому убедитесь, что вы скопировали его.</span><span class="sxs-lookup"><span data-stu-id="2145f-121">This client secret is never shown again, so make sure you copy it now.</span></span>

    ![Снимок экрана с недавно добавленным секретом клиента](./images/05.png)

1. <span data-ttu-id="2145f-123">Выберите **разрешения API** в разделе **Управление**.</span><span class="sxs-lookup"><span data-stu-id="2145f-123">Select **API Permissions** under **Manage**.</span></span> <span data-ttu-id="2145f-124">**Добавьте разрешение** и выберите **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="2145f-124">**Add a permission** and select **Microsoft Graph**.</span></span> <span data-ttu-id="2145f-125">Выберите **разрешение приложения** и разверните элемент **пользователь** и выберите область **User. ReadWrite. ALL** .</span><span class="sxs-lookup"><span data-stu-id="2145f-125">Select **Application Permission** and expand **User** and select the **User.ReadWrite.All** scope.</span></span> <span data-ttu-id="2145f-126">Нажмите кнопку **Добавить разрешения** , чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="2145f-126">Select **Add permissions** to save your changes.</span></span>

    ![Снимок экрана с недавно добавленным секретом клиента](./images/06.png)

<span data-ttu-id="2145f-128">Приложение запрашивает разрешение приложения с областью **User. ReadWrite. ALL** .</span><span class="sxs-lookup"><span data-stu-id="2145f-128">The application requests an application permission with the **User.ReadWrite.All** scope.</span></span> <span data-ttu-id="2145f-129">Для этого разрешения требуется согласие администратора.</span><span class="sxs-lookup"><span data-stu-id="2145f-129">This permission requires administrative consent.</span></span>

<span data-ttu-id="2145f-130">Выберите параметр **предоставить согласие администратора для Contoso** , а затем выберите **Да** , чтобы согласиться с этим приложением и предоставить приложению доступ к клиенту с помощью указанных областей.</span><span class="sxs-lookup"><span data-stu-id="2145f-130">Select **Grant admin consent for Contoso** and then select **Yes** to consent this application and grant the application access to your tenant using the scopes you specified.</span></span>

![Снимок экрана входа](./images/07.png)
