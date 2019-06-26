# <a name="using-change-notifications-and-track-changes-with-microsoft-graph"></a><span data-ttu-id="0d02e-101">Использование уведомлений об изменениях и отслеживание изменений с помощью Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="0d02e-101">Using Change Notifications and Track Changes with Microsoft Graph</span></span>

<span data-ttu-id="0d02e-102">В этой лабораторной работе вы создадите консольное приложение .NET Core, которое получает уведомления об изменениях от Microsoft Graph при обновлении учетной записи пользователей в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0d02e-102">In this lab you will create a .NET Core console application that receives change notifications from the Microsoft Graph when an update is made to a users account in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="0d02e-103">Приложение будет управлять подпиской на уведомления об изменениях и использовать отслеживание изменений в Microsoft Graph, чтобы убедиться, что никакие изменения не пропускают.</span><span class="sxs-lookup"><span data-stu-id="0d02e-103">The application will managed the Change Notification subscription and use Track Changes in the Microsoft Graph to ensure no changes are missed.</span></span>

## <a name="in-this-lab"></a><span data-ttu-id="0d02e-104">В этой лаборатории</span><span class="sxs-lookup"><span data-stu-id="0d02e-104">In this lab</span></span>

1. [<span data-ttu-id="0d02e-105">Общие сведения о лаборатории</span><span class="sxs-lookup"><span data-stu-id="0d02e-105">Introduction to the lab</span></span>](./tutorial/01_intro.md)
1. [<span data-ttu-id="0d02e-106">Регистрация и предоставление согласия приложения в Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="0d02e-106">Register and grant consent to the application in Microsoft Graph</span></span>](./tutorial/02_create-app.md)
1. [<span data-ttu-id="0d02e-107">Установка ngrok</span><span class="sxs-lookup"><span data-stu-id="0d02e-107">Install ngrok</span></span>](./tutorial/03_ngrok.md)
1. [<span data-ttu-id="0d02e-108">Создание основного проекта .NET</span><span class="sxs-lookup"><span data-stu-id="0d02e-108">Create the .NET Core project</span></span>](./tutorial/04_create-project.md)
1. [<span data-ttu-id="0d02e-109">Код API HTTP</span><span class="sxs-lookup"><span data-stu-id="0d02e-109">Code the HTTP API</span></span>](./tutorial/05_add-code.md)
1. [<span data-ttu-id="0d02e-110">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="0d02e-110">Run the application</span></span>](./tutorial/06_run.md)
1. [<span data-ttu-id="0d02e-111">Управление подписками на уведомления</span><span class="sxs-lookup"><span data-stu-id="0d02e-111">Manage notification subscriptions</span></span>](./tutorial/07_subbscription-management.md)
1. [<span data-ttu-id="0d02e-112">Запрос изменений</span><span class="sxs-lookup"><span data-stu-id="0d02e-112">Query for changes</span></span>](./tutorial/08_deltaquery.md)
1. [<span data-ttu-id="0d02e-113">Завершенная Лаборатория</span><span class="sxs-lookup"><span data-stu-id="0d02e-113">Completed Lab</span></span>](./tutorial/09_completed.md)

## <a name="prerequisites"></a><span data-ttu-id="0d02e-114">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="0d02e-114">Prerequisites</span></span>

<span data-ttu-id="0d02e-115">Прежде чем приступить к работе с этим руководством, на компьютере для разработки должен быть установлен [пакет SDK для .NET Core 2,2](https://dotnet.microsoft.com/download) и [Visual Studio Code](https://code.visualstudio.com/) .</span><span class="sxs-lookup"><span data-stu-id="0d02e-115">Before you start this tutorial, you should have [.NET Core 2.2 SDK](https://dotnet.microsoft.com/download) and [Visual Studio Code](https://code.visualstudio.com/) installed on your development machine.</span></span> 

## <a name="completed-exercises"></a><span data-ttu-id="0d02e-116">Завершенные упражнения</span><span class="sxs-lookup"><span data-stu-id="0d02e-116">Completed Exercises</span></span>

<span data-ttu-id="0d02e-117">Готовые решения представлены в папке [демонстрации](./Demos) , если вы повисает.</span><span class="sxs-lookup"><span data-stu-id="0d02e-117">Finished solutions are provided in the [Demos](./Demos) folder if you get stuck.</span></span>