# mitxpro-theme
An open edX theme for MIT xPRO 

## Table of contents:
1. Configure Open edX
2. Configuring MIT xPRO theme


### 1. Configure Open edX

Please follow [Configure Open edX](https://github.com/mitodl/mitxpro/blob/master/docs/configure_open_edx.md).

## 2. Configuring MIT xPRO theme

For detail about themes, please see [edx-docs about themes](https://edx.readthedocs.io/projects/edx-installing-configuring-and-running/en/latest/configuration/changing_appearance/theming/overview_themes.html).

For the LMS, you edit `/edx/app/edxapp/lms.env.json` to set 

`"ENABLE_COMPREHENSIVE_THEMING": true`

For Studio, you edit `/edx/app/edxapp/cms.env.json` to set 

`"ENABLE_COMPREHENSIVE_THEMING": true`

For each Open edX component that you want to apply a theme to, add the absolute path of the themes directory to the `COMPREHENSIVE_THEME_DIRS` configuration property.
That path should be accessible to docker container. Easiest way is to put you theme in `edx-platform/themes`.

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
