**HTML Purifier**

HTML Purifier is an HTML filtering solution that uses a unique combination
of robust whitelists and aggressive parsing to ensure that not only are
XSS attacks thwarted, but the resulting HTML is standards compliant.

HTML Purifier is oriented towards richly formatted documents from
untrusted sources that require CSS and a full tag-set.  This library can
be configured to accept a more restrictive set of tags, but it won't be
as efficient as more bare-bones parsers. It will, however, do the job
right, which may be more important.

HTML Purifier can be found on the web at: [http://htmlpurifier.org/](http://htmlpurifier.org/)

## Samples

```c#
// quickly purify HTML string
var purifier = new HTMLPurifier(default);
var clean_html = purifier.purify("<html><title>ahoj</title>");
```

```c#
// using configuration object
using var ctx = Context.CreateEmpty();

var config = HTMLPurifier_Config.createDefault(ctx);
var purifier = new HTMLPurifier(PhpValue.FromClass(config));

var clean_html = purifier.purify("<html><title>ahoj</title>");
```
