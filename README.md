<h2 align="center"> Проект по автоматизации тестирования для компании "Магнит Доставка" </h2>
<a href="https://rabota.sber.ru"><img src="./images/icons/logo.svg"></a>

# <a name="TableOfContents">Содержание</a>
+ [Описание](#Описание)
+ [Технологии и инструменты](#Технологии-и-инструменты)
+ [Варианты запуска](#Jenkins)
    + [Gradle command](#GradleCommand)
    + [Запуск в Jenkins](#RunInJenkins)
+ [Telegram уведомления](#TelegramNotifications)
+ [Результаты тестов в Allure Report](#AllureReport)
+ [Интеграция с Allure TestOps](#AllureTestOps)
+ [Интеграция с Jira](#Jira)
+ [Видео запуска тестов](#Video)


# <a name="Описание">Описание</a>
Тестовый проект состоит из веб-тестов (UI), тестов API и мобильных тестов (Android).\
Краткий список интересных фактов о проекте:
- [x] `Page Object` проектирование
- [x] Параметризованные тесты
- [x] Различные файлы конфигурации для запуска теста в зависимости от параметров сборки
- [x] Конфигурация с библиотекой `Owner`
- [x] Использование `Lombok` для моделей в API тестах
- [x] Objects serialization/deserialization for API requests/responses using `Jackson`
- [x] Использование request/response спецификаций для API тестов
- [x] Custom Allure listener для API requests/responses логов
- [x] Интеграция с `Allure TestOps`
- [x] Autotests as test documentation
- [x] Интеграция с `Jira`


# <a name="Технологии и инструменты">Технологии и инструменты</a>
<p  align="center">
  <code><img width="5%" title="IntelliJ IDEA" src="./images/icons/IDEA-logo.svg"></code>
  <code><img width="5%" title="Java" src="./images/icons/java-logo.svg"></code>
  <code><img width="5%" title="Selenide" src="./images/icons/selenide-logo.svg"></code>
  <code><img width="5%" title="REST-Assured" src="./images/icons/rest-assured-logo.svg"></code>
  <code><img width="5%" title="Selenoid" src="./images/icons/selenoid-logo.svg"></code>
  <code><img width="5%" title="Gradle" src="./images/icons/gradle-logo.svg"></code>
  <code><img width="5%" title="JUnit5" src="./images/icons/junit5-logo.svg"></code>
  <code><img width="5%" title="Allure Report" src="./images/icons/allure-Report-logo.svg"></code>
  <code><img width="5%" title="Allure TestOps" src="./images/icons/allure-ee-logo.svg"></code>
  <code><img width="5%" title="Github" src="./images/icons/git-logo.svg"></code>
  <code><img width="5%" title="Jenkins" src="./images/icons/jenkins-logo.svg"></code>
  <code><img width="5%" title="Jira" src="./images/icons/jira-logo.svg"></code>
  <code><img width="5%" title="Telegram" src="./images/icons/Telegram.svg"></code>
  <code><img width="5%" title="Browserstack" src="./images/icons/browserstack.svg"></code>
  <code><img width="5%" title="Android Studio" src="https://upload.wikimedia.org/wikipedia/commons/9/95/Android_Studio_Icon_3.6.svg"></code>
  <code><img width="5%" title="Appium" src="./images/icons/appium.svg"></code>
</p>

Автотесты в этом проекте написаны на `Java` использую `Selenide` фреймворк.\
`Gradle` - используется как инструмент автоматизации сборки.  \
`JUnit5` - для выполнения тестов.\
`REST Assured` - для тестирования REST-API сервисов.\
`Jenkins` - CI/CD для запуска тестов удаленно.\
`Selenoid` - для удаленного запуска браузера в `Docker` контейнерах.\
`Browserstack` - для запуска мобильных тестов удаленно.\
`Android Studio tools`, `Appium` - для запуска мобильных тестов локально на эмуляторе мобильных устройств.\
`Allure Report` - для визуализации результатов тестирования.\
`Telegram Bot` - для уведомлений о результатах тестирования.\
`Allure TestOps` - как система управления тестированием.

[Вернуться к оглавлению ⬆](#TableOfContents)

# <a name="HowToRun">How to run</a>

## <a name="GradleCommand">Gradle command</a>
To run locally and in Jenkins the following command is used:
```bash
gradle clean test -Dtag=<tag> -DrunIn=<runIn>
```
Additional parameters:
> `-Dselenoid_user_sys_prop=enter_user` `-Dselenoid_key_sys_prop=enter_key` - credentials for selenoid\
> `-Dbrowserstack_user_sys_prop=enter_user` `-Dbrowserstack_key_sys_prop=enter_key` - credentials for browserstack\
> `-Dthreads=number_of_threads` can be added for parallel tests execution\
> `-DapiBaseUrl=url` can be added to set a base url for API tests

`tag` - tests with this tag will be executed:
>- *API*
>- *Web*
>- *Android*
 
`runIn` - defines an environment for running these tests:
>- *\<not defined\>(for API tests)*
>- *browser_selenoid*
>- *browser_local*
>- *android_browserstack*
>- *android_emulator*
>- *android_real*
>- *android_selenoid*

Additional properties are retrieved from the corresponding properties file(depending on `runIn` value):
```bash
./resources/config/project-${runIn}.properties
```

Valid combinations:
```mermaid
graph LR
A[tag] --> B[API]
A --> C[Web]
A --> D[Android]
C --> E[browser_selenoid]
C --> F[browser_local]
D --> G[android_browserstack]
D --> H[android_emulator]
```

[Вернуться к оглавлению ⬆](#TableOfContents)
