# <a name="using-change-notifications-and-track-changes-with-microsoft-graph"></a>Использование уведомлений об изменениях и отслеживание изменений с помощью Microsoft Graph

В этой лабораторной работе вы создадите консольное приложение .NET Core, которое получает уведомления об изменениях от Microsoft Graph при обновлении учетной записи пользователей в Azure Active Directory (Azure AD). Приложение будет управлять подпиской на уведомления об изменениях и использовать отслеживание изменений в Microsoft Graph, чтобы убедиться, что никакие изменения не пропускают.

## <a name="in-this-lab"></a>В этой лаборатории

1. [Общие сведения о лаборатории](./tutorial/01_intro.md)
1. [Регистрация и предоставление согласия приложения в Microsoft Graph](./tutorial/02_create-app.md)
1. [Установка ngrok](./tutorial/03_ngrok.md)
1. [Создание основного проекта .NET](./tutorial/04_create-project.md)
1. [Код API HTTP](./tutorial/05_add-code.md)
1. [Запуск приложения](./tutorial/06_run.md)
1. [Управление подписками на уведомления](./tutorial/07_subbscription-management.md)
1. [Запрос изменений](./tutorial/08_deltaquery.md)
1. [Завершенная Лаборатория](./tutorial/09_completed.md)

## <a name="prerequisites"></a>Необходимые условия

Прежде чем приступить к работе с этим руководством, на компьютере для разработки должен быть установлен [пакет SDK для .NET Core 2,2](https://dotnet.microsoft.com/download) и [Visual Studio Code](https://code.visualstudio.com/) . 

## <a name="completed-exercises"></a>Завершенные упражнения

Готовые решения представлены в папке [демонстрации](./Demos) , если вы повисает.