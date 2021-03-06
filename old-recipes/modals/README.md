# Problem

You want to add a [modal window](http://getbootstrap.com/javascript/) to your [reagent](https://github.com/reagent-project/reagent) webapp.

# Solution

**Plan of Action**

We are going to use the [reagent-modals](https://github.com/Frozenlock/reagent-modals) library.

Steps:

* Create a new project using the [reagent-seed](https://github.com/gadfly361/reagent-seed) template.
* Add reagent-modals library to `project.clj`
* Add modal window to `home-page` component.

Affected files:

* `project.clj`
* `src/modals/views/home_page.cljs`

## Create a reagent project

```
$ lein new reagent-seed modals
```

## Add reagent-modals library to project.clj

First, let's add the [reagent-modals](https://github.com/Frozenlock/reagent-modals) library to our `project.clj` file.

```clojure
(defproject modals "0.1.0-SNAPSHOT"
  :source-paths ["src" "dev"]
  :dependencies [[org.clojure/clojure "1.6.0"]
                 [org.clojure/clojurescript "0.0-2342"]
                 [ring "1.2.2"]
                 [compojure "1.1.6"]
                 [enlive "1.1.5"]
                 ;; ReactJS wrapper
                 [reagent "0.4.2"]
                 ;; Client-side routing
                 [secretary "1.2.0"]
                 ;; CSS
                 [garden "1.2.1"] 
;; ATTENTION \/
                 ;; modal window
                 [org.clojars.frozenlock/reagent-modals "0.1.0"] ]
;; ATTENTION /\

...
```

## Add modal window to home-page component

Navigate to `src/modals/views/home_page.cljs`. To add a modal window, we need to require the reagent-modals library in our namespace.

```clojure
(ns modals.views.home-page
  (:require [reagent-modals.modals :as reagent-modals]))

...
```

Next, we create a modal function called `modal-example`.

```clojure
(ns modals.views.home-page
  (:require [reagent-modals.modals :as reagent-modals]))

;; ATTENTION \/
(defn modal-example []
  (reagent-modals/modal [:div "some message to the user!"]))
;; ATTENTION /\

...
```

Finally, we 1) include the `modal-window` function, and 2) execute the `modal-example` function when we click on a button.

```clojure
(ns modals.views.home-page
  (:require [reagent-modals.modals :as reagent-modals]))

(defn modal-example []
  (reagent-modals/modal [:div "some message to the user!"]))

;; ATTENTION \/
(defn home-page []
  [:div
   [:h2 "Home Page"]
   [reagent-modals/modal-window]
   [:div.btn.btn-primary {:on-click modal-example} "My Modal"]
   ])
;; ATTENTION /\
```

# Usage

To view our app, we need to perform the following steps:

Create a css file.

```
$ lein garden once
```

*Note: if it says "Successful", but you aren't able to type anything into the terminal, hit `Ctrl-c Ctrl-c`.*

Create a javascript file from your clojurescript files.

```
$ lein cljsbuild once
```

Start a repl and then start the server.

```
$ lein repl

user=> (run!)
```

Open a browser and go to *localhost:8080*. You should see your reagent application!
