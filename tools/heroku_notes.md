## Heroku Commands

### Deploy steps
Before the deployment you must upload all your changes to the main or master branch
#### 1. Login to Heroku
```bash
heroku login -i
```
#### 2. Push with Heroku
```bash
git push heroku main
```

If you want to track the logs on the heroku server use the following command:
```
heroku logs --tail
```

#### Heroku errors

## Fix to wrong app git remote
Change the herokuApp with your name app
```
heroku git:remote -a herokuAppName
git push heroku master
```
