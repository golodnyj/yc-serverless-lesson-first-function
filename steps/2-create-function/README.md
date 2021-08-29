# Создание Функции
## Создание функции

Создайте свою первую функцию с именем `my-first-function`: 

    yc serverless function create --name my-first-function

При создании функции вы получите URL по которому можно будет сделать вызов функции `http_invoke_url`. По умолчанию функция будет не публичной.

## Загрузка кода

Находясь в директории с файлом `index.py` вызовите следующую команду, это позволит вам загрузите код функции в облако и создать ее версию:

    yc serverless function version create \
    --function-name my-first-function          \
    --memory 256m                     \
    --execution-timeout 5s            \
    --runtime python37                \
    --entrypoint index.handler     \
    --service-account-id $SERVICE_ACCOUNT_ID     \
    --source-path index.py

Успешное выполнение команды приведет к созданию версии функции.

## Вызов функции

Получите список функций и получите информацию о функции `my-first-function`:

    yc serverless function list
    yc serverless function version list --function-name my-first-function

В результате вызова последней команды в столбце `FUNCTION ID` вы узнаете идентификатор функции и сможете сделать вызов функции с помощью следующей команды:

    yc serverless function invoke <идентификатор функции>

По умолчанию функция создается не публичной. Чтобы сделать функцию `my-first-function` публичной, вызовете следующую команду: 
    
    yc serverless function allow-unauthenticated-invoke my-first-function

После этого вы можете сделать ее вызов в браузере. Получите параметр `http_invoke_url` для функции `my-first-function`

    yc serverless function get my-first-function

Введите значение параметра `http_invoke_url` в браузере и наслаждайтесь вызовом вашей функции. 