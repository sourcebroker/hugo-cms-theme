hugo-typo3
==========

.. contents:: :local:

What does it do?
----------------

This is proof of concept for having HUGO working with TYPO3 as backend.


Installation
------------

1) Install package with composer:
   ::

      composer require sourcebroker/hugo-typo3


2) Run:
   ::

      hugo server


What is working already?
-------------------------

For pages
+++++++++

- **Equivalent of backend_layouts**

  Sections in HUGO can be use as equivalent of "backend_layouts" in TYPO3. This is working well except homepage (TODO).

- **Content elements rendering**

  What is to be rendered on page is defined in front matter as "col_x" where x is the id of column defined in
  "backend_layout". The "col_x" should have array of tt_content uids. The minimal front matter for showing content
  would be then (YAML format):

  ::

    title: About us
    layout: main_and_sidebar_right

    col_0:
      - 10
      - 31
      - 2

    col_1:
      - 113
      - 9

For content elements
++++++++++++++++++++

- **Content elements templates as partials at /partials/content-**

  Templates of content elements as defined as partials. For example: ``/layouts/partials/content-faq2.html``

- **Content elements data in /data/content**

  Data to render content element are kept in ``/data/contant/x.yaml`` where x is equal to uid of content element in TYPO3.
  You can consider this folder as equivalent of "tt_content" table form TYPO3.

- **Multilang content**

  Data can be multilang. The file must then have the value of lang from url. Like ``/data/content/1.yaml`` is default
  and ``/data/contant/1.de.yaml`` is for german language.

- **Multilang content fallback**

  There is content fallback for multilang content. For example if page is DE and there is no file
  ``/data/contant/1.de.yaml`` then content from ``/data/contant/1.yaml`` is taken as fallback.

- **Content elements can be disabled/enabled**

  There is support for enable/disable single content element. In TYPO3 there is "hidden" field for that. Here the field
  for that in data of content element is "draft" (which is analogy for "draft" from front matter of page in HUGO)


TO DO
+++++

- Support for images.
- Make separate template for showing content elements from column. Right now we repeat it in /section. Not cool at all.
- Make support for start time to show content/ end time to stop showing content.
- Make support for ext:gridelements