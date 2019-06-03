<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="cb0a6-101">Откройте командную строку, перейдите к каталогу, в котором у вас есть права на создание файлов, и выполните следующие команды, чтобы создать новое приложение .NET Core WebApi.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-101">Open your command prompt, navigate to a directory where you have rights to create files, and run the following commands to create a new .NET Core WebApi app.</span></span>

```shell
dotnet new webapi -o msgraphapp
```

<span data-ttu-id="cb0a6-102">После завершения выполнения команды выполните следующие команды, чтобы новый проект выполнялся правильно.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-102">Once the command finishes, run the following commands to ensure your new project runs correctly.</span></span>

```shell
cd msgraphapp
dotnet add package Microsoft.Identity.Client
dotnet add package Microsoft.Graph
dotnet run
```

<span data-ttu-id="cb0a6-103">Приложение запустится и выводится:</span><span class="sxs-lookup"><span data-stu-id="cb0a6-103">The application will start and output:</span></span>

```shell
Now listening on: http://localhost:5000
```

<span data-ttu-id="cb0a6-104">Если вы не видите этот результат или вы видите сообщение об ошибке, вероятно, проблема связана с [пакетом SDK .NET Core 2,2](https://dotnet.microsoft.com/download) , установленным на компьютере для разработки, который необходимо исправить перед продолжением работы.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-104">If you don't see this output, or you see error messages, there is likely a problem with the [.NET Core 2.2 SDK](https://dotnet.microsoft.com/download) installed on your development machine that needs to be fixed before continuing.</span></span>

<span data-ttu-id="cb0a6-105">Остановите работу приложения, нажав <kbd>CTRL</kbd>+<kbd>C</kbd>.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-105">Stop the application running by pressing <kbd>CTRL</kbd>+<kbd>C</kbd>.</span></span>

<span data-ttu-id="cb0a6-106">Откройте приложение в Visual Studio Code с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="cb0a6-106">Open the application in Visual Studio Code using the following command:</span></span>

```shell
code .
```

<span data-ttu-id="cb0a6-107">Когда откроется диалоговое окно, предлагающее добавить в проект необходимые ресурсы, нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-107">When a dialog box asks if you want to add required assets to the project, select **Yes**.</span></span>
