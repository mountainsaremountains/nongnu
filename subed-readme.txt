subed
═════

  subed is an Emacs major mode for editing subtitles while playing the
  corresponding media file with [mpv]. At the moment, the only supported
  formats are:

  • SubRip ( `.srt')
  • WebVTT ( `.vtt' )
  • Advanced SubStation Alpha ( `.ass', experimental )
  • Tab-separated values ( `.tsv', experimental ) - as exported by
    Audacity for labels. TSVs are not recognized automatically because
    it's a common data format, but you can use `subed-tsv-mode' to turn
    it on in a buffer.

  <file:https://raw.githubusercontent.com/sachac/subed/master/screenshot.jpg>

  <file:word-data-and-waveform.png>


[mpv] <https://mpv.io/>

Features
────────

  • Jump to next (`M-n') and previous (`M-p') subtitle text.
  • Jump to the beginning (`C-M-a') and end (`C-M-e') of the current
    subtitle's text.
  • Merge subtitles with `M-m' (`subed-merge-dwim') and split them with
    `M-.' (`subed-split-subtitle'). If the media file is playing in MPV,
    use the current playback position. If not, use the relative position
    in the subtitle text, or other functions listed in
    `subed-split-subtitle-timestamp-functions'.
  • Insert subtitles evenly spaced throughout the available space
    (`M-i') or right next to the current subtitle (`C-M-i').  A prefix
    argument controls how many subtitles to insert and whether they are
    inserted before or after the current subtitle.
  • Kill subtitles (`M-k').
  • Adjust subtitle start (`M-[' / `M-]' or `C-M-[' / `C-M-]' if Emacs
    lives in a terminal) and stop (`M-{' / `M-}') time.  A prefix
    argument sets the number of milliseconds for the current session
    (e.g. `C-u 1000 M-[ M-[ M-[' decreases start time by 3 seconds).
  • Move the current subtitle or all marked subtitles
    (`subed-move-subtitles') forward (`C-M-n') or backward (`C-M-p') in
    time without changing subtitle duration.  A prefix argument sets the
    number of milliseconds for the current session (e.g. `C-u 500 C-M-n
    C-M-n' moves the current subtitle 1 second forward).
  • Shift the current subtitle together with all following subtitles
    using (`subed-shift-subtitles'), or shift them forward (`C-M-f') or
    backward (`C-M-b').  This is basically a convenience shortcut for
    `C-SPC M-> C-M-n/p'.  This is handy for correcting sync delays where
    the subtitles are correctly spaced but are offset from the audio.
  • Scale all subtitles or all marked subtitles forward (`C-M-x') or
    backward (`C-M-S-x') in time without changing subtitle duration.  A
    prefix argument sets the number of milliseconds for the current
    session (e.g. `C-u 500 C-M-x' moves the last [or last marked]
    subtitle forward 500ms and proportionally scales all [or all marked]
    subtitles based on this time extension.  Similarly, `C-u 500
    C-M-S-x' moves the last [or last marked] subtitle backward 500ms and
    proportionally scales all [or all marked] subtitles based on this
    time contraction).  This can be extremely useful to correct
    synchronization issues in existing subtitle files.  First, adjust
    the starting time if necessary (e.g. `C-M-f'), then adjust the
    ending and scale constituent subtitles (e.g. `C-M-x').
  • Show CPS (characters per second) for the current subtitle.
  • Insert HTML-like tags (`C-c C-t C-t', with an optional attribute
    when prefixed by `C-u'), in particular italics (`C-c C-t C-i') or
    boldface (`C-c C-t C-b').
  • SRT: Sort and re-number subtitles and remove any extra spaces and
    newlines (`M-s'). This is done automatically every time the buffer
    is saved.
  • Trim subtitle overlaps with `M-x subed-trim-overlaps'. By default,
    this adjusts the stop time of overlapping subtitles to
    `subed-subtitle-spacing' milliseconds before the next subtitle
    starts. Use `M-x customize-group' `subed' to configure trimming to
    happen automatically when buffers are loaded or saved, which time is
    adjusted, and how much time to leave between subtitles.
  • Convert between formats with `M-x subed-convert'.
  • Show the waveform (`M-x subed-waveform-minor-mode', off by default)
    extracted from the media file using `ffmpeg' with the start/stop
    positions of the current subtitle and the current position in MPV
    marked along with the subtitle.  Change the "volume" of the waveform
    (i.e., the /visible/ amplitude) with `C-c C--' and `C-c C-='.
    Redisplay the waveform with `C-c |'.  Left/right-click on the
    waveform to set the start/stop timestamps. If you would like to
    display the waveform automatically when you open a file, you can add
    `(add-hook 'subed-mode-hook 'subed-waveform-minor-mode)' to your
    configuration.
  • Load word timing data (ex: SRV2) using `M-x
      subed-word-data-load-from-file'. This will be used for splitting
      words at timestamps when available.
  • Use `M-x subed-align' and [aeneas] to align your text or subtitles
    with an audio file in order to get timestamps.


[aeneas] <https://www.readbeyond.it/aeneas/>

mpv integration (optional)
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  Using network sockets to control MPV works on Linux and on Mac OS X,
  but not on Microsoft Windows due to the lack of Unix-style sockets. On
  Microsoft Windows, you will not be able to synchronize with MPV.

  • Automatically open the associated media file in MPV based on the
    filename, open a media file manually with `C-c C-v'
    (`subed-mpv-play-from-file'), or play media directly from a URL with
    `C-c C-u' (`subed-mpv-play-from-url') . You can customize the
    automatic detection of files by changing `subed-video-extensions'
    and `subed-audio-extensions'.
  • Pause and resume playback without leaving Emacs (`M-SPC').
  • Jump to the current subtitle in the MPV player with `M-j'
    (`subed-mpv-jump-to-current-subtitle'). Toggle looping over the
    current subtitle with `C-c C-l'
    (`subed-toggle-loop-over-current-subtitle').  Control how many
    seconds to loop before or after the current subtitles by customizing
    `subed-loop-seconds-before' and `subed-loop-seconds-after'.
  • Use `C-c .' (`subed-toggle-sync-point-to-player') to toggle whether
    the point should move to the currently playing subtitle.
  • Use `C-c ,' (`subed-toggle-sync-player-to-point') to toggle whether
    mpv should seek to the position of the current subtitle when the
    point moves between subtitles.
  • Subtitles are automatically reloaded in mpv when the buffer is
    saved.
  • Copy the current playback position as start (`C-c [') or stop (`C-c
    ]') time of the current subtitle.
  • Playback is paused or slowed down when a subtitle's text is edited
      (`C-c C-p', `subed-toggle-pause-while-typing').
  • Loop over the current subtitle in mpv (`C-c C-l').
  • When a subtitle's start or stop time changes, mpv seeks to the
    subtitle's start time (`C-c C-r',
    `subed-toggle-replay-adjusted-subtitle').
  • Move one frame forward or backward (`C-c C-f .' and `C-c C-f ,';
    pressing `,' or `.' afterwards moves by frames until any other key
    is pressed).


Installation
────────────

Installing the subed package from NonGNU Elpa
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  `subed' is now on [NonGNU ELPA].  On Emacs 28 and later, you can
  install it with `M-x package-install' `subed'.

  To install it on Emacs 27 or earlier, add the following to your Emacs
  configuration file:

  ┌────
  │ (with-eval-after-load 'package (add-to-list 'package-archives '("nongnu" . "https://elpa.nongnu.org/nongnu/")))
  └────

  Use `M-x eval-buffer' to run the code, use `M-x
  package-refresh-contents' to load the package archives, and then use
  `M-x package-install' `subed'.

  Sample configuration:

  ┌────
  │ (with-eval-after-load 'subed-mode
  │ 	;; Remember cursor position between sessions
  │ 	(add-hook 'subed-mode-hook 'save-place-local-mode)
  │ 	;; Break lines automatically while typing
  │ 	(add-hook 'subed-mode-hook 'turn-on-auto-fill)
  │ 	;; Break lines at 40 characters
  │ 	(add-hook 'subed-mode-hook (lambda () (setq-local fill-column 40)))
  │ 	;; Some reasonable defaults
  │ 	(add-hook 'subed-mode-hook 'subed-enable-pause-while-typing)
  │ 	;; As the player moves, update the point to show the current subtitle
  │ 	(add-hook 'subed-mode-hook 'subed-enable-sync-point-to-player)
  │ 	;; As your point moves in Emacs, update the player to start at the current subtitle
  │ 	(add-hook 'subed-mode-hook 'subed-enable-sync-player-to-point)
  │ 	;; Replay subtitles as you adjust their start or stop time with M-[, M-], M-{, or M-}
  │ 	(add-hook 'subed-mode-hook 'subed-enable-replay-adjusted-subtitle)
  │ 	;; Loop over subtitles
  │ 	(add-hook 'subed-mode-hook 'subed-enable-loop-over-current-subtitle)
  │ 	;; Show characters per second
  │ 	(add-hook 'subed-mode-hook 'subed-enable-show-cps))
  └────


[NonGNU ELPA] <https://elpa.nongnu.org/nongnu/subed.html>


Manual installation
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  If that doesn't work, you can install it manually. To install from the
  main branch:

  ┌────
  │ git clone https://github.com/sachac/subed.git
  └────

  This will create a `subed' directory with the code.

  If you have the `make' utility, you can regenerate the autoload
  definitions with

  ┌────
  │ make autoloads
  └────

  If you don't have `make' installed, you can generate the autoloads
  with:

  ┌────
  │ emacs --quick --batch --eval "(progn (setq generated-autoload-file (expand-file-name \"subed-autoloads.el\" \"subed\") backup-inhibited t) \
  │ 	(update-directory-autoloads \"./subed\"))"
  └────

  Then you can add the following to your Emacs configuration (typically
  `~/.config/emacs/init.el', `~/.emacs.d/init.el', or `~/.emacs'; you
  can create this file if it doesn't exist yet). Here's a configuration
  example:

  ┌────
  │ ;; Note the reference to the subed subdirectory, instead of the one at the root of the checkout
  │ (add-to-list 'load-path "/path/to/subed/subed")
  │ (require 'subed-autoloads)
  │ 
  │ (with-eval-after-load 'subed-mode
  │ 	;; Remember cursor position between sessions
  │ 	(add-hook 'subed-mode-hook 'save-place-local-mode)
  │ 	;; Break lines automatically while typing
  │ 	(add-hook 'subed-mode-hook 'turn-on-auto-fill)
  │ 	;; Break lines at 40 characters
  │ 	(add-hook 'subed-mode-hook (lambda () (setq-local fill-column 40)))
  │ 	;; Some reasonable defaults
  │ 	(add-hook 'subed-mode-hook 'subed-enable-pause-while-typing)
  │ 	;; As the player moves, update the point to show the current subtitle
  │ 	(add-hook 'subed-mode-hook 'subed-enable-sync-point-to-player)
  │ 	;; As your point moves in Emacs, update the player to start at the current subtitle
  │ 	(add-hook 'subed-mode-hook 'subed-enable-sync-player-to-point)
  │ 	;; Replay subtitles as you adjust their start or stop time with M-[, M-], M-{, or M-}
  │ 	(add-hook 'subed-mode-hook 'subed-enable-replay-adjusted-subtitle)
  │ 	;; Loop over subtitles
  │ 	(add-hook 'subed-mode-hook 'subed-enable-loop-over-current-subtitle)
  │ 	;; Show characters per second
  │ 	(add-hook 'subed-mode-hook 'subed-enable-show-cps))
  └────

  You can reload your configuration with `M-x eval-buffer' or restart
  Emacs.

  If you want to try a branch (ex: `derived-mode'), you can use the
  following command inside the `subed' directory:

  ┌────
  │ git checkout branchname
  └────


use-package configuration
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  Here's an example setup if you use [use-package]:

  ┌────
  │ (use-package subed
  │ 	:ensure t
  │ 	:config
  │ 	;; Remember cursor position between sessions
  │ 	(add-hook 'subed-mode-hook 'save-place-local-mode)
  │ 	;; Break lines automatically while typing
  │ 	(add-hook 'subed-mode-hook 'turn-on-auto-fill)
  │ 	;; Break lines at 40 characters
  │ 	(add-hook 'subed-mode-hook (lambda () (setq-local fill-column 40)))
  │ 	;; Some reasonable defaults
  │ 	(add-hook 'subed-mode-hook 'subed-enable-pause-while-typing)
  │ 	;; As the player moves, update the point to show the current subtitle
  │ 	(add-hook 'subed-mode-hook 'subed-enable-sync-point-to-player)
  │ 	;; As your point moves in Emacs, update the player to start at the current subtitle
  │ 	(add-hook 'subed-mode-hook 'subed-enable-sync-player-to-point)
  │ 	;; Replay subtitles as you adjust their start or stop time with M-[, M-], M-{, or M-}
  │ 	(add-hook 'subed-mode-hook 'subed-enable-replay-adjusted-subtitle)
  │ 	;; Loop over subtitles
  │ 	(add-hook 'subed-mode-hook 'subed-enable-loop-over-current-subtitle)
  │ 	;; Show characters per second
  │ 	(add-hook 'subed-mode-hook 'subed-enable-show-cps)
  │ 	)
  └────


[use-package] <https://github.com/jwiegley/use-package>


straight configuration
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  If you use [straight.el], you can install subed with the following
  recipe:

  ┌────
  │ (straight-use-package '(subed :type git :host github :repo "sachac/subed" :files ("subed/*.el")))
  └────


[straight.el] <https://github.com/radian-software/straight.el>


Getting started
───────────────

  `C-h f subed-mode' should get you started. This is the parent mode for
  `subed-srt-mode', `subed-vtt-mode', and `subed-ass-mode'. When
  manually loading a mode, use those specific format modes instead of
  `subed-mode'.


Some workflow ideas
───────────────────

Reflowing subtitles into shorter or longer lines
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  You may want to use `set-fill-column' and
  `display-fill-column-indicator-mode' to show the target number of
  characters.

  Use `subed-split-subtitle' (`M-.'), `subed-merge-dwim' (`M-b'), and
  `subed-merge-with-previous' (`M-M') to split lines.

  Splitting will use the current MPV position if available. If not, it
  will guess where to split based on the the number of characters in the
  subtitle. You can use `subed-mpv-jump-to-current-subtitle' (`M-j') to
  play the current subtitle manually and use `subed-mpv-toggle-pause'
  (`M-SPC') to stop at the right time. Use
  `subed-toggle-loop-over-current-subtitle' (`C-c C-l') if you want to
  keep looping. `subed-waveform-show-current' can help you fine-tune the
  split.


Adjusting timestamps
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  You can use `subed-mpv-jump-to-current-subtitle' (`M-j') to play the
  current subtitle manually. Use
  `subed-mpv-jump-to-current-subtitle-near-end' (`M-J') to jump to near
  the end of the subtitle in order to test it. Use
  `subed-toggle-loop-over-current-subtitle' (`C-c C-l') if you want to
  keep looping automatically. Use `subed-mpv-toggle-pause' (`M-SPC') to
  stop at the right time.

  `subed-waveform-show-current' or `subed-waveform-show-all' can be
  useful for adjusting start and end timestamps. Use
  `subed-waveform-set-start' (`mouse-1', which is left click) or
  `subed-waveform-set-stop' (`mouse-3', which is right-click) to adjust
  only the current subtitle's timestamps, or use
  `subed-waveform-set-start-and-copy-to-previous' (`S-mouse-1' or
  `M-mouse-1') or `subed-waveform-set-stop-and-copy-to-next'
  (`S-mouse-3' or `M-mouse-3') to adjust adjacent subtitles as well.

  You can also manually adjust

  • subtitle start: `M-[' / `M-]'
  • subtitle stop: (`M-{' / `M-}')

  A prefix argument sets the number of milliseconds (e.g. `C-u 1000 M-[
  M-[ M-[' decreases start time by 3 seconds).


Editing subtitles
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  You can use `subed-mpv-jump-to-current-subtitle' (`M-j') to play the
  current subtitle and use `subed-mpv-toggle-pause' (`M-SPC') to stop at
  the right time.  Use `subed-toggle-loop-over-current-subtitle' (`C-c
  C-l') if you want to keep looping automatically.

  If you have wdiff installed, you can use
  `subed-wdiff-subtitle-text-with-file' to compare the subtitle text
  with a script or another subtitle file.


Writing subtitles from scratch
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  One way is to start with one big subtitle that covers the whole media
  file, and then split it using `subed-split-subtitle' (`M-.').

  Another way is to type as much of the text as you can without worrying
  about timestamps, putting each caption on a separate line. Then you
  can use `subed-align' to convert it into timestamped captions.


Timing / resynchronizing subtitles
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  If you're using `subed-waveform-show-current' or
  `subed-waveform-show-all', you can use `M-mouse-2' (Meta-middle-click,
  `subed-waveform-shift-subtitles') to shift the current subtitle and
  succeeding subtitles so that they start at the position you clicked
  on.

  To do this with the keyboard, you can use
  `subed-shift-subtitles-to-start-at-timestamp' if you want to specify a
  timestamp or `subed-shift-subtitles' to specify a millisecond offset.

  To use word timing data from something like WhisperX, load
  subed-word-data.el and then use `subed-word-data-load-from-file'. The
  word times will then be used when you split subtitles with
  `subed-split-subtitle'.

  Rodrigo Morales also has some functions for [playing part of the
  subtitles and changing them by a little bit].


[playing part of the subtitles and changing them by a little bit]
<https://rodrigo.morales.pe/2024/11/17/my-subed-configuration-for-adding-subtitles-to-emacsconf-2024/>


Exporting text for review
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  You can use `subed-copy-region-text' to copy the text of the subtitles
  for pasting into another buffer. Call it with the universal prefix
  `C-u' to copy comments as well.


Troubleshooting
───────────────

subed-mpv: Service name too long
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  If `subed-mpv-client' reports `(error "Service name too long")', this
  is probably because the path to the socket used to communicate with
  MPV is too long for your operating system. You can use `M-x customize'
  to set `subed-mpv-socket-dir' to a shorter path.


Important change in v1.0.0
──────────────────────────

  `subed' now uses `subed-srt-mode', `subed-vtt-mode', and
  `subed-ass-mode' instead of directly using `subed-mode'. These modes
  should be automatically associated with the `.vtt', `.srt', and `.ass'
  extensions. If the generic `subed-mode' is loaded instead of the
  format-specific mode, you may get an error such as:

  ┌────
  │ Error in post-command-hook (subed--post-command-handler): (cl-no-applicable-method subed--subtitle-id)
  └────

  If you set `auto-mode-alist' manually in your config, please make sure
  you associate extensions the appropriate format-specific mode instead
  of `subed-mode'. The specific backend functions (ex:
  `subed-srt--jump-to-subtitle-id') are also deprecated in favor of
  using generic functions such as `subed-jump-to-subtitle-id'.


Testing
───────

  You'll need to install the `buttercup' and `package-lint' Emacs
  packages. You'll also need `GNU Make' so that you can work with
  Makefiles. To run the tests, use the command `make test'.


Contributions
─────────────

  Contributions would be really appreciated! subed conforms to the
  [REUSE Specification]; this means that every file has copyright and
  license information. If you modify a file, please update the year
  shown after `SPDX-FileCopyrightText'. Thank you!

  There's a list of authors in the file `AUTHORS.org'. If you have at
  any point contributed to subed, you are most welcome to add your name
  (and email address if you like) to the list.


[REUSE Specification] <https://reuse.software/spec/>


License
───────

  subed is free software: you can redistribute it and/or modify it under
  the terms of the GNU General Public License as published by the Free
  Software Foundation, either version 3 of the License, or (at your
  option) any later version.

  This program is distributed in the hope that it will be useful but
  WITHOUT ANY WARRANTY; without even the implied warranty of
  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the [GNU
  General Public License] for more details.


[GNU General Public License] <https://www.gnu.org/licenses/gpl-3.0.txt>


Build tips
══════════

  Here's a post-commit hook that will make it easier to remember to tag
  releases:

  ┌────
  │ #!/usr/bin/python
  │ 
  │ # place in .git/hooks/post-commit
  │ # Based on https://gist.github.com/ajmirsky/1245103
  │ 
  │ import subprocess
  │ import re
  │ 
  │ print("checking for version change...",)
  │ 
  │ output = subprocess.check_output(['git', 'diff', 'HEAD^', 'HEAD', '-U0']).decode("utf-8")
  │ 
  │ version_info = None
  │ for d in output.split("\n"):
  │     rg = re.compile(r'\+(?:;;\s+)?Version:\s+(?P<major>[0-9]+)\.(?P<minor>[0-9]+)\.(?P<rev>[0-9]+)')
  │     m = rg.search(d)
  │     if m:
  │ 	version_info = m.groupdict()
  │ 	break
  │ 
  │ if version_info:
  │     tag = "v%s.%s.%s" % (version_info['major'], version_info['minor'], version_info['rev'])
  │     existing = subprocess.check_output(['git', 'tag']).decode("utf-8").split("\n")
  │     if tag in existing:
  │ 	print("%s is already tagged, not updating" % tag)
  │     else:
  │ 	result = subprocess.run(['git', 'tag', '-f', tag])
  │ 	if result.returncode:
  │ 	    raise Exception('tagging not successful: %s %s' % (result.stdout, result.returncode))
  │ 	print("tagged revision: %s" % tag)
  │ else:
  │     print("none found.")
  └────


Other resources
═══════════════

  • [My subed customizations for editing captions of Emacsconf 2024 –
    Rodrigo Morales]
  • [Sacha Chua's subed-related blog posts]
  • [Marcin Borkowski: 2023-09-18 Making Anki flashcards from subtitles]
  • [sachac/subed-record: Record audio in segments and compile it into a
    file]
  • [EmacsConf - Captioning tips]


[My subed customizations for editing captions of Emacsconf 2024 –
Rodrigo Morales]
<https://rodrigo.morales.pe/2024/11/17/my-subed-configuration-for-adding-subtitles-to-emacsconf-2024/>

[Sacha Chua's subed-related blog posts]
<https://sachachua.com/blog/category/subed>

[Marcin Borkowski: 2023-09-18 Making Anki flashcards from subtitles]
<https://mbork.pl/2023-09-18_Making_Anki_flashcards_from_subtitles>

[sachac/subed-record: Record audio in segments and compile it into a
file] <https://github.com/sachac/subed-record>

[EmacsConf - Captioning tips] <https://emacsconf.org/captioning/>
