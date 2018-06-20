
Changelog
---------

master
~~~~~
1) [TASK] Use partial file directly for "get-column-content".
2) [TASK] Use partial as partial and not template.
3) [TASK] Cleanup on "ce--section-header.html"
4) [DOCS] Docs update.

0.0.9
~~~~~
1) [DOC] Add docs about media management.

0.0.8
~~~~~
1) [TASK] Remove inclusion of partial as all partials are anyway read at start of hugo.
2) [TASK] Refactor content elements by removing "with" and allowing all variables to be available inside content element
  scope.
3) [TASK] Refactor of ce--section-header
4) [TASK] Add image processing options to general config and /resources folder to .gitignore.
5) [TASK] Add media storage. Configuring card element for using media.

0.0.7
~~~~~
1) [TASK] Refactor grid support.

0.0.6
~~~~~
1) [FEATURE] First raw version for grid support.

0.0.5
~~~~~
1) [FEATURE] Support for publishDate, expireDate for content elements.

0.0.4
~~~~~
1) [TASK] Change the way columns data is stored. Its now assoc array instead
   of separate arrays.

0.0.3
~~~~~
1) [TASK] Make homepage to read layouts from content files.
2) [BUGFIX] Fix wrong path on content.
3) [TASK] Rename section names / add new section main_sidebar_left.
4) [TASK] Code cleanup.
5) [TASK] Move getColumnContent template to separate file in /partial and include it in each section.
6) [TASK] Multiple cleanup / file renaming / variables renaming.

0.0.2
~~~~~

1) [BUGFIX] Fix wrong/old naming of content columns.
2) [DOCS] Docs fixes.
3) [DOCS] Definitive way of doing translation for pages section is "url" in front matter. Change docs.
4) [TASK] Implement template getColumnContent for repeating code for fetching columns content.
5) [TASK] Cleanup on content elements and content itself.

0.0.1
~~~~~

1) Init version.