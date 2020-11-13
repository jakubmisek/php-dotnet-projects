> Motto: "Every business should have a detection script to detect mobile readers."

#### About

Mobile Detect is a lightweight PHP class for detecting mobile devices (including tablets).
It uses the User-Agent string combined with specific HTTP headers to detect the mobile environment.

*Why*

Your website's _content strategy_ is important! You need a complete toolkit to deliver an experience that is _optimized_, 
_fast_ and _relevant_ to your users. Mobile Detect class is a 
[server-side detection](http://www.w3.org/TR/mwabp/#bp-devcap-detection) tool that can help you with your RWD strategy, 
it is not a replacement for CSS3 media queries or other forms of client-side feature detection.

*How*

We're committed to make Mobile_Detect the best open-source mobile detection resource and this is why before 
each release we're running [unit tests](https://github.com/serbanghita/Mobile-Detect/tree/master/tests) and research and update the detection rules on **monthly** basis.

*Who*

See [the history](https://github.com/serbanghita/Mobile-Detect/blob/master/docs/HISTORY.md) of the project.

#### Example

```c#
var detect = new Mobile_Detect(new PhpArray() { }, "Mozilla/5.0 (iPad; U; CPU OS 3_2_1 like Mac OS X; en-us) AppleWebKit/531.21.10 (KHTML, like Gecko) Mobile/7B405");

var isMobile = (bool)md.isMobile();
var isTablet = (bool)md.isTablet();

var knownBrowsers = (PhpArray)Mobile_Detect.getBrowsers(ContextExtensions.CurrentContext);
```

#### Announcements

* **JetBrains** is sponsoring the project by providing licenses for [PHPStorm](https://www.jetbrains.com/phpstorm/) and 
[DataGrip](https://www.jetbrains.com/datagrip/).
* **Mobile_Detect `2.x.x`** is only integrating new regexes, User-Agents and tests. We are focusing on **new tablets only**. 
The rest of the PRs about TVs, bots or optimizations will be closed and analyzed after `3.0.0-beta` is released.
* **Mobile_Detect `3.x.x`** is experimental and WIP.


#### Contribute

*Submit a PR*
> Submit a pull request but before make sure you read [how to contribute](https://github.com/serbanghita/Mobile-Detect/blob/master/docs/CONTRIBUTING.md) guide.

*Donate*

|Paypal|
|------|
|[Donate :+1:](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=mobiledetectlib%40gmail%2ecom&lc=US&item_name=Mobile%20Detect&currency_code=USD&bn=PP%2dDonationsBF%3abtn_donate_SM%2egif%3aNonHosted)|


I'm currently paying for hosting and spend a lot of my family time to maintain the project and planning the future releases.
I would highly appreciate any money donations that will keep the research going.

Special thanks to the community :+1: for donations, JetBrains team for the continuous support and [Dragos Gavrila](https://twitter.com/grafician) who contributed with the logo.
