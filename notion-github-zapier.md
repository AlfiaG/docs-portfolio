# Настройка интеграции Notion и GitHub с помощью Zapier

## Подробнее о Zapier

[Zapier](https://zapier.com/app/dashboard) - это платформа, которая связывает различные приложения и автоматизирует повторяющиеся задачи в рамках рабочего процесса. Данный сервис позволяет настроить обмен данными между приложениями по заданной инструкции. **Триггер** (trigger), т.е. заданное событие в одном из связанных приложений, запускает **действие** (action), т.е. ожидаемое событие в другом связанном приложении. Путь, который данные пользователя проходят в рамках такого процесса, называется Zap. 

В зависимости от того, каким образом настроена интеграция, одно из приложений становится истоником события-триггера, а другое приложение (или ряд приложений, если данные проходят через несколько узлов в рамках интеграции) выполняет действие.  Zapier позволяет настроить интеграцию между системой управления знаниями [Notion](https://www.notion.so/) и сервисом для хранения кода [GitHub](https://github.com/), используя те возможности, которые предоставляют API этих платформ. 

Например, в Notion с помощью Zapier можно настроить один триггер - создание нового элемента в [базе данных](https://www.notion.so/Intro-to-databases-fd8cd2d212f74c50954c11086d85997e) - и два действия: создание нового элемента в базе данных и обновление уже существующего элемента. Кроме того, доступны два промежуточныx действия: поиск нужного элемента базы данных и поиск [страницы](https://www.notion.so/Create-a-new-page-6c3fe9aad94749099ea4bdfc072e5f97).

Если GitHub выбран источником события-триггера, таким событием могут послужить создание нового репозитория, ветки, пулреквеста, комита и др. Как приложение, выполняющее действие, GitHub дает возможность создавать или обновлять пулреквесты, issue, удалять ветки и др., а также выполнять промежуточные действия поиска по репозиториям, пулреквестам, пользователям, организациям и др.

Полный список [поддерживаемых возможностей](https://zapier.com/apps/notion/integrations/github#triggers-and-actions) представлен на странице интеграции.

Самый популярный в Zapier сценарий интеграции Notion и GitHub выглядит так: когда в определенную базу данных в Notion добавляется новый элемент, в соответствующем репозитории на GitHub автоматически создается новое issue.

![most popular Zap](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.1.png)

## Предварительная настройка

Чтобы зарегистрироваться в Zapier, нажмите на кнопку *Sign up* на [главной странице сайта](https://zapier.com/)

![Sign up](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.0.png)

Прежде чем начать настройку интеграции, создайте базу данных в Notion, из которой будут запускаться события-триггеры. Для этого нажмите на иконку *New page* в левом нижнем углу интерфейса Notion:

![New page](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.0.1.png)

Выберите *Table* в разделе *DATABASE*:

![Table](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.0.2.png)

Выберите *New database* в меню справа:

![New database](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.0.3.png)

Нажмите на +, чтобы создать дополнительный столбец *Issue body*, который будет отвечать за текст комментария к создаваемому issue:

![Issue body](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.0.4.png)

В поле *Type* для этого столбца выберите значение *Text*:

![Issue body](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.0.5.png)

В графу *Tags* вы можете добавить варианты ярлыков, которые будут отображаться как *Labels* в карточке issue на GitHub): 

![Labels](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.0.6.png)

## Настройка интеграции 

Чтобы настроить эту интеграцию, удостоверьтесь, что на [странице интеграции Notion и GitHub](https://zapier.com/apps/notion/integrations/github) в графе *When this happens...* выбрано **New Database Item**, а в графе *automatically do this!* выбрано **Create Issue** и нажмите на *Connect Notion + GitHub*:

![Connect Notion + GitHub](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.2.png)

На открывшейся странице выберите кнопку *Get started*:

![Get started](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.3.png)

Следующий шаг - подключение аккаунта Notion. Нажмите на *Connect*:

![ConnectN](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.4.png)

После переадресации на страницу предоставления доступа к Notion, ознакомьтесь с деталями доступа к своему аккаунту. Если вы согласны продолжить, нажмите на *Select pages*: 

![Select pages](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.5.png)

В открывшемся меню выберите созданную ранее базу данных и нажмите на *Allow access*:

![Allow access](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.6.png)

Вернитесь на предыдущую вкладку. После авторизации подключение аккаунта будет подтверждено зеленой галочкой. Чтобы продолжить, нажмите на *Next*:

![Next](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.7.png)

Подтвердите выбор базы данных, затем нажмите на *Next*:

![Next](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.8.png)

Далее подключите аккаунт GitHub к Zapier, нажав на *Connect*:

![Connect](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.9.png)

После переадресации на страницу авторизации в GitHub, ознакомьтесь с деталями предоставления доступа к своему аккаунту. Если вы согласны продолжить, нажмите на *Authorize zapier*: 

![Authorize zapier](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.10.png)

На [странице авторизации в GitHub](https://github.com/login/oauth/authorize) введите пароль от своего аккаунта:

![Password](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.11.png)

После авторизации подключение аккаунта будет подтверждено зеленой галочкой. Чтобы продолжить, нажмите на *Next*:

![NextN](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.12.png)

Выберите репозиторий, который необходимо подключить к интеграции, и нажмите на *Next*:

![Repo](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.13.png)

Открывшийся редактор интеграции не позволяет задавать значение *Labels* через столбец *Tags* в базе данных. Чтобы настроить эту функцию, перейдите в продвинутый режим редактирования, нажав на *See how the Zap editor can help you*:

![Zap editor](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.14.png)

Нажмите на кнопку *Use advanced mode* в открывшемся окне:

![Use advanced mode](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.15.png)

Откройте второй шаг интеграции (*Action*) и выберите *Set up action*:

![Set up action](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.16.png)

В графе *Title* по умолчанию выставлено значение **Title**, оставьте эту графу без изменений. В графе *Body* выберите значение **Issue body**:

![Action setup](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.17.png)

В графе *Labels* выберите меню *Custom*, затем выберите из списка значение *Tags*:

![Labels](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.18.png)

Нажмите на *Continue*. В открывшемся разделе *Test action* нажмите на *Test & continue*:

![Test & continue](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.19.png)

В вашем репозитории, подключенном к интеграции, должно появиться тестовое issue *Untitled Page*. Если это произошло, значит, интеграция подключена правильно. Нажмите на *Publish Zap*. В открывшемся окне выберите *Publish & Turn On*, чтобы включить созданную автоматизацию:

![Publish & Turn On](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.20.png)

Интеграция готова. Обратите внимание, что в таблицах Notion по умолчанию создаются три пустых строки. Когда вы заполняете эти три строки, интеграция не работает. Чтобы отправить issue в GitHub, создавайте новую строку с помощью кнопки *New* в правом верхнем углу таблицы или под уже созданными столбцами:

![New](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.21.png)

Чтобы протестировать автоматизацию самостоятельно, создайте новые элементы в подключенной базе данных. Они должны появиться в виде новых issue в вашем репозитории.

![test](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.22.png)

![test](https://raw.github.com/AlfiaG/docs-portfolio/blob/main/screenshots/image1.23.png)