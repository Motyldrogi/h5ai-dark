# h5ai

[![license][license-img]][github]

A modern HTTP web server index for Apache httpd, lighttpd, and nginx.


## Important

* Do **not** install any files from the `src` folder, they need to be
  preprocessed to work correctly!

## Prerequisites
- Install PHP and PHP-FPM

## Nginx Conf

```sh
server {
    listen 80;
    index index.php /_h5ai/public/index.php;
    server_name share.example.com;
    
    root /var/www/share.example.com;
        
    location /_h5ai/private {
        return 403;
    }

    location ~ [^/]\.php(/|$) {
    fastcgi_split_path_info ^(.+?\.php)(/.*)$;
    if (!-f $document_root$fastcgi_script_name) {
        return 404;
    }

    fastcgi_param HTTP_PROXY "";

    fastcgi_pass unix:/run/php/php7.4-fpm.sock;
    fastcgi_index index.php;

    include fastcgi_params;

    fastcgi_param  SCRIPT_FILENAME   $document_root$fastcgi_script_name;
    fastcgi_param  PATH_INFO         $fastcgi_path_info;
    }
}
```

## Build

To build **h5ai** yourself either `git clone` or
download the repository. From within the root folder run the following
commands to find a fresh zipball in folder `build` (tested on linux only,
requires [`node 10.0+`][node] to be installed, might work on other
configurations).

~~~sh
> npm install
> npm run build
~~~


## License

The MIT License (MIT)

Copyright (c) 2020 Lars Jung (https://larsjung.de)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.


## References
**h5ai** profits from other projects, all of them licensed under the MIT license
too. Exceptions are some [Material Design icons][material-design-icons] (CC BY 4.0).

[github]: https://github.com/motyldrogi/h5ai-dark
[node]: https://nodejs.org
[material-design-icons]: https://github.com/google/material-design-icons

[license-img]: https://img.shields.io/badge/license-MIT-a0a060.svg?style=flat-square
