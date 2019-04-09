# docker compose name resolution test lab

## scenario 1
Isolate docker compose from the same folder using `project-name` parameter

```
docker-compose -f docker-compose.yml build 
docker-compose -f docker-compose.1.yml build  

docker-compose -f docker-compose.yml --project-name first up  -d 
docker-compose -f docker-compose.1.yml --project-name second up -d 
```

Connect to the first machine and curl www.foo.com
```
docker exec -it first_base_1 sh 
curl www.foo.com
```

Connect to the second machine and curl www.foo.com, the results should be different
```
docker exec -it second_base_1 sh 
curl www.foo.com
```

## scenario 2
Isolate docker compose using separated folders

```
cd scenario-wihtout-project-name
cd third
docker-compose build 
docker-compose up  -d 

cd ../fourth
docker-compose build 
docker-compose up  -d 
```

Connect to the third machine and curl www.foo.com
```
docker exec -it third_base_1 sh 
curl www.foo.com
```

Connect to the fourth machine and curl www.foo.com, the results should be different
```
docker exec -it fourth_base_1 sh 
curl www.foo.com
```



## Notes

- If running minikube on mac make sure to run the experiment on the local docker
```eval $(docker-machine env -u)```
