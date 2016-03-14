# Flavy - a simple ffmpeg layer for laravel 5.2
[![downloads](https://poser.pugx.org/folour/flavy/downloads.png)](https://packagist.org/packages/folour/flavy)
[![license](https://poser.pugx.org/folour/flavy/license.png)](https://packagist.org/packages/folour/flavy)

FFmpeg layer for Laravel 5.2, this is a fork of rafasamp/sonus package.

Simple API for convert audio/video files, get thumbnails from video, information of files

## Installation
Install Flavy via composer

    composer require folour/flavy dev-master
    
### In config/app.php to providers array add:

    Folour\Flavy\Provider\FlavyServiceProvider::class,

### And to aliases array add:

    'Flavy' => Folour\Flavy\FlavyFacade::class,

### In terminal in project root run:

    php artisan vendor:publish
    
## Usage
### Simple conversion from ogg to mp3, with change bitrate:

    Flavy::from('path/to/file.ogg')
        ->to('path/to/converted/file.mp3')
        ->aBitrate(128)
        ->aCodec('libmp3lame')
        ->overwrite()
		->run();

### Get file info:

    Flavy::info('path/to/file.mp3'); //returns array with file info
    Flavy::info('path/to/file.mp3', 'xml'); //returns xml string with file info
    Flavy::info('path/to/file.mp3', 'csv'); //returns csv string with file info
    Flavy::info('path/to/file.mp3', 'json', false); //returns json string with file info
    
### Make thumbnails:

    Flavy::thumbnail('path/to/video.mov', 'path/to/images/thumb_%d.jpg', 10); //Make 10 thumbnail and calculate time interval $duration/$count
    Flavy::thumbnail('path/to/video.mov', 'path/to/images/thumb_%d.jpg', 10, 30); //Make 10 thumbnail with specified interval
    
### Get ffmpeg base information:

    Flavy::encoders(); //return a nested array with audio and video encoders
    Flavy::decoders(); //return a nested array with audio and video decoders
    Flavy::formats(); //return array with supported formats
    
    Flavy::canEncode('encoder'); //Check encoder support
    Flavy::canDecode('decoder'); //Check decoder support
    
		
