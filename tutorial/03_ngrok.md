<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="b9c68-101">Чтобы Microsoft Graph мог отправлять уведомления в ваше приложение, работающее на вашем компьютере для разработки, необходимо использовать такие средства, как ngrok, для туннелирования вызовов из Интернета на компьютер для разработки.</span><span class="sxs-lookup"><span data-stu-id="b9c68-101">In order for the Microsoft Graph to send notifications to your application running on your development machine you need to use a tool such as ngrok to tunnel calls from the internet to your development machine.</span></span> <span data-ttu-id="b9c68-102">Ngrok позволяет перенаправлять вызовы из Интернета в ваше приложение, запущенное локально, без необходимости создавать правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="b9c68-102">Ngrok allows calls from the internet to be directed to your application running locally without needing to create firewall rules.</span></span>

<span data-ttu-id="b9c68-103">Прежде чем продолжить, необходимо установить [ngrok](https://ngrok.com) на компьютере для разработки.</span><span class="sxs-lookup"><span data-stu-id="b9c68-103">Before you continue you should have [ngrok](https://ngrok.com) installed on your development machine.</span></span> <span data-ttu-id="b9c68-104">Если у вас нет ngrok, посетите предыдущую ссылку для получения сведений о параметрах и инструкциях по загрузке.</span><span class="sxs-lookup"><span data-stu-id="b9c68-104">If you do not have ngrok, visit the previous link for download options and instructions.</span></span>

<span data-ttu-id="b9c68-105">Запустите ngrok, выполнив следующую команду из командной строки:</span><span class="sxs-lookup"><span data-stu-id="b9c68-105">Run ngrok by executing the following from the command line:</span></span>

```shell
ngrok http 5000
```

<span data-ttu-id="b9c68-106">Это приведет к запуску ngrok и попросит от внешнего URL-адреса ngrok на свой компьютер для разработки на порте 5000.</span><span class="sxs-lookup"><span data-stu-id="b9c68-106">This will start ngrok and will tunnel requests from an external ngrok url to your development machine on port 5000.</span></span>

<span data-ttu-id="b9c68-107">Скопируйте адрес для переадресации HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b9c68-107">Copy the https forwarding address.</span></span> <span data-ttu-id="b9c68-108">В приведенном ниже примере `https://787b8292.ngrok.io`.</span><span class="sxs-lookup"><span data-stu-id="b9c68-108">In the example below that would be `https://787b8292.ngrok.io`.</span></span> <span data-ttu-id="b9c68-109">Это будет необходимо позже.</span><span class="sxs-lookup"><span data-stu-id="b9c68-109">You will need this later.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b9c68-110">При каждом перезапуске ngrok будет создан новый адрес, и его необходимо будет скопировать повторно.</span><span class="sxs-lookup"><span data-stu-id="b9c68-110">Each time ngrok is restarted a new address will be generated and you will need to copy it again.</span></span>

```shell
ngrok by @inconshreveable

Session Status                online
Account                       ???? ???? (Plan: Free)
Version                       2.3.15
Region                        United States (us)
Web Interface                 http://127.0.0.1:4040
Forwarding                    http://787b8292.ngrok.io -> http://localhost:5000
Forwarding                    https://787b8292.ngrok.io -> http://localhost:5000

Connections                   ttl     opn     rt1     rt5     p50     p90
                              0       0       0.00    0.00    0.00    0.00
```
