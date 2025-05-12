# Some notes on patches for the site halgebra.math.msu.su


## How these patches were created

Simple example (without -d option):
```bash
# Current production state directory: /var/vhosts/halgebra/wiki/lib/plugins/translation
# Directory with my changes:          /var/vhosts/halgebra/wiki-dev/lib/plugins/translation

parent_dir="/var/vhosts/halgebra"
current_state="wiki/lib/plugins/translation"
changed_state="wiki-dev/lib/plugins/translation"
patch_name="/path/to/halgebra-patches/patch-name.patch"

cd $parent_dir
diff -Naru $current_state $changed_state > $patch_name
```


## How to apply these patches

Simple example (without -d option):
```bash
parent_dir="/var/vhosts/halgebra"
wiki_dir="${parent_dir}/wiki"
patch_name="/path/to/halgebra-patches/patch-name.patch"

cd $wiki_dir
# Check:
patch -p1 --dry-run < $patch_name
# Patch:
patch -p1 < $patch_name
```


## dokuwiki-plugin-translation

Original repo: [dokuwiki-plugin-translation](https://github.com/splitbrain/dokuwiki-plugin-translation/)

Why the patch: fixes the Russian translation on the page `/doku.php/main?do=admin&page=translation`

Install last supported by dokuwiki-2020-07-29a translation plugin version:
```bash
wget https://github.com/splitbrain/dokuwiki-plugin-translation/archive/refs/tags/2021-08-23.zip
unzip 2021-08-23.zip
# Change name if needed
```

Apply patch to production:
```bash
patch -p1 -d /var/vhosts/halgebra/wiki < dokuwiki-plugin-translation.fix-ru-lang.patch
```

Revert patch:
```bash
patch -R -p1 -d /var/vhosts/halgebra/wiki < dokuwiki-plugin-translation.fix-ru-lang.patch
```
