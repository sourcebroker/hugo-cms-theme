hugo-cms-theme
==============

.. contents:: :local:

What does it do?
----------------

This is proof of concept for having Hugo (gohugo.io) working as frontend renderer for any content element based CMSes
as TYPO3, Drupal for example. The CMS acts then only as backend or JSON API data provider.

This is only Hugo theme. If you want to test it with real CMS then the only real working exporter at this time is exporter
for TYPO3. You can find it here https://github.com/sourcebroker/hugo


Why someone would need that ?
-----------------------------

Several reasons:

- **Less time to implement**

  Today "well done" clickdummies are almost working websites. For small websites the time needed to implement clickdummy
  into TYPO3, Drupal or whatever other content element based CMS can be huge compared to gains. Therefore one can consider
  to prepare clickdummy using this package and use backend of CMS only for editing content which will be then exported
  to Hugo files which will generate complete website. If for some reason the website will go too complicated in future
  and Hugo will be not able to handle that complex case then there is always fallback to implement frontend rendering in
  CMS as the content is already prepared in backend of that CMS.

- **Security**

  Hugo serves only static pages and if there will be no JSON API served by CMS then this CMS can be fully hidden
  and accessed only by dedicated IP.

- **Speed**

  Compare following. Hugo can render 1000 pages in 1 seconds and they are static - means no more pressure on
  server and extremely fast TTFB (30-60ms). Average for CMSes is like render 0,5 to 4 pages in 1 second. Then the pages
  are in cache and served with average TTFB 120ms-200ms. One can argue that CMSes are able also to generate static html.
  This is true but first those pages must be rendered with average like 0,5 to 4 pages in 1 second. Imagine now you have
  website with 10.000 pages and you must clear cache often for whatever reason.

- **Content element based clickdummy pattern**

  Sometimes its hard to explain to external frontend developers what means to build clickdummy with universal layouts
  and content elements (which share common classes for modification). This Hugo based clickdummy reflects the logic
  behind content element based CMSes (general layouts and reusable content elements). So even if you still want to
  implement frontend with CMS then this package can help you to prepare clickdummy the way which can be easily implemented.


Installation
------------

1) Clone package:
   ::

      git clone https://github.com/sourcebroker/hugo-cms-theme.git

2) Run:
   ::

      hugo server


What is working already?
-------------------------

For pages
+++++++++

- **Equivalent of layouts**

  "Sections" in this Hugo theme are used as equivalent of "layouts" in CMSes.

- **Content elements rendering**

  What is to be rendered on page is defined in front matter as "colx" where x is the id of column defined in
  "layout" of CMS. The "colx" should have array of content element id's. The minimal example front matter for showing
  content would be then (YAML format):

  ::

    title: About us
    layout: main_and_sidebar_right

    columns:
      col0:
        - 10
        - 31
        - 2
      col1:
        - 113
        - 9

For content elements
++++++++++++++++++++

- **Content elements as partials in /partials/content/**

  Templates of content elements are defined as partials. For example: ``/layouts/partials/content/faq.html``

- **Content elements data in /data/content**

  Data to render content element are kept in ``/data/content/x.yaml`` where x is equal to uid of content element.

- **Multilang content support**

  Data can be multilang. The file name must then have the value of lang defined in "languages" part of Hugo config.
  For example ``/data/content/1.yaml`` is default language and ``/data/content/1.de.yaml`` is for german language.

- **Multilang content fallback**

  There is content fallback for multilang content. For example if lang is DE and there is no file
  ``/data/content/1.de.yaml`` then content from ``/data/content/1.yaml`` is taken as fallback.

- **Content elements can be disabled/enabled (draft)**

  There is support for enable/disable single content element. As analogy to Hugo page its also called "draft".

- **Content elements can be disabled/enabled according to date (publishDate, expireDate)**

  There is support for enable/disable single content element according to time. As analogy to Hugo page its called
  "publishDate", "expireDate".

- **Content elements can be put into grid / columns**

  There is support creating a grids of content elements. Look at ``data/content/50.yaml`` how such content element
  looks like. So far there is only support for two columns - some refactor is needed to make it more universal.

- **Global media storage**

  Every CMS has now some kind of media management module. Here it is reflected in folder ``/content/_media/``. You can
  define as much separate storages as needed placing them for example in ``/content/_media/storage01``,
  ``/content/_media/storage01``, etc. Each file from CMS storage must be reflected in ``content/_media/index.md``
  and have following structure.

  ::

    ---
    resources:
      - src: "storage01/sunsets/sunset.jpg"
        name: "445"
        title: "Sunset"
        params:
          alt: "Sunset on sea"
      - src: "storage01/image-1.png"
        name: "441"
        title: "Hugo banner"
        params:
          alt: "Hugo banner"
    ---

  The "name" should be some identifier (id) of media resource from CMS. In content element file the media file then
  must be reflected by this identifier. Look for example in ``data/content/20.yaml`` and example of media file usage and
  resizing in ``layouts/partials/content/card.html``.


NOTE
----

For translations of the url the "url" option in front matter is used because slug is not working for page sections.
Read here for more explanation: https://discourse.gohugo.io/t/multilingual-url-slug-is-being-ignored/10003
