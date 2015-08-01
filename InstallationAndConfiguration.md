# Installing Files #

AssetLibPro consists of two files:
  1. A **library** file _"Assetlibpro.php"_
  1. A **config** file _"assetlibpro.php"_

The **library** file _"Assetlibpro.php"_ goes into your CodeIgniter application's "libraries" folder, such as:
_"CodeIgniter/application/libraries/Assetlibpro.php"_

The **config** file _"assetlibpro.php"_ goes into your CodeIgniter application's "config" folder, such as:
_"CodeIgniter/application/config/assetlibpro.php"_

To allow compression you also need to download **CSSTidy** and **JSMin**

Download **CSSTidy** and put the contents of the package into your _"/system/plugins/"_ folder (or wherever you’ve set it in your config file)
```
https://sourceforge.net/project/showfiles.php?group_id=148404&package_id=166584
```

Download **JSMin** and put the jsmin php file (renamed to "jsmin.php"!) into your _"/system/plugins/"_ folder (or wherever you’ve set it in your config file)
```
http://jsmin-php.googlecode.com/files/jsmin-1.1.1.php
```

You also need to add the url helper to your autoload configuration.

# Configuration #

In your **Controller** you need to load the library, like:
```
$this->load->library('assetlibpro');
```
…or add it to your autoload config, like:
```
$autoload['libraries'] = array('assetlibpro');
```

Now we need to actually add some assets to AssetLibPro. This is also done in your Controller, like:
```
<?php
$this->assetlibpro->add_css('styles_1.css');
$this->assetlibpro->add_css('styles_2.css');
$this->assetlibpro->add_css('styles_3.css');
$this->assetlibpro->add_js('mootools.js');
$this->assetlibpro->add_js('foobar.js');
?>
```
If you want to have one styles reference for print styles and one for screen, or whatever, then you can do this by adding a media tag to the command:
```
<?php
$this->assetlibpro->add_css('print_styles_1.css', 'print');
$this->assetlibpro->add_css('print_styles_2.css', 'print');
$this->assetlibpro->add_css('styles_1.css');
$this->assetlibpro->add_css('styles_2.css');
$this->assetlibpro->add_css('styles_3.css');
$this->assetlibpro->add_js('mootools.js','frameworks');
$this->assetlibpro->add_js('foobar.js');
?>
```
Asset file paths are relative to the asset directory as defined in config file!

If you do not provide a group name, then the asset gets added to the default group (see config).
(Splitting up Javascript into groups —like seen here— does not make any sense (imho). But as both functions (_add\_css()_ & _add\_js()_) share the same functionality, it's possible to do it and thus documented. :D

Additionally you can provide a third parameter:
```
<?php
$this->assetlibpro->add_css('print_styles_1.css', 'print', 'dark_theme');
//or:
$this->assetlibpro->add_css('print_styles_1.css', '', 'dark_theme');
?>
```
This allows you to have some theme switching functionality.
(Once again this is also available for ".js" files.)

Then in your **View** you need to tell AssetLibPro to actually insert the references to the assets, like:
```
<?= $this->assetlibpro->output('css'); ?>
<?= $this->assetlibpro->output('js'); ?>
```
Btw, using this variation would result in the same output:
```
<?= $this->assetlibpro->output('all'); ?>
```


I for one also prefer to surround the output commands with a benchmark mark:
```
<?php
$this->benchmark->mark('AssetLib_Pro_start');
echo $this->assetlibpro->output('css');
echo $this->assetlibpro->output('js');
$this->benchmark->mark('AssetLib_Pro_end');
?>
```


Further more you either need load the config file in your controller manually (and before actually loading the library file), like:
```
$this->config->load('assetlibpro');
```
…or add it to your autoload config, like:
```
$autoload['config'] = array('assetlibpro');
```

# Optimal Results #

I **strongly recommend** to set these config settings to "TRUE" for **optimal compression** and **caching** results:
  * $config['alp\_enable\_csstidy'] = TRUE;
  * $config['alp\_enable\_jsmin'] = TRUE;
  * $config['alp\_gzip\_compress\_css'] = TRUE;
  * $config['alp\_gzip\_compress\_js'] = TRUE;
  * $config['alp\_force\_cache\_css'] = TRUE;
  * $config['alp\_force\_cache\_js'] = TRUE;
They are set to TRUE by default, so just don't change them. ;)