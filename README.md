## Настройка CD 

На предыдущем этапе вы создалии пайплайн для сборки чартов и деплоя, надеюсь вы не забыли записать себе значения `CI_API_V4_URL`, `CI_PROJECT_ID` и `CHART_PROJECT_TRIGGER_TOKEN`. На этом этапе мы создадим пайплайн для сборки приложения (CI).

1. Добавьте в секреты gitlab'a необходимые значения:
|Ключ|Значение|Пояснение|
|--- |---     |---      |
|"CHART_PROJECT_API_V4_URL"|<CI_API_V4_URL>|значение из предыдущего шага|
|"CHART_PROJECT_ID"|<CI_PROJECT_ID>|значение из предыдущего шага|
|"CHART_PROJECT_TRIGGER_TOKEN"|<CHART_PROJECT_TRIGGER_TOKEN>|значение из предыдущего шага|
|"SONAR_LOGIN"|| логин от sonar|
|"SONARQUBE_URL"|****||
|"SONAR_TOKEN"||получите токен на странице https://sonarqube.*****.ru/account/security/ |

2. На этом этапе CI/CD полностью настроены. После успешной сборки кода, будет триггерится пайплайн для деплоя чарта с новой версией бекенда или фронтенда. Deployment настроен ручным образом, для его запуска в репозитории с чартами перейдите на вкладку pipelines и запустите последний пайплайн с тегом 'trigger token':
![alt text](image-1.png)

3. Следуйте дальнейшим указаниям, которые найдёте в конце логов job с названием 'deploy' в репозитории с чартами.


# Momo Store aka Пельменная №2

<img width="900" alt="image" src="https://user-images.githubusercontent.com/9394918/167876466-2c530828-d658-4efe-9064-825626cc6db5.png">

## Frontend

```bash
npm install
NODE_ENV=production VUE_APP_API_URL=http://localhost:8081 npm run serve
```

## Backend

```bash
go run ./cmd/api
go test -v ./... 
```

## code quality 

1. generate test coverage:
```bash
go test -coverprofile=coverage.out ./...
``` 
2. add sonarqube quality gate:
```bash
sonar-scanner -Dsonar.go.coverage.reportPaths=coverage.out -Dsonar.qualitygate.wait=true
```
