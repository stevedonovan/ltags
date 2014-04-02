`ltags` produces tag files compatible with extended [tags format](http://ctags.sourceforge.net/FORMAT)
used by Vim and [many other editors](http://en.wikipedia.org/wiki/Ctags#Editors_that_support_ctags)
This adds very useful semantic hints for symbols, such as basic type, global or file scope, belonging to what
struct, etc.

Although [Exuberant ctags](http://ctags.sourceforge.net/) is the most commonly used implementation, supporting
41 programming languages, it does not do Lua very well.  It only does functions, and always collects the module
and the function together (e.g 'tablex.imap') as the 'tag'.  No extended type information is provided, and no
indication of file scope.

Invocation is easy - this script only needs Lua (5.1 or 5.2) and is to be passed the filenames to be processed.
On Windows, a single wildcard argument will be expanded.

As with `ctags`, a single file 'tags' is generated in the directory where `ltags` is invoked.
