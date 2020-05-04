<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="e9465-101">Откройте командную строку, перейдите к каталогу, в котором у вас есть права на создание проекта, и выполните следующую команду, чтобы создать новое приложение .NET Core WebApi:</span><span class="sxs-lookup"><span data-stu-id="e9465-101">Open your command prompt, navigate to a directory where you have rights to create your project, and run the following command to create a new .NET Core WebApi app:</span></span>

```shell
dotnet new webapi -o msgraphapp
```

<span data-ttu-id="e9465-102">После создания приложения выполните следующие команды, чтобы новый проект выполнялся правильно.</span><span class="sxs-lookup"><span data-stu-id="e9465-102">After creating the application, run the following commands to ensure your new project runs correctly.</span></span>

  ```shell
  cd msgraphapp
  dotnet add package Microsoft.Identity.Client
  dotnet add package Microsoft.Graph
  dotnet run
  ```

  <span data-ttu-id="e9465-103">Приложение запустится и выведет следующие данные:</span><span class="sxs-lookup"><span data-stu-id="e9465-103">The application will start and output the following:</span></span>

  ```shell
  info: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[0] ...
  info: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[58] ...
  warn: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[35] ...
  info: Microsoft.AspNetCore.DataProtection.Repositories.FileSystemXmlRepository[39] ...
  Hosting environment: Development
  Content root path: /Users/ac/_play/graphchangenotifications/msgraphapp
  Now listening on: https://localhost:5001
  Now listening on: http://localhost:5000
  Application started. Press Ctrl+C to shut down.
  ```

<span data-ttu-id="e9465-104">Остановите работу приложения, нажав <kbd>CTRL</kbd>+<kbd>C</kbd>.</span><span class="sxs-lookup"><span data-stu-id="e9465-104">Stop the application running by pressing <kbd>CTRL</kbd>+<kbd>C</kbd>.</span></span>

<span data-ttu-id="e9465-105">Откройте приложение в Visual Studio Code с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="e9465-105">Open the application in Visual Studio Code using the following command:</span></span>

```shell
code .
```

<span data-ttu-id="e9465-106">Если в Visual Studio Code отображается диалоговое окно с вопросом о том, хотите ли вы добавить в проект необходимые ресурсы, нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="e9465-106">If Visual Studio code displays a dialog box asking if you want to add required assets to the project, select **Yes**.</span></span>
