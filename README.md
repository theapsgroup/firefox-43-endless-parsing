# firefox-43-endless-parsing
bug reproduction of endless sourcemap parsing

# steps to reproduce
- visit http://theapsgroup.github.io/firefox-43-endless-parsing/index.html in firefox (tested in 43)
- open the developer tools
- open the debugger tab once so the sourcemaps will be loaded
- reload the page
- the console should log "script tag" and "empty.js" but not "end of body", if "end of body" is there reload again until it does not

It does not always seem to work, just keep refreshing until it does (works almost every time though).
It helps to disable cache since it seems to have some kind of race condition.

# bug results
- loading icon in the tab never ends
- loading information in the bottom corner never ends
- parsing never reaches the bottom console log
- when recording performance you'll see the fps stays around 0.99 and only doing garbage collection
- document.readyState never leaves "loading" and thus several load events never happen
