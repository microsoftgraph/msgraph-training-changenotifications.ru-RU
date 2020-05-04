<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="a3964-101">В этом руководстве рассказывается, как создать основное приложение .NET, которое использует API Microsoft Graph для получения уведомлений (веб-перехватчиков) при изменении учетной записи пользователя в Azure Active Directory (Azure AD) и выполнении запросов с помощью API запросов Дельта для получения всех изменений учетных записей пользователей с момента последнего запроса.</span><span class="sxs-lookup"><span data-stu-id="a3964-101">This tutorial teaches you how to build a .NET Core app that uses the Microsoft Graph API to receive notifications (webhooks) when a user account changes in Azure Active Directory (Azure AD) and perform queries using the delta query API to receive all changes to user accounts since the last query was made.</span></span>

> [!TIP]
> <span data-ttu-id="a3964-102">Если вы предпочитаете просто скачать заполненный учебник, вы можете скачать или клонировать [репозиторий GitHub](https://github.com/microsoftgraph/msgraph-training-changenotifications).</span><span class="sxs-lookup"><span data-stu-id="a3964-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-changenotifications).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3964-103">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a3964-103">Prerequisites</span></span>

<span data-ttu-id="a3964-104">Прежде чем приступить к работе с этим руководством, на компьютере для разработки должен быть установлен [пакет SDK для .NET Core 2,2](https://dotnet.microsoft.com/download) и [Visual Studio Code](https://code.visualstudio.com/) .</span><span class="sxs-lookup"><span data-stu-id="a3964-104">Before you start this tutorial, you should have [.NET Core 2.2 SDK](https://dotnet.microsoft.com/download) and [Visual Studio Code](https://code.visualstudio.com/) installed on your development machine.</span></span>

> [!NOTE]
> <span data-ttu-id="a3964-105">Это руководство было написано с помощью .NET Core версии 2,2.</span><span class="sxs-lookup"><span data-stu-id="a3964-105">This tutorial was written with .NET Core version 2.2.</span></span> <span data-ttu-id="a3964-106">Действия, описанные в этом руководстве, могут работать с другими версиями, но не тестировались.</span><span class="sxs-lookup"><span data-stu-id="a3964-106">The steps in this guide may work with other versions, but that has not been tested.</span></span>

## <a name="watch-the-tutorial"></a><span data-ttu-id="a3964-107">Просмотр руководства</span><span class="sxs-lookup"><span data-stu-id="a3964-107">Watch the tutorial</span></span>

<span data-ttu-id="a3964-108">Этот модуль записан и доступен в канале разработки Office на YouTube.</span><span class="sxs-lookup"><span data-stu-id="a3964-108">This module has been recorded and is available in the Office Development YouTube channel.</span></span>

<!-- markdownlint-disable MD033 MD034 -->
<br/>

> [!VIDEO https://www.youtube-nocookie.com/embed/fThiCZmIcMQ]
<!-- markdownlint-enable MD033 MD034 -->

## <a name="feedback"></a><span data-ttu-id="a3964-109">Отзывы</span><span class="sxs-lookup"><span data-stu-id="a3964-109">Feedback</span></span>

<span data-ttu-id="a3964-110">Сообщите о нем в [репозиторий GitHub](https://github.com/microsoftgraph/msgraph-training-changenotifications).</span><span class="sxs-lookup"><span data-stu-id="a3964-110">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-changenotifications).</span></span>
