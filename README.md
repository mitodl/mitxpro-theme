# mitxpro-theme
An open edX theme for MIT xPRO 

## Table of contents:
1. Configure Open edX
2. Configuring MIT xPRO theme


### 1. Configure Open edX

Following steps are inspired by [edx-devstack](https://github.com/edx/devstack).

#### Clone edx/devstack

```
$ git clone https://github.com/edx/devstack
$ cd devstack
$ make requirements
$ export OPENEDX_RELEASE=ironwood.master
$ make dev.clone
```

#### Clone and checkout edx-platform.
```
$ git clone https://github.com/mitodl/edx-platform
$ git checkout xpro/ironwood
```

#### Pull latest images and run provision

```
$ make pull
$ make dev.provision 
```

#### Common issues:
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


Once all are complete, run the following command to start Open edX

```$ make dev.up```

And run the following to stop it.

```$ make stop```


## 2. Configuring MIT xPRO theme

For detail about themeing, please see edx-docs [edx-docs](https://edx.readthedocs.io/projects/edx-installing-configuring-and-running/en/latest/configuration/changing_appearance/theming/overview_themes.html).

For the LMS, you edit `/edx/app/edxapp/lms.env.json` to set 

`"ENABLE_COMPREHENSIVE_THEMING": true`

For Studio, you edit `/edx/app/edxapp/cms.env.json` to set 

`"ENABLE_COMPREHENSIVE_THEMING": true`

For each Open edX component that you want to apply a theme to, add the absolute path of the themes directory to the `COMPREHENSIVE_THEME_DIRS` configuration property.
That path should be accessible to docker container. Easiast way is to put you theme in `edx-platform/themes`.

If you have you theme along with other themes at `edx-platform/themes/mitxpro-theme`, you have to add path as follows.

For Studio, add the path to `COMPREHENSIVE_THEME_DIRS` in `/edx/app/edxapp/cms.env.json`.

```
"COMPREHENSIVE_THEME_DIRS": [
    "/my-open-edx-themes/edx-platform"

],
```

For the LMS, add the path to `COMPREHENSIVE_THEME_DIRS` in `/edx/app/edxapp/lms.env.json`.

```
"COMPREHENSIVE_THEME_DIRS": [
    "/my-open-edx-themes/edx-platform"
],
```

Restart LMS and Studio

`docker-compose restart lms studio`

#### Structure of your theme

Use the following file structure:

```
edx-platform
    └──mitxpro-theme
                ├── cms
                └── lms
                    └── static
                    └── templates
```

### Apply mitxpro-theme

To apply a theme to an Open edX site, follow these steps.

1. Sign in to the Django administration console for your base URL. For example, http://{your_URL}/admin.
2. Select Site themes.
3. Select Add site theme.
4. From the Site menu, select the site you want to apply a theme to. You can select default site.
5. In the Theme dir name field, enter the `mitxpro-theme` of the theme.
6. Select Save.

### Compiling a Theme

```
$ make lms-shell
$ paver update_assets --themes mitxpro-theme
```
