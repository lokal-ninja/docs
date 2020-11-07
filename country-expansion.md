# Country expansion

Step by step guide how to expand Shoogle with a new country, in this example for Canada

## 1. Fetch and build

* Create a build script `canada.sh` in https://github.com/lokal-ninja/scripts `/build/` for new country if it has subregions, otherwise extend `all.sh` for specific continent

* Copy this file to your https://github.com/midzer/pbf2md folder

* Checkout language branch of new country, in this case `en`

* Run `go build` to compile pbf2md

* Run `./canada.sh`

* If everything worked smoothly, dont't forget to commit the build script

## Prepare region(s)

* Move region folder(s) from build step to a new folder, I use the country code in this case `shoogle/countries/ca`

* Copy `config.toml`, `.gitignore` and `.gitmodules` from an already existing same language region repo to each region folder

* Edit each `config.toml` (baseURL, title and repo). Do it carefully!

* Create new `content/_index.md` for each region with data taken from Wikipedia

* `git init`

* `git submodule sync`, then `git submodule update`

* `hugo server` to see if everything works (fix content/data if necessary). Clean up with `rm -rf resources/` afterwards

* `git commit -m "add theme"`

* `git add -A`

* `git commit -m "initial version"`

* Create repo on GitHub in Lokal Ninja organisation with region name

* `git remote add origin git@github.com:lokal-ninja/$region.git`

* `git push -u origin master`

## Prepare website

* Open https://github.com/lokal-ninja/website in your favourite IDE

* Checkout branch of a country where language matches your new country, in this case `us`

* Edit `content/_index.md` text to fit new country

* Edit `layouts/index.html` `<ul class="columns">` to fit new region paths

* Replace `static/us.json` with your new country code, in this case `ca.json` with new content

* Edit `config.toml` (baseURL, title)

* Edit `netlify.toml` to adapt redirects for each region

* `hugo server` to see if everything works

* `git checkout -b ca` <- new country code

* `git add -A`

* `git commit -m "branch ca"` <- new country code

* `git push origin ca` <- new country code

## Deploy

* In Netlify -> New site from Git -> choose `website` repo -> choose `ca` branch -> Site Settings -> Site name `shoogle-ca`

* Wait for build then -> Set up a custom domain -> `ca.shoogle.net` -> Site settings -> Build & Deploy -> Post processing -> Disable Form detection

* In Netlify for new region(s) -> New site from Git -> choose `$region` repo -> Show advanced -> New variable -> `HUGO_VERSION` `0.76.5`

* -> Site Settings -> Site name `ln-$region` -> Build & Deploy -> Post processing -> Disable Form detection

## Going live

* Open https://github.com/lokal-ninja/landingpage in your favourite IDE

* Edit `layouts/index.html` AND `layouts/overview/section.html.html` `<ul class="columns">` to fit new country path

* In same (identical) files extend `const countries` array with new country code, in this case `ca`

* Edit `netlify.toml` with new redirect for new country

* `hugo server` to see if everything works

* `git commit -am "enable ca"` <- new country code

* `git push origin master`

* Test `ca.shoogle.net` <- new country code

* DONE!

