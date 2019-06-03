# <a name="microsoft-graph-training-module---using-change-notifications-and-track-changes-with-microsoft-graph"></a><span data-ttu-id="fddfd-101">Модуль обучения Microsoft Graph — использование уведомлений об изменениях и отслеживание изменений с помощью Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="fddfd-101">Microsoft Graph Training Module - Using Change Notifications and Track Changes with Microsoft Graph</span></span>

<span data-ttu-id="fddfd-102">В этом модуле вы узнаете, как работать с уведомлениями об изменениях (веб-перехватчиками) & отслеживать изменения (разностный запрос) в Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="fddfd-102">This module will introduce you to working with change notifications (webhooks) & track changes (delta query) in the Microsoft Graph.</span></span>

## <a name="lab---change-notifications-and-track-changes-with-the-microsoft-graph"></a><span data-ttu-id="fddfd-103">Lab — уведомления об изменениях и отслеживание изменений с помощью Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="fddfd-103">Lab - Change Notifications and Track Changes with the Microsoft Graph</span></span>

<span data-ttu-id="fddfd-104">В этой лабораторной работе вы создадите консольное приложение .NET Core, которое получает уведомления об изменениях от Microsoft Graph при обновлении учетной записи пользователей в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fddfd-104">In this lab you will create a .NET Core console application that receives change notifications from the Microsoft Graph when an update is made to a users account in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="fddfd-105">Приложение будет управлять подпиской на уведомления об изменениях и использовать отслеживание изменений в Microsoft Graph, чтобы убедиться, что никакие изменения не пропускают.</span><span class="sxs-lookup"><span data-stu-id="fddfd-105">The application will managed the Change Notification subscription and use Track Changes in the Microsoft Graph to ensure no changes are missed.</span></span>

- [<span data-ttu-id="fddfd-106">Руководство по лаборатории</span><span class="sxs-lookup"><span data-stu-id="fddfd-106">Lab Manual</span></span>](./Lab.md)

## <a name="demos"></a><span data-ttu-id="fddfd-107">Демонстрации</span><span class="sxs-lookup"><span data-stu-id="fddfd-107">Demos</span></span>

- [<span data-ttu-id="fddfd-108">Создание основного приложения .NET</span><span class="sxs-lookup"><span data-stu-id="fddfd-108">Create a .NET Core app</span></span>](./demos/01-create-application)
- [<span data-ttu-id="fddfd-109">Добавление жизненного цикла подписки</span><span class="sxs-lookup"><span data-stu-id="fddfd-109">Add Subscription Lifecycle</span></span>](./demos/02-subscription-management)
- [<span data-ttu-id="fddfd-110">Добавление изменений записей</span><span class="sxs-lookup"><span data-stu-id="fddfd-110">Add Track Changes</span></span>](./demos/03-track-changes)

## <a name="watch-the-module"></a><span data-ttu-id="fddfd-111">Просмотр модуля</span><span class="sxs-lookup"><span data-stu-id="fddfd-111">Watch the module</span></span>

<span data-ttu-id="fddfd-112">Этот модуль записан и доступен в канале разработки Office на YouTube: [изменение уведомлений и отслеживание изменений с помощью Microsoft Graph](https://youtu.be/MvJ15BHTdHA)</span><span class="sxs-lookup"><span data-stu-id="fddfd-112">This module has been recorded and is available in the Office Development YouTube channel: [Change Notifications and Track Changes with the Microsoft Graph](https://youtu.be/MvJ15BHTdHA)</span></span>

## <a name="contributors"></a><span data-ttu-id="fddfd-113">Авторы</span><span class="sxs-lookup"><span data-stu-id="fddfd-113">Contributors</span></span>

| <span data-ttu-id="fddfd-114">Роли</span><span class="sxs-lookup"><span data-stu-id="fddfd-114">Roles</span></span>                | <span data-ttu-id="fddfd-115">Authors (s)</span><span class="sxs-lookup"><span data-stu-id="fddfd-115">Author(s)</span></span>                                               |
| -------------------- | ------------------------------------------------------- |
| <span data-ttu-id="fddfd-116">Лабораторные руководства и слайды</span><span class="sxs-lookup"><span data-stu-id="fddfd-116">Lab Manuals / Slides</span></span> | <span data-ttu-id="fddfd-117">Эндрю Коннелл (Майкрософт MVP, Воитанос) @andrewconnell</span><span class="sxs-lookup"><span data-stu-id="fddfd-117">Andrew Connell (Microsoft MVP, Voitanos) @andrewconnell</span></span> |
| <span data-ttu-id="fddfd-118">Спонсор и поддержка</span><span class="sxs-lookup"><span data-stu-id="fddfd-118">Sponsor / Support</span></span>    | <span data-ttu-id="fddfd-119">Джереми саке (Майкрософт) @jthake</span><span class="sxs-lookup"><span data-stu-id="fddfd-119">Jeremy Thake (Microsoft) @jthake</span></span>                        |

## <a name="version-history"></a><span data-ttu-id="fddfd-120">Журнал версий</span><span class="sxs-lookup"><span data-stu-id="fddfd-120">Version history</span></span>

| <span data-ttu-id="fddfd-121">Версия</span><span class="sxs-lookup"><span data-stu-id="fddfd-121">Version</span></span> | <span data-ttu-id="fddfd-122">Дата</span><span class="sxs-lookup"><span data-stu-id="fddfd-122">Date</span></span>           | <span data-ttu-id="fddfd-123">Comments</span><span class="sxs-lookup"><span data-stu-id="fddfd-123">Comments</span></span>             |
| ------- | -------------- | -------------------- |
| <span data-ttu-id="fddfd-124">1.1</span><span class="sxs-lookup"><span data-stu-id="fddfd-124">1.1</span></span>     | <span data-ttu-id="fddfd-125">9 апреля 2019 г.</span><span class="sxs-lookup"><span data-stu-id="fddfd-125">April 9, 2019</span></span> | <span data-ttu-id="fddfd-126">Добавлена ссылка на презентацию</span><span class="sxs-lookup"><span data-stu-id="fddfd-126">Added screencast link</span></span> |
| <span data-ttu-id="fddfd-127">1.0</span><span class="sxs-lookup"><span data-stu-id="fddfd-127">1.0</span></span>     | <span data-ttu-id="fddfd-128">14 марта 2019 г.</span><span class="sxs-lookup"><span data-stu-id="fddfd-128">March 14, 2019</span></span> | <span data-ttu-id="fddfd-129">Новый модуль отправлен</span><span class="sxs-lookup"><span data-stu-id="fddfd-129">New module submitted</span></span> |

## <a name="disclaimer"></a><span data-ttu-id="fddfd-130">Заявление об отказе</span><span class="sxs-lookup"><span data-stu-id="fddfd-130">Disclaimer</span></span>

<span data-ttu-id="fddfd-131">**Этот код предоставляется без каких _-_ либо гарантий, явных или подразумеваемых, включая любые подразумеваемые гарантии пригодности для конкретной цели, пригодности к отдельному ОБЪЕМу или ненарушениям.**</span><span class="sxs-lookup"><span data-stu-id="fddfd-131">**THIS CODE IS PROVIDED _AS IS_ WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESS OR IMPLIED, INCLUDING ANY IMPLIED WARRANTIES OF FITNESS FOR A PARTICULAR PURPOSE, MERCHANTABILITY, OR NON-INFRINGEMENT.**</span></span>

<img src="https://telemetry.sharepointpnp.com/msgraph-training-changenotifications" />
