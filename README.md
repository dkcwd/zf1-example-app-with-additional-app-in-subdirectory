zf1-example-app-with-additional-app-in-subdirectory
====================================================


Overview
--------

Based on a question from a student, this is a quick and dirty example of running 2 separate ZF1 apps where one app is accessed via a subdirectory of the other app.

For clarity one app project folder is called 'mainapp' and the other is 'subdirapp'.

Both apps initially used the default folder structure for ZF1 apps when created using Zend_Tool, the Zend Framework 1 CLI based Rapid Application Development tool.

'mainapp' has been modified in the following ways:

+ added a folder to the public folder and named it `subdirectory`
Note: `subdirectory` replaces the 'public' folder of 'subdirapp' and contains the usual default ZF1 .htaccess file and index.php file.
+ the index.php file in `subdirectory` has been modified so the `APPLICATION_PATH` constant is defined with a path which leads to `'subdirapp/application'`

'subdirapp' has been modified in the following ways:

+ a layout has been added to demonstrate use of the `baseUrl()` view helper
+ the public directory has been removed completely as it is not required


Requirements
------------

+ PHP >= 5.2.11 
+ Zend Framework 1 library on your PHP include path (I used version 1.12 during development)


Setup
-----

If you want to work with this project to experiment with this kind of configuration then I recommend you set up a virtual host.

Using very basic settings for a ZF1 virtual host you could use this as a template if you are unsure of the settings

		<VirtualHost *:80>
		  ServerAdmin webmaster@dummy-host.example.com
			DocumentRoot "EDIT-THIS-AND-ADD-FULL-PATH-TO\mainapp\public"
			ServerName zf-project-with-subdirectory-zf-project.local
			<Directory EDIT-THIS-AND-ADD-FULL-PATH-TO\mainapp\public>
			Options Indexes FollowSymLinks
			AllowOverride All
			allow from all
			</Directory>
		</VirtualHost>



Notes
-----

+ Feel free to name your virtual host `ServerName` as you like. I've used `zf-project-with-subdirectory-zf-project.local` within the example in these notes.

+ My example is based on both 'mainapp' and 'subdirapp' project folders being placed at the same level within a particular directory structure so if you choose to place them in a different location from each other you will need to adjust the value being assigned to `APPLICATION_PATH` in the index.php file found in the 'subdirectory' folder within the 'public' folder of 'mainapp'.

+ I used the `baseUrl()` view helper in the layout of 'subdirapp' in order to make the links to assets work appropriately with relative paths (Example: compare the css file links in the source code at `subdirapp/application/layouts/scripts/layout.phtml` with the code when you visit `http://zf-project-with-subdirectory-zf-project.local/subdirectory` then 'view-source' in your browser and you will see the css is being served relative to `subdirectory`. 

+ See the configuration settings at 'subdirapp/application/configs/application.ini' and you can see the configuration for the `baseUrl()` view helper

		resources.frontController.baseUrl = /subdirectory
		
+ Bear in mind the apps are completely separate and so you would be required to configure them separately one way or another. 