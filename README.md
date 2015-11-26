# Apt-Cacher NG

[https://www.unix-ag.uni-kl.de/~bloch/acng/](https://www.unix-ag.uni-kl.de/~bloch/acng/)

Manual build:
```sh
docker build -t apt-cacher-ng -f Dockerfile .
docker run -d --cap-drop=all --name apt-cacher-ng -p 3142:3142 apt-cacher-ng VerboseLog=1 Debug=7 ForeGround=1 PassThroughPattern=.*
http://DOCKERCONTAINERIP:3142/acng-report.html
```

Autobuild:
```
docker run -d --restart=always --cap-drop=all --name apt-cacher-ng -p 3142:3142 konstruktoid/apt-cacher-ng VerboseLog=1 Debug=7 ForeGround=1 PassThroughPattern=.*
```

/etc/apt/apt.conf.d/01proxy:
```sh
Acquire::http::Proxy "http://DOCKERCONTAINERIP:3142";
Acquire::https::Proxy "http://DOCKERCONTAINERIP:3142";
```

`./apparmor/` contains apparmor profile and toml file, `--security-opt="apparmor:docker-aptcacherng"`  
`docker run -d --security-opt="apparmor:docker-aptcacherng" --name apt-cacher-ng -p 3142:3142 apt-cacher-ng VerboseLog=1 Debug=7 ForeGround=1 PassThroughPattern=.*`
