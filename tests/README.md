#### Adding build breaker plugin to sonarqube 

  *  login to sonarqube server
```
docker exec -it sonarqube bash
```

  * Change into plugins dir and download the plugin 

```
cd extensions/plugins/

wget -c https://github.com/adnovum/sonar-build-breaker/releases/download/v2.3/sonar-build-breaker-plugin-2.3.jar

exit
```

  * Restart sonarqube 

```
docker restart sonarqube 
```



     
