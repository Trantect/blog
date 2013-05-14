---
published: true
layout: default

---

## Outline
Big Wallpaper is an desktop software based on Python and GTK for Unity.It can fetch images of the world most hottest news from the specific web sites you configure.

## Default image source
- [boston.com](http://www.boston.com/bigpicture)
- [theatlantic.com](http://www.theatlantic.com/infocus/)
- [latimes.com](http://framework.latimes.com/)
- [nbcnews.com](http://photoblog.nbcnews.com/)
- [reuters.com](http://blogs.reuters.com/fullfocus/)

## Building Debian/Ubuntu package

### Update changelog (optional)

    dch -v VERSION-1
    
### Update debian files with setup.py (optional)

    python setup.py sdist
    
### Build it

    debuild -us -uc -b

### Build DSC file (optional, for PPA)
    
    debuild -tc -S -sa 

### Clean folder debian (optional)

    debuild clean

## Install with PPA repository (Ubuntu)

    sudo add-apt-repository ppa:yale-huang/ppa
    sudo apt-get update
    sudo apt-get install python-big-wallpaper
    
## Run it

Type ```BigWallpaper``` in the *Dash Home* of Unity launcher, and click the icon.
