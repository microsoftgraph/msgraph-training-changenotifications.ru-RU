<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="6175d-101">В этом упражнении вы создадите регистрацию нового веб-приложения Azure AD с помощью центра администрирования Azure Active Directory и выдасте согласие администратора для требуемых областей разрешений.</span><span class="sxs-lookup"><span data-stu-id="6175d-101">In this exercise, you will create a new Azure AD web application registration using the Azure Active Directory admin center and grant administrator consent to the required permission scopes.</span></span>

1. <span data-ttu-id="6175d-102">Откройте браузер и перейдите в [центр администрирования Azure Active Directory (https://aad.portal.azure.com)](https://aad.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6175d-102">Open a browser and navigate to the [Azure Active Directory admin center (https://aad.portal.azure.com)](https://aad.portal.azure.com).</span></span> <span data-ttu-id="6175d-103">Войдите с помощью **рабочей или учебной учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="6175d-103">Login using a **Work or School Account**.</span></span>

1. <span data-ttu-id="6175d-104">Выберите **Azure Active Directory** в левой панели навигации, а затем выберите **Регистрация приложений** в разделе **Управление**.</span><span class="sxs-lookup"><span data-stu-id="6175d-104">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![Снимок экрана с регистрациями приложений](./images/aad-portal-home.png)

1. <span data-ttu-id="6175d-106">Выберите **Новая регистрация**.</span><span class="sxs-lookup"><span data-stu-id="6175d-106">Select **New registration**.</span></span> <span data-ttu-id="6175d-107">На странице **Регистрация приложения**</span><span class="sxs-lookup"><span data-stu-id="6175d-107">On the **Register an application** page</span></span>

    ![Снимок экрана: страница "Регистрация приложений"](./images/aad-portal-newapp.png)

    <span data-ttu-id="6175d-109">Задайте значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6175d-109">Set the values as follows:</span></span>

    - <span data-ttu-id="6175d-110">**Name**: графнотификатионтуториал</span><span class="sxs-lookup"><span data-stu-id="6175d-110">**Name**: GraphNotificationTutorial</span></span>
    - <span data-ttu-id="6175d-111">**Поддерживаемые типы учетных**записей: учетные записи в любых организациях и личных учетных записях Майкрософт</span><span class="sxs-lookup"><span data-stu-id="6175d-111">**Supported account types**: Accounts in any organizational directory and personal Microsoft accounts</span></span>
    - <span data-ttu-id="6175d-112">**URI перенаправления**: веб->http://localhost</span><span class="sxs-lookup"><span data-stu-id="6175d-112">**Redirect URI**: Web > http://localhost</span></span>

    ![Снимок страницы "регистрация приложения"](./images/aad-portal-newapp-01.png)

    <span data-ttu-id="6175d-114">Выберите **регистр**.</span><span class="sxs-lookup"><span data-stu-id="6175d-114">Select **Register**.</span></span>

1. <span data-ttu-id="6175d-115">На странице **графнотификатионтуториал** скопируйте значение ID **Application (Client) ID** и **Directory (Client) ID (идентификатор клиента)** , чтобы они потребуются на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="6175d-115">On the **GraphNotificationTutorial** page, copy the value of the **Application (client) ID** and **Directory (tenant) ID** save it, you will need them in the next step.</span></span>

    ![Снимок экрана с ИДЕНТИФИКАТОРом приложения для новой регистрации приложения](./images/aad-portal-newapp-details.png)

1. <span data-ttu-id="6175d-117">Выберите **Управление сертификатами > & секреты**.</span><span class="sxs-lookup"><span data-stu-id="6175d-117">Select **Manage > Certificates & secrets**.</span></span> 

    <span data-ttu-id="6175d-118">Выберите **новый секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="6175d-118">Select **New client secret**.</span></span>

    <span data-ttu-id="6175d-119">Введите значение в поле **Описание** и выберите один из вариантов истечения **срока действия** , а затем нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="6175d-119">Enter a value in **Description** and select one of the options for **Expires** and select **Add**.</span></span>

    ![Снимок экрана: диалоговое окно добавления секрета клиента](./images/aad-portal-newapp-secret.png)

    ![Снимок экрана: диалоговое окно добавления секрета клиента](./images/aad-portal-newapp-secret-02.png)

1. <span data-ttu-id="6175d-122">Скопируйте значение секрета клиента, а затем покиньте эту страницу.</span><span class="sxs-lookup"><span data-stu-id="6175d-122">Copy the client secret value before you leave this page.</span></span> <span data-ttu-id="6175d-123">Оно вам понадобится на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="6175d-123">You will need it in the next step.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6175d-124">Это секрет клиента, он никогда не отображается еще раз, поэтому убедитесь, что вы скопировали его.</span><span class="sxs-lookup"><span data-stu-id="6175d-124">This client secret is never shown again, so make sure you copy it now.</span></span>

    ![Снимок экрана с недавно добавленным секретом клиента](./images/aad-portal-newapp-secret-03.png)

1. <span data-ttu-id="6175d-126">Выберите **Управление Разрешениями > API**.</span><span class="sxs-lookup"><span data-stu-id="6175d-126">Select **Manage > API Permissions**.</span></span>

    <span data-ttu-id="6175d-127">Выберите **Добавить разрешение** и выберите **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="6175d-127">Select **Add a permission** and select **Microsoft Graph**.</span></span>

    ![Снимок экрана: Выбор службы Microsoft Graph](./images/aad-portal-newapp-graphscope.png)

    <span data-ttu-id="6175d-129">Выберите **разрешение приложения**, разверните группу **пользователей** и выберите **User. ReadWrite. ALL** .</span><span class="sxs-lookup"><span data-stu-id="6175d-129">Select **Application Permission**, expand the **User** group and select **User.ReadWrite.All** scope.</span></span>

    <span data-ttu-id="6175d-130">Нажмите кнопку **Добавить разрешения** , чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="6175d-130">Select **Add permissions** to save your changes.</span></span>

    ![Снимок экрана: выбор области действия Microsoft Graph](./images/aad-portal-newapp-graphscope-02.png)

    ![Снимок экрана с недавно добавленным секретом клиента](./images/aad-portal-newapp-graphscope-03.png)

<span data-ttu-id="6175d-133">Приложение запрашивает разрешение приложения с областью **User. ReadWrite. ALL** .</span><span class="sxs-lookup"><span data-stu-id="6175d-133">The application requests an application permission with the **User.ReadWrite.All** scope.</span></span> <span data-ttu-id="6175d-134">Для этого разрешения требуется согласие администратора.</span><span class="sxs-lookup"><span data-stu-id="6175d-134">This permission requires administrative consent.</span></span>

<span data-ttu-id="6175d-135">Выберите параметр **предоставить согласие администратора для Contoso**, а затем выберите **Да** , чтобы согласиться с этим приложением и предоставить приложению доступ к клиенту с помощью указанных областей.</span><span class="sxs-lookup"><span data-stu-id="6175d-135">Select **Grant admin consent for Contoso**, then select **Yes** to consent this application and grant the application access to your tenant using the scopes you specified.</span></span>

![Согласие администратора с утвержденным администратором](./images/aad-portal-newapp-graphscope-04.png)
