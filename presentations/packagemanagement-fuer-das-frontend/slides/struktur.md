##  Struktur

Flach vs. Baumstruktur

```
 └─┬ bower_components/
   ├── bootstrap/
   ├── html5shiv/
   ├── jquery/
   ├── jquery-placeholder/
   ├── rangesliderjs/
   ├── respondJs/
   └── tablesaw/
```
<!-- .element: class="fragment roll-in" data-fragment-index="1" -->

```
└──┬ node_modules/
   ├─┬ grunt-bump/
   │ └─┬ node_modules/
   │   └── semver/
   ├─┬ grunt-contrib-watch/
   │ └─┬ node_modules/
   │   ├── gaze/
   │   └── lodash/
   ├── semver/
   └─┬ yo/
     └─┬ node_modules/
       ├── lodash/
       └─── meow/
```
<!-- .element: class="fragment roll-in" data-fragment-index="2" -->

note:
    Duplikate Segen und Fluch! (Node Dedupe – Default ab npm 3.0)


