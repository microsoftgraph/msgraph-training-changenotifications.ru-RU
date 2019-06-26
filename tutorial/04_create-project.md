<!-- markdownlint-disable MD002 MD041 -->

Откройте командную строку, перейдите к каталогу, в котором у вас есть права на создание проекта, и выполните следующую команду, чтобы создать новое приложение .NET Core WebApi:

```shell
dotnet new webapi -o msgraphapp
```

После создания приложения выполните следующие команды, чтобы новый проект выполнялся правильно.

  ```shell
  cd msgraphapp
  dotnet add package Microsoft.Identity.Client
  dotnet add package Microsoft.Graph
  dotnet run
  ```

  Приложение запустится и выведет следующие данные:

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

Остановите работу приложения, нажав <kbd>CTRL</kbd>+<kbd>C</kbd>.

Откройте приложение в Visual Studio Code с помощью следующей команды:

```shell
code .
```

Если в Visual Studio Code отображается диалоговое окно с вопросом о том, хотите ли вы добавить в проект необходимые ресурсы, нажмите кнопку **Да**.
