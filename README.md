# WebLaminar - Mediawiki
## Docker stack with NGINX, Mediawiki, and MariaDB.
## Uses Mediawiki 1.29 binaries.


Docker compose cluster to get Mediawiki running with customizations, including collapsible menu and multi-file uploads.
Uses NGINX instead of Apache for better performance and Alpine Linux for a smaller image.

## Instructions

1. Install Docker on host if needed.
1. Create directory and cd into it.
1. git clone the repository.
1. Edit stack.yml for db credentials.
1.  Run docker-compose -f stack.yml up
1.  Browse to http://localhost:7000
1. Configure mediawiki
  * DBhost = db
  * document all choices for future reference.
  * download LocalSettings.php from configuration.
1. Bring down the stack ```docker-compose -f stack.yml down```
1. List your container instances ```docker ps -a```
1. Remove the mediawiki container ```docker rm container_id```
1. Edit LocalSettings.php and add text from Settings.Addons to bottom of file.
1. mv LocalSettings.php to conf directory
1. mv Dockerfile Dockerfile.orig
1. mv Dockerfile.Addon Dockerfile
1. Run docker-compose -f stack.yml build
1. Run docker-compose -f stack.yml up
1. Browse to http://localhost:7000 and begin content creation.  Enjoy!

## Known issues

If you want to change the skin background images use the url http://localhost:7000/index.php?title=MediaWiki:Vector.css to change the css.
Be sure to add images in the conf directory, edit the Dockerfile and rebuild.

```
    body {
    	background-color: #f3f3f3;
    	background-image: url(images/paper.gif); <== menu background
    }

    #mw-page-base {
    	height: 5em;
    	background-color: white;
    	background-image: url(images/Cherry.jpg); <== header background
    	background-position: bottom left;
    	background-repeat: repeat-x;
    }
```
http://localhost:7000/index.php?title=Special:MultiUpload is a link to the
MultiUpload form.  Comes in handy for images, etc.

Collapsible menus are enabled and editable with http://localhost:7000/index.php?title=Mediawiki:Sidebar&action=edit

Adminer database tool http://localhost:6080

## Credits

Many thanks to Jesse Savary ( sirsavary/dockerfiles) to get the ball rolling.
