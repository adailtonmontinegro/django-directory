A simple app that allows listing and downloading files from a given directory, 
while controlling who can access the files.

Installation
============
Add to `INSTALLED_APPS` entry `'directory'`
Syncdb is not required as there are no models.

Add to the `settings.py` file::

    DIRECTORY_DIRECTORY = '/path/to/dir'

That's the directory to be listed.

Add to the `urls.py` file the url entry, e.g.:

    ('^backups/$', include('directory.urls')),

Dependencies
============
If setting `DIRECTORY_ACCESS_MODE` is set to `'check-perms'`, or (possibly) `'custom'`,
then this app will require `django.contrib.auth` installed in the project.

Configuration
=============

Setting `DIRECTORY_ACCESS_MODE`, can be one of: `'public'`, `'check-perms'`, `'custom'`,
value `'public'` is default.

* value `'public'` means that anyone can see the directory and download files.
* `'check-perms'` means that django permission `'directory_read'` from `django.contrib.auth` will be checked
* `'custom'` - means that function provided with `DIRECTORY_ACCESS_FUNCTION` will be called to check the permission

`DIRECTORY_ACCESS_FUNCTION` - a function or python path to the custom permission checking function e.g. `'myapp.perms.check_get_backups_perm'`.

The function should accept parameter `request` and return a Boolean value - access granted if `True`.

`DIRECTORY_TEMPLATE` - path to the template file for the directory listing. Default value
is `'directory/list.html'`
