#### Hiding the Folders

Move the system and application folders above web root. Open main index.php file and set the $system_path and $application_folder.


#### Using Local CSS

Put the style file in the html folder.

```php
<link rel="stylesheet" type="text/css" href="<?php echo base_Url(); ?>css/style.css">
```



#### Defining a Default Controller

```php
// application/config/routes.php
$route['default_controller'] = 'blog';
```

