                            ━━━━━━━━━━━━━━━━
                             TELEPHONE LINE
                            ━━━━━━━━━━━━━━━━


[file:https://img.shields.io/badge/license-GPL_3-green.svg]
[file:http://melpa.org/packages/telephone-line-badge.svg]
[file:http://stable.melpa.org/packages/telephone-line-badge.svg]

<./screenshots/abs.png>

<./screenshots/cubed.png>

<./screenshots/gradient.png>

<./screenshots/rainbow.png>

For more information on how to get those screenshots, check out [the
examples].


[file:https://img.shields.io/badge/license-GPL_3-green.svg]
<http://www.gnu.org/licenses/gpl-3.0.txt>

[file:http://melpa.org/packages/telephone-line-badge.svg]
<http://melpa.org/#/telephone-line>

[file:http://stable.melpa.org/packages/telephone-line-badge.svg]
<http://stable.melpa.org/#/telephone-line>

[the examples] <./examples.org>


1 Features
══════════

  Telephone Line is a new implementation of Powerline for emacs with
  *(optional) baked-in evil support*, *antialiased separators*, and an
  *easy configuration language* which makes it *trivial to write your
  own themes*. Additionally, I *dogfood the hell out of it* so bugfixes
  should come quickly. It's also *[named after a song]* which is what I
  always look for in software.


[named after a song] <https://www.youtube.com/watch?v=77R1Wp6Y_5Y>


2 Installation
══════════════

  The easiest way to install telephone-line is with package.el through
  MELPA. Once you have the package installed, initializing it is the
  usual stuff:

  ┌────
  │ (require 'telephone-line)
  │ (telephone-line-mode 1)
  └────


3 Separator Gallery
═══════════════════

  abs

  <./screenshots/separators/telephone-line-abs-left.png>
  <./screenshots/separators/telephone-line-abs-hollow-left.png>

  cubed

  <./screenshots/separators/telephone-line-cubed-left.png>
  <./screenshots/separators/telephone-line-cubed-hollow-left.png>

  identity

  <./screenshots/separators/telephone-line-identity-left.png>
  <./screenshots/separators/telephone-line-identity-hollow-left.png>

  sin

  <./screenshots/separators/telephone-line-sin-left.png>
  <./screenshots/separators/telephone-line-sin-hollow-left.png>

  halfsin

  <./screenshots/separators/telephone-line-halfsin-left.png>
  <./screenshots/separators/telephone-line-halfsin-hollow-left.png>

  cos

  <./screenshots/separators/telephone-line-cos-left.png>
  <./screenshots/separators/telephone-line-cos-hollow-left.png>

  halfcos

  <./screenshots/separators/telephone-line-halfcos-left.png>
  <./screenshots/separators/telephone-line-halfcos-hollow-left.png>

  tan

  <./screenshots/separators/telephone-line-tan-left.png>
  <./screenshots/separators/telephone-line-tan-hollow-left.png>

  gradient

  <./screenshots/separators/telephone-line-gradient.png>

  There is also a perfectly flat vertical separator,
  `telephone-line-flat', though there's not much to look at here ;)


4 Configuration
═══════════════

  First, remember that all configuration must be done *before* calling
  `(telephone-line-mode 1)'

  Segments can be added by configuring the `telephone-line-lhs' and
  `telephone-line-rhs' variables. Example configuration demonstrating
  the format can be found in <./examples.org>, and available segments
  are in <./telephone-line-segments.el>. You can also make your own!

  Separators are chosen by configuring
  `telephone-line-primary-left-separator',
  `telephone-line-primary-right-separator',
  `telephone-line-secondary-left-separator', and
  `telephone-line-secondary-right-separator'. Available separators are
  in <./telephone-line-separators.el>. You can also make your own!

  You can force the height of the mode-line by setting
  `telephone-line-height'.

  If you want to further information on configuration or creating your
  own segments/separators, continue on to <./configuration.org>!
