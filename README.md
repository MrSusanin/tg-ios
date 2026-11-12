# tg-vpn

Неофициальный клиент на базе открытого кода [Telegram-iOS](https://github.com/TelegramMessenger/Telegram-iOS)
со встроенным VPN-ядром (sing-box). Проект не связан с Telegram Messenger LLP.
Исходный код распространяется на условиях GPL, как и оригинал.

## Статус

- [x] Этап 0: сборка обычного Telegram в GitHub Actions (этот workflow)
- [ ] Этап 1: встроенное ядро sing-box и локальный прокси для Telegram
- [ ] Этап 2: парсер ссылок/подписок, страница с DNS и автопроверкой

## Как запустить сборку

1. На my.telegram.org получите `api_id` и `api_hash`.
2. В репозитории: Settings -> Secrets and variables -> Actions -> New repository secret.
   Создайте два секрета:
   - `TG_API_ID`
   - `TG_API_HASH`
3. Вкладка Actions -> `Build IPA (stage 0 - plain Telegram)` -> Run workflow.
4. Сборка идёт долго (от 1 часа). Если упала, откройте последний шаг с красным крестиком
   и скопируйте последние 50-100 строк лога.
5. После успеха внизу страницы запуска, в разделе Artifacts, появится `telegram-ipa`.
   Внутри два файла:
   - `Telegram-noext.ipa` - без расширений, его ставьте с бесплатным Apple ID
   - `Telegram-full.ipa` - полный, для платного аккаунта

`api_hash` нигде не хранится в файлах репозитория, только в Secrets.

## Установка на iPhone с Windows (бесплатный Apple ID)

Вариант A: Sideloadly
1. Установите iTunes с сайта apple.com (не из Microsoft Store).
2. Установите Sideloadly с sideloadly.io.
3. Подключите iPhone кабелем, перетащите `Telegram-noext.ipa` в Sideloadly,
   введите Apple ID и нажмите Start.
4. На iPhone: Настройки -> Конфиденциальность и безопасность -> Режим разработчика (включить, перезагрузка).
5. Настройки -> Основные -> VPN и управление устройством -> доверять своему Apple ID.

Вариант B: AltStore. Нужны iTunes и iCloud с сайта apple.com, затем AltServer для Windows.
Он умеет переподписывать приложение сам, пока компьютер включён и в одной сети с телефоном.

Ограничения бесплатного аккаунта: подпись действует 7 дней, потом приложение нужно
переподписать; одновременно можно держать 3 приложения; push-уведомления не работают.
