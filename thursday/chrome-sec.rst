=============================
Chrome Security Special Sauce
=============================

:Authors: Parisa
:Time: 10:40
:Session:
:Link:
:Slides:

"A few of the key ingredients in teh Chrome browser tha help keep you
safe on the web."

Disclaimers:

* I'm not a developer
* This talk will not make you a better developer
* This is a new talk :)

Working on Chrome's Security engineering team; originally at Google as
an engineer working to break web applications. Chrome was built with
three core principles: speed, simplicity, and security. So Security in
Chrome is a core focus of the team.

The security team is about 20 full engineers. They are responsible for
designing and implementing security features, finding security bugs,
and reponding to vulnerabilities.

Browser security is important, and its role is growing. Internet crime
continues to rise: attackers have easy, remote access to systems, and
lots of users [targets]. Browser software is particularly hard to
secure: huge user base (for something like Chrome), lots of untrusted
content, and it's very complex.

Browser Exploits
================

Browser exploits are malicious code that aims to acheive remote code
execution on a victim's computer by exploiting some bug in the browsre
itself. These may target plugins like Flash, PDF, and Java, not just
the browser proper. The Chrome team works to thwart these attacks by
finding and fixing bugs, and acknowledging the reality of the
situation.

The Chrome team uses Fuzzing to find bugs in the browser itself.
Fuzzing involves throwing random(-ish) data at a program in an attempt
to see if it will crash. The most basic fuzzer could just read from
``/dev/urandom`` and pipe to the program, but it can by optimized. For
example, figuring out how to cover more LOCs, fuzzing over multiple
cores, and ensuring you can reproduce the bug. Additionally, while you
*could* just throw random data at the program, that's probably going
to fail way too early to be interesting. Starting from a valid input
(ie, a correct protocol request) and then varying parameters might be
more interesting.

Google also pays security researches a bounty for discovering and
responsibly reporting bugs. The bounty program runs over time. Google
has also sponsored rewards for proof of concept exploits: running
untrusted code by just opening a web page.

In addition to fixing bugs, it's critical for users to actually
download and install updates.

[Shows graph of version deployment over time; obvious that users are
using the auto-update feature.]

Bugs will always exist, so it's important to architect the software
with Defense In Depth. Chrome was the first browser to use process
sandboxing for individual pages/components. This means that an
exploited bug in one area doesn't lead to a compromise of the entire
browser.

Chrome sandboxes plugins like Flash and its PDF Reader, but not all
plugins can be sandboxed. To address this potential vulnerability --
as well as the use of outdated, potentially vulnerable plugins --
Chrome has different plugin blocking features (click to run, etc).

Phising & Malware Sites
=======================

Safe Browsing warns users when they're visiting a page that Google
believes to contain malware or be phishing.
