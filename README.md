# mitxpro-theme
An open edX theme for MIT xPRO

## Table of contents:
1. Configure Open edX
2. Configuring MIT xPRO theme


### 1. Configure Open edX

Please follow [Configure Open edX](https://github.com/mitodl/mitxpro/blob/master/docs/configure_open_edx.md).

## 2. Configuring MIT xPRO theme

For detail about themes, please see [edx-docs about themes](https://edx.readthedocs.io/projects/edx-installing-configuring-and-running/en/latest/configuration/changing_appearance/theming/overview_themes.html).

**Note:** Please use `koa` branch from the theme repository if you are integrating it with `koa` release of `Open edX`.

Make sure you have MIT xPRO base url set in your settings. You can either add it in `env` files or simply add it in `edx-platform/lms/envs/private.py`. e.g

`XPRO_BASE_URL="http://xpro.odl.local:8053/"`

To apply themes in Open edX you have to add the absolute path of the themes directory to the `COMPREHENSIVE_THEME_DIRS` in `lms.yml` and `studio.yml` respectively.
That path should be accessible to docker container. Easiest way is to put your theme in `edx-platform/themes`.

If you have your theme along with other themes at `edx-platform/themes/mitxpro-theme`, you can use `/edx/app/edxapp/edx-platform/themes` as directory path while you follow the steps below.

#### Open Shell
First of all you open lms/studio shell e.g. `make lms-shell` or `make studio-shell`

### OpenEdx release Juniper and above:
For the LMS, you edit `/edx/etc/lms.yml` and for Studio, you edit `/edx/etc/studio.yml` to set below properties

#### Enable theme
`ENABLE_COMPREHENSIVE_THEMING: true`

#### Add theme directory path
```
COMPREHENSIVE_THEME_DIRS:
- '/edx/app/edxapp/edx-platform/themes'
```


### For OpenEdx release before Juniper:
For the LMS, you edit `/edx/app/edxapp/lms.env.json` and For the Studio, you edit `/edx/app/edxapp/cms.env.json` to set below properties

#### Enable theme
`"ENABLE_COMPREHENSIVE_THEMING": true`

#### Set theme directory path
```
"COMPREHENSIVE_THEME_DIRS": [
    "/edx/app/edxapp/edx-platform/themes"
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
