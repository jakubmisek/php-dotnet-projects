**Stand-alone diff implementation.**

## Generating diff

The `Differ` class can be used to generate a textual representation of the difference between two strings:

```c#
using SebastianBergmann.Diff;

var differ = new Differ();
Console.WriteLine( differ.diff("foo", "bar") );
```

The code above yields the output below:

```diff
--- Original
+++ New
@@ @@
-foo
+bar
```

There are three output builders available in this package:

#### UnifiedDiffOutputBuilder

This is default builder, which generates the output close to `udiff` and is used by PHPUnit.

```c#
using SebastianBergmann.Diff;
using SebastianBergmann.Diff.Output;

var builder = new UnifiedDiffOutputBuilder(
    "--- Original
+++ New
", // custom header
    false                      // do not add line numbers to the diff 
);

var differ = new Differ(builder);
Console.WriteLine( $differ.diff("foo", "bar") );
```

#### StrictUnifiedDiffOutputBuilder

Generates (strict) Unified diff's (unidiffs) with hunks,
similar to `diff -u` and compatible with `patch` and `git apply`.

```c#
using SebastianBergmann.Diff;
using SebastianBergmann.Diff.Output;

var builder = new StrictUnifiedDiffOutputBuilder(new PhpArray() {
    { "collapseRanges", true }, // ranges of length one are rendered with the trailing `,1`
    { "commonLineThreshold", 6},    // number of same lines before ending a new hunk and creating a new one (if needed)
    { "contextLines", 3 },    // like `diff:  -u, -U NUM, --unified[=NUM]`, for patch/git apply compatibility best to keep at least @ 3
    { "fromFile", PhpValue.Null },
    { "fromFileDate", PhpValue.Null },
    { "toFile", PhpValue.Null },
    { "toFileDate", PhpValue.Null },
});

var differ = new Differ(builder);
Console.WriteLine( differ.diff("foo", "bar") );
```

#### DiffOnlyOutputBuilder

Output only the lines that differ.

```c#
using SebastianBergmann.Diff;
using SebastianBergmann.Diff.Output;

var builder = new DiffOnlyOutputBuilder(
    "--- Original
+++ New
"
);

var differ = new Differ(builder);
Console.WriteLine( differ.diff("foo", "bar") );
```

#### DiffOutputBuilderInterface

You can pass any output builder to the `Differ` class as longs as it implements the `DiffOutputBuilderInterface`. 

## Parsing diff

The `Parser` class can be used to parse a unified diff into an object graph:

```c#
using SebastianBergmann.Diff;
// using SebastianBergmann;

// var git = new Git('/usr/local/src/money');

//var diff = git.getDiff(
//  "948a1a07768d8edd10dcefa8315c1cbeffb31833",
//  "c07a373d2399f3e686234c4f7f088d635eb9641b"
//);

var parser = new Parser();
var diff = parser.parse(diff);
```

The code above returns `ICollection` of `SebastianBergmann.Diff.Diff` objects.
