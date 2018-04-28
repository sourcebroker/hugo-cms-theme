hugo-typo3-theme
================

.. contents:: :local:

What does it do?
----------------

This is proof of concept for having HUGO (gohugo.io) working with TYPO3 (typo3.org) as backend. That means no fronted
possibilities of TYPO3 will be used except maybe JSON API.

This is only HUGO theme. If you want to test it with TYPO3 you need ext:hugo here https://github.com/sourcebroker/hugo

This theme and ext:hugo are in early beta - so be patient with bugs!

Any help to improve the code appreciated.


Why someone would need that ?
-----------------------------

Several reasons:

- **Less time to implement**

  Today "well done" clickdummies are almost working websites. For small websites the time needed to implement clickdummy
  into TYPO3 can be huge compared to gains (which sometimes is simple editing only). Therefore one can consider to use
  TYPO3 as backend only for editing content. This content then will be written to files used by HUGO to generate website.
  If for some reason the website will go complicated in future and HUGO will be not able to handle that complex case
  then there is always fallback to implement frontend rendering in TYPO3.

- **Security**

  HUGO serves only static pages and if there will be no JSON API served by TYPO3 then TYPO3 can be fully hidden
  and accessed only by dedicated IP.

- **Speed**

  Compare following. Hugo can render 1000 pages in 1 seconds and they are static - means no more pressure on
  server and extremely fast TTFB (30-60ms). TYPO3 average is like render 0,5 to 4 pages in 1 second. Then they are in cache
  and served with average TTFB 120ms-200ms. One can argue that there is ext:nc_staticfilecache which can serve TYPO3 generated
  pages as static html. This is true but first those pages must be rendered by TYPO3 with average like 0,5 to 4 pages in
  1 second. Imagine now you have TYPO3 website with 10.000 pages and you must clear cache often for whatever reason...

- **Content element based clickdummy pattern**

  Sometimes its hard to explain to external frontend developers what means to build clickdummy the "TYPO3 way" so with
  well-thought-out layouts and content elements (which share common classes for modification). This hugo based clickdummy
  reflects the logic behind TYPO3 layouts and reusable content elements. So even if you still want to implement frontend
  with TYPO3 this clickdummy can help you to prepare clickdummy that will be easily implemented into TYPO3.

Installation
------------

1) Clone package:
   ::

      git clone https://github.com/sourcebroker/hugo-typo3.git

2) Run:
   ::

      hugo server

What is working already?
-------------------------

For pages
+++++++++

- **Equivalent of backend_layouts**

  "Sections" in HUGO are used as equivalent of "backend_layouts" in TYPO3.

- **Content elements rendering**

  What is to be rendered on page is defined in front matter as "col_x" where x is the id of column defined in
  "backend_layout". The "col_x" should have array of tt_content uids. The minimal example front matter for showing content
  would be then (YAML format):

  ::

    title: About us
    layout: main_and_sidebar_right

    column0:
      - 10
      - 31
      - 2

    column1:
      - 113
      - 9

For content elements
++++++++++++++++++++

- **Content elements templates as partials at /partials/content-**

  Templates of content elements as defined as partials. For example: ``/layouts/partials/content-faq2.html``

- **Content elements data in /data/content**

  Data to render content element are kept in ``/data/contant/x.yaml`` where x is equal to uid of content element in TYPO3.
  You can consider this folder as equivalent of "tt_content" table form TYPO3.

- **Multilang content support**

  Data can be multilang. The file name must then have the value of lang defined in "languages" part of hugo config.
  For example ``/data/content/1.yaml`` is default language and ``/data/contant/1.de.yaml`` is for german language.

- **Multilang content fallback**

  There is content fallback for multilang content. For example if lang is DE and there is no file
  ``/data/contant/1.de.yaml`` then content from ``/data/contant/1.yaml`` is taken as fallback.

- **Content elements can be disabled/enabled**

  There is support for enable/disable single content element. In TYPO3 there is "hidden" field for that. Here the field
  for that in data of content element is "draft" (which is analogy for "draft" from front matter of page in HUGO)

NOTE
++++

For translations of the url the "url" option in front matter is used because slug is not working for page sections.
Read here for more explanation: https://discourse.gohugo.io/t/multilingual-url-slug-is-being-ignored/10003

TO DO
+++++

- Support for images.
- Make support for start time to show content end time to stop showing content.
- Make support for ext:gridelements.
