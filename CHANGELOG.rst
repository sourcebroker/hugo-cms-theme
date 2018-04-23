
Changelog
---------

dev-master
~~~~~~~~~~

a) [TASK] Use deployer-loader to load recipes.
b) [TASK] Add PhpIncludeInspection to prevent warnings in IDE.
c) [TASK][!!!] Update packages sourcebroker/deployer-extended, sourcebroker/deployer-extended-media,
   sourcebroker/deployer-extended-database, sourcebroker/deployer-loader. Add package sourcebroker/deployer-loader.
d) [TASK] Add .gitignore with vendors/ and composer.lock.
e) [TASK] Update docs.
f) [TASK] Move "magento:deploy:git_checkout" and "magento:setup:static-content:deploy:extended" to separate files/folders.
g) [BUGFIX] Add "area" parameter to "magento:setup:static-content:deploy:extended".
h) [TASK] Pass language as parameter of setup:static-content:deploy command.
i) [FEATURE] Add "deployer-bulk-tasks". Remove standard magento tasks file.
j) [TASK] Extend "shared_files" and "writable_dirs".
k) [TASK][!!!] Change deploy tasks order / add new tasks for Magento 2.2.
l) [TASK][!!!] Change name of "magento:deploy:git_checkout" to "magento:deploy:git-checkout" to follow magento convention.
m) [TASK] Make "magento:deploy:git-checkout" to be run before "deploy:clear_paths".
n) [TASK] Replace occurance 'pub' in deployer/set.php with {{web_path}}
o) [TASK] Add default value for 'db_defaults'.
p) [TASK] Change naming from 'db_defaults' to 'db_default'.

0.7.1
~~~~~

a) [DOCS] Update changelog


0.7.0
~~~~~

a) [FEATURE] Add second default place to check config file which is out of git /app/etc/env/unversioned.php

0.6.0
~~~~~

a) [TASK][!!!BREAKING] Remove task "deploy:magento:bugfix_for_deployed_version_txt" as the problem was fixed in Magento2.

b) [TASK][!!!BREAKING] Remove task "deploy:maintenance". Protecting deployment instances should be done by special modules.

c) [TASK][!!!BREAKING] Rename task "magento:setup:static-content:deploy" to "magento:setup:static-content:deploy:extended"

d) [TASK][!!!BREAKING] Remove task "deploy:magento:remove_var_regenerate" as the problem was fixed in Magento2.

e) [TASK][!!!BREAKING] Rename task "deploy:magento:checkout_for_overwritten_htaccess" to "magento:deploy:git_checkout"

f) [TASK] Add default settings for task magento:setup:static-content:deploy:extended
   ::

   set('static_content_deploy_frontend_themes', ['Magento/blank']);
   set('static_content_deploy_frontend_languages', ['en_US']);
   set('static_content_deploy_adminhtml_themes', ['Magento/backend']);
   set('static_content_deploy_adminhtml_languages', ['en_US']);

g) [TASK] Add deafult settings for task "magento:deploy:git_checkout":
   ::

   set('magento_git_checkout_items', ['pub/.htaccess']);


0.5.0
~~~~~

a) [TASK] Make dependency to deployer/deployer-dist

0.4.0
~~~~~

a) Update sourcebroker/deployer-extended-database to version 4.0.0

0.3.0
~~~~~

a) Set "default_stage" as callable. This way "default_stage" can be now overwritten in higher level packages.