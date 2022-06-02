## Bugs or Errors to start react

## Error on npm start
You can have an error when initiliaze on linux a react project like:
```
...System limit for number of file watchers reached
```
You need to clean using the following command
```
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```