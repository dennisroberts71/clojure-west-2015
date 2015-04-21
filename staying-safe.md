# SAFE - Sonian Archive File Engine

Three subsystems:

* Configuration
* Modules
* Administration

## Configuration

* `.clj` or `.js` or `.edn` file
* finds on classpath
* simpel call in
* `#_` for comments

The way that they load configurations is pretty interesting, and they
can merge the configurations together. They do search for configs in
the classpath, which is something that we may want to change, but it
does sound like the system is fairly flexible.

Open-source version called Carica.

https://github.com/sonian/carica

## Modules

* Which modules are loaded is controlled by the configuration.
* They can schedule periodic tasks.

Open-source version carousel.

https://github.com/sonian/carousel

## Administration

* `defadmin` macro defines administrative commands

Open-source version coming soon.
