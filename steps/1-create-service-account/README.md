# Service Account
## Создание

Создайте сервисный аккаунт с именем `service-account-for-cf`: 

    export SERVICE_ACCOUNT=$(yc iam service-account create --name service-account-for-cf \
    --description "service account for cloud functions" \
    --format json | jq -r .)

Проверьте текущий список сервисных аккаунтов:
     
    yc iam service-account list
    echo $SERVICE_ACCOUNT

После проверки запишите ID, созданного сервисного аккаунта, в переменную `SERVICE_ACCOUNT_ID`:

    echo "export SERVICE_ACCOUNT_ID=<ID>" >> ~/.bashrc && . ~/.bashrc 
    echo $SERVICE_ACCOUNT_ID

## Назначение роли сервисному аккаунту

Добавим вновь созданному сервисному аккаунту роль `editor`:

    echo "export FOLDER_ID=$(yc config get folder-id)" >> ~/.bashrc && . ~/.bashrc 
    echo $FOLDER_ID

    yc resource-manager folder add-access-binding $FOLDER_ID \
    --subject serviceAccount:$SERVICE_ACCOUNT_ID \
    --role editor