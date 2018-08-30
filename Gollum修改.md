# Gollum修改

```
diff --git a/lib/gollum/public/gollum/css/gollum.css b/lib/gollum/public/gollum/css/gollum.css_old
index dd1a33e..de90e47 100755
--- a/lib/gollum/public/gollum/css/gollum.css
+++ b/lib/gollum/public/gollum/css/gollum.css_old
@@ -77,7 +77,7 @@ a:hover, a:visited {
 
   #head ul.actions {
     clear: none;
-    float: left;
+    float: right;
     margin: 0;
   }
 }

```

```
diff --git a/lib/gollum/templates/page.mustache b/lib/gollum/templates/page.mustache_old
index efeec4b..80d1bf8 100644
--- a/lib/gollum/templates/page.mustache
+++ b/lib/gollum/templates/page.mustache_old
@@ -7,6 +7,7 @@ Mousetrap.bind(['e'], function( e ) {
 </script>
 <div id="wiki-wrapper" class="page">
 <div id="head">
+  <h1>{{page_header}}</h1>
   <ul class="actions">
     <li class="minibutton">
       {{>searchbar}}
@@ -44,8 +45,6 @@ Mousetrap.bind(['e'], function( e ) {
        class="action-page-history">History</a></li>
     <li class="minibutton"><a href="{{base_url}}/latest_changes"
        class="action-page-history">Latest Changes</a></li>
-    <li class="minibutton"><a href="https://github.com/linyingx/WiKi"  target="_blank"
-       class="action-page-history">Project GitHub</a></li>
     {{/page_exists}}
   </ul>
 </div>
```