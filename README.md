# mitxpro-theme
An open edX theme for MIT xPRO 

##Table of contents:
1. Configure Open edX
2. Configuring MIT xPRO theme


###1. Configure Open edX
Following steps are inspired by https://github.com/edx/devstack

####Clone edx/devstack

```
$ git clone https://github.com/edx/devstack
$ cd devstack
$ make requirements
$ export OPENEDX_RELEASE=hawthorn.master
$ make dev.clone
```

####Clone and checkout edx-platform.
```
$ git clone https://github.com/mitodl/edx-platform
$ git checkout xpro/ironwood
```

#### Pull latest images and run provision

```
$ make pull
$ make dev.provision 
```

####Common issues:
If you get issue while gettings any particular repo/images. You can simply try downloading our relevant images. 

```docker-compose pull lms studio```

As we don't need ecommerce, registerar etc. I believe we only need following IDAs, may be even less than these.

1. edx.devstack.elasticsearch
2. edx.devstack.chrome
3. edx.devstack.memcached
4. edx.devstack.firefox
5. edx.devstack.mongo
5. edx.devstack.devpi
6. edx.devstack.mysql
8. edx.devstack.studio
9. edx.devstack.discovery

If you get issues while running provision. You can try following 

```make dev.provision.run```

It will ignore the pull command and don't try to download missing images. You can even run provision for particular services e.g

```./provision-lms.sh```
