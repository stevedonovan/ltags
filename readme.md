`ltags` produces tag files compatible with extended [tags format](http://ctags.sourceforge.net/FORMAT)
used by Vim and [many other editors](http://en.wikipedia.org/wiki/Ctags#Editors_that_support_ctags)
This adds very useful semantic hints for symbols, such as basic type, global or file scope, belonging to what
struct, etc.

Although [Exuberant ctags](http://ctags.sourceforge.net/) is the most commonly used implementation, supporting
41 programming languages, it does not do Lua very well.  It only does functions, and always collects the module
and the function together (e.g 'tablex.imap') as the 'tag'.  No extended type information is provided, and no
indication of file scope.

Invocation is easy - this script only needs Lua (5.1 or 5.2) and is to be passed the filenames to be processed.
On Windows, wildcard arguments will also be expanded.

As with `ctags`, a single file 'tags' is generated in the directory where `ltags` is invoked.

The `-nv` option switches off module-level local variable tagging. 
The common practice of declaring imported functions as locals up front can complicate 
the simple business of going to the original definition.  So if we had `local imap = tablex.imap` up
top then there would be two items with name 'imap' visible in that module - the local alias
and the actual function.  Not a problem if your editor is comfortable with multiple tag values.

The `-nr` option switches off module-level local require tagging.
Class systems that return the class table from require produce lots of noise but the class definition is
removed by -nv (it's too aggressive). If we had `local Animal = class(function(a,name) a.name = name end)`,
then that definition would be removed by -nv but is retained with -nr and imports of that class like `local
Animal = require("Animal")` are not tagged.

The `-filelist` option takes a file full of filenames to process.
Passing filenames in a file instead of on the command-line may be preferable if you cannot use globs or have
other scripts that determine which files to parse.
