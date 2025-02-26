[file:https://travis-ci.org/bastibe/org-journal.svg?branch=master]
[https://elpa.nongnu.org/nongnu/org-journal.svg]
[file:http://melpa.org/packages/org-journal-badge.svg]
[file:http://stable.melpa.org/packages/org-journal-badge.svg]

<./org-journal.svg>


[file:https://travis-ci.org/bastibe/org-journal.svg?branch=master]
<https://travis-ci.org/bastibe/org-journal>

[https://elpa.nongnu.org/nongnu/org-journal.svg]
<https://elpa.nongnu.org/nongnu/org-journal.html>

[file:http://melpa.org/packages/org-journal-badge.svg]
<http://melpa.org/#/org-journal>

[file:http://stable.melpa.org/packages/org-journal-badge.svg]
<http://stable.melpa.org/#/org-journal>


1 org-journal
═════════════

  Adapted from <https://www.emacswiki.org/emacs/PersonalDiary>

  Functions to maintain a simple personal diary / journal using in
  Emacs.

  Feel free to use, modify and improve the code!  — mtvoid, bastibe


1.1 Synopsis
────────────

  `org-journal' maintains a set of files, depending on the value of
  `org-journal-file-type', a file represents a day, week, month or
  year. When `org-journal-file-type' is set to `'daily', each file
  represent a day. In case `org-journal-file-type' is set to `'weekly',
  a file represents a week, etc. Convenient bindings allow the creation
  of journal records in the current daily, weekly, monthly or yearly
  file and search within all records or specified time intervals. All
  records can be browsed and searched from the Emacs Calendar for
  convenience. All entries in a specified TODO state will be carried
  over to the next day, see `org-journal-carryover-items'. Optionally,
  the journal entry can be encrypted, so can the file, see
  `org-journal-enable-encryption' and `org-journal-encrypt-journal',
  respectively.

  Every journal entry must have a *CREATED* property when using yearly,
  monthly and weekly journal files. This property is added by
  `org-journal-new-entry' automatically.

  An example of a daily file (it will actually look a lot nicer,
  depending on your org-mode settings):

  ┌────
  │ * Tuesday, 06/04/13
  │ ** 10:28 Company meeting
  │ Endless discussions about projects. Not much progress
  │ 
  │ ** 11:33 Work on org-journal
  │ For the longest time, I wanted to have a cool diary app on my
  │ computer. However, I simply lacked the right tool for that job. After
  │ many hours of searching, I finally found PersonalDiary on EmacsWiki.
  │ PersonalDiary is a very simple diary system based on the emacs
  │ calendar. It works pretty well, but I don't really like that it only
  │ uses unstructured text.
  │ 
  │ Thus, I spent the last two hours making that diary use org-mode
  │ and represent every entry as an org-mode headline. Very cool!
  │ 
  │ ** 15:33 Work on org-journal
  │ Now my journal automatically creates the right headlines (adds the
  │ current time stamp if on the current day, does not add a time stamp
  │ for any other day). Additionally, it automatically collapses the
  │ headlines in the org-file to the right level (shows everything if in
  │ view mode, shows only headlines in new-entry-mode). Emacs and elisp
  │ are really cool!
  │ 
  │ ** 16:40 Work on org-journal
  │ I uploaded my journal mode to marmalade and Github! Awesome!
  │ 
  │ ** TODO teach org-journal how to brew coffee
  └────

  An example of a weekly/monthly/yearly journal file, see also
  `org-journal-file-type'.

  ┌────
  │ * Tuesday, 06/04/13
  │   :PROPERTIES:
  │   :CREATED:  20130604
  │   :END:
  │ ** 10:28 Company meeting
  │ ...
  │ 
  │ ** 11:33 Work on org-journal
  │ ...
  │ 
  │ ** 15:33 Work on org-journal
  │ ...
  │ 
  │ ** 16:40 Work on org-journal
  │ ...
  │ 
  │ * Wednesday, 06/05/13
  │   :PROPERTIES:
  │   :CREATED:  20130605
  │   :END:
  │ ** 10:28 A new day
  │ ...
  │ 
  │ ** 11:33 Work is almost over
  │ ...
  │ 
  │ ** TODO teach org-journal how to brew coffee
  └────


1.2 Installation
────────────────

  `org-journal' is available through [NonGNU ELPA], [MELPA] and [MELPA
  Stable]. So installation should be trivial:

  ┌────
  │ M-x package-install org-journal
  └────

  Then add `(require 'org-journal)' to your `.emacs'.

  *Note!* If you are using `org-mode' version 9.6 consider customizing
   the variable `org-element-use-cache' and setting it to `nil' to
   workaround [an issue where journal items are not properly carried
   over to the next day]


[NonGNU ELPA] <https://elpa.nongnu.org/>

[MELPA] <https://melpa.org/>

[MELPA Stable] <https://stable.melpa.org/>

[an issue where journal items are not properly carried over to the next
day] <https://github.com/bastibe/org-journal/issues/406>


1.3 Quickstart
──────────────

  Doing `M-x org-journal-new-entry' will immediately create a journal
  directory in the default path (customized using the `org-journal-dir'
  variable), open or create a file in `org-journal-mode', and insert a
  template for a new journal entry.

  The same command with a prefix argument (`C-u M-x
  org-journal-new-entry') will do everything mentioned while skipping
  entry creation, which is useful for looking at the current journal
  file.


1.4 Basic Usage
───────────────

  Bindings available in `org-journal-mode':

  • `C-c C-f' - go to the next journal file.

  • `C-c C-b' - go to the previous journal file.

  • `C-c C-j' - insert a new entry into the current journal file
    (creates the file if not present).

  • `C-c C-s' - search the journal for a string.

  All journal entries are registered in the Emacs Calendar. To see
  available journal entries do `M-x calendar'. Bindings available in the
  `calendar-mode':

  • `j m' - mark entries in calendar

  • `j r' - view an entry in a new buffer.

  • `j d' - view an entry but do not switch to it.

  • `j n' - add a new entry into the day's file (creates the file if not
    present).

  • `j s w' - search in all entries of the current week.

  • `j s m' - search in all entries of the current month.

  • `j s y' - search in all entries of the current year.

  • `j s f' - search in all entries of all time.

  • `j s F' - search in all entries in the future.

  • `[' - go to previous day with journal entries.

  • `]' - go to next day with journal entries.


1.5 Setup and customization
───────────────────────────

  The following variables can be customized through `M-x customize', or
  configured programmatically in your `.init.el'.

  See below for an example.


1.5.1 Journal Directory and Files
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  Customization options related to journal directory and files:

  • `org-journal-dir' - the journal path.

  • `org-journal-file-format' - format string for journal file names
    (may contain directories relative to `org-journal-dir').

  • `org-journal-find-file' - a function to use when opening a journal
    file. By default it opens a window using
    `find-file-other-window'. Set this to `find-file' if you don't want
    org-journal to split your window.

  • `org-extend-today-until' - a number that indicates the hour of
    /your/ end of the day. If you create a new entry with
    `org-journal-new-entry' earlier than this time, the journal entry
    will go into the previous day's journal.

  • `org-journal-file-type' - the journal file type either 'daily
    (default), 'weekly, 'monthly or 'yearly.  Also see the customizable
    variables `org-journal-start-on-weekday' for changing the start of
    the week for weekly journals (defaults to Monday). Keep in mind
    changing `org-journal-start-on-weekday' won't work for existing
    weekly journal files.


1.5.2 Journal File Content
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  Customization options related to the journal file contents:

  • `org-journal-date-format' - date format `org-journal' uses when
    showing a date within a journal and search results page. It can also
    be a function, which return value will than be inserted.

  • `org-journal-date-prefix' - this string will prefix the date at the
    top of a journal file.

  • `org-journal-time-format' - a timestamp format that will prefix
    every entry within a daily journal file.

  • `org-journal-time-prefix' - a string that will prefix every entry
    within a daily journal file.

  • `org-journal-file-header' - a string that will be inserted at the
    top of every new journal file. If a string, it will be passed to
    `format-time-string` along the time value of the new journal entry.
    It can also be a function expecting a time value.

    ┌────
    │ (defun org-journal-file-header-func (time)
    │   "Custom function to create journal header."
    │   (concat
    │     (pcase org-journal-file-type
    │       (`daily "#+TITLE: Daily Journal\n#+STARTUP: showeverything")
    │       (`weekly "#+TITLE: Weekly Journal\n#+STARTUP: folded")
    │       (`monthly "#+TITLE: Monthly Journal\n#+STARTUP: folded")
    │       (`yearly "#+TITLE: Yearly Journal\n#+STARTUP: folded"))))
    │ 
    │ (setq org-journal-file-header 'org-journal-file-header-func)
    └────

  • `org-journal-hide-entries-p' - a boolean (defaults to `true') that
    will hide previous journal entries if true. Can be set to `nil' to
    show previous entries.


1.5.3 `org-journal' behavior
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  Customization options related to `org-journal' itself:

  • `org-journal-mode-hook' - List of functions to run when
    `org-journal-mode' is loaded. By default this is set to
    `'(turn-on-visual-line-mode org-journal-default-enable-encryption)'.


1.5.4 An example setup
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  A very basic example of customization.

  ┌────
  │ (setq org-journal-dir "~/org/journal/")
  │ (setq org-journal-date-format "%A, %d %B %Y")
  │ (require 'org-journal)
  └────

  For users of `use-package', this setup could look like the following:

  ┌────
  │ (use-package org-journal
  │   :ensure t
  │   :defer t
  │   :init
  │   ;; Change default prefix key; needs to be set before loading org-journal
  │   (setq org-journal-prefix-key "C-c j ")
  │   :config
  │   (setq org-journal-dir "~/org/journal/"
  │         org-journal-date-format "%A, %d %B %Y"))
  └────


1.6 Advanced Usage
──────────────────

1.6.1 Searching the Journal
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  `org-journal' has two searching options: the usual `org-mode' agenda
  search and the built-in plain text search. The former can become slow
  with bigger journals, so the built-in search is a recommended option.

  To use the agenda search, you can add all journal entries to your
  org-agenda by adding `org-journal-dir' to `org-agenda-files' and
  setting `org-agenda-file-regexp' to include files matching your
  `org-journal-file-pattern'.

  ┌────
  │ ;; When =org-journal-file-pattern= has the default value, this would be the regex.
  │ (setq org-agenda-file-regexp "\\`\\\([^.].*\\.org\\\|[0-9]\\\{8\\\}\\\(\\.gpg\\\)?\\\)\\'")
  │ (add-to-list 'org-agenda-files org-journal-dir)
  └────

  However, this can become /very/ slow if you have many journal
  entries. As a compromize, you can set
  `org-journal-enable-agenda-integration' to `t', which automatically
  adds the current and all future journal entries to the agenda. This is
  enough to get an overview over current and future tasks.

  The built-in search is available through the following function:
  `org-journal-search' (`C-c C-s' in `org-journal-mode'). By default, it
  will ask for the time interval to search within (accepting the
  `org-read-date' format such as "-1y" or "-1m") and the string to
  search for. Given a prefix argument (`C-u org-journal-search'), it
  will go through the whole journal.

  The order of the search results (ascending or descending by date) can
  be customized using the `org-journal-search-results-order-by'
  variable.

  Search is also available through the Emacs Calendar as described in
  "Basic Usage".


1.6.2 Carry Over
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  By default, `org-journal' will try to /carry over/ previous day
  TODO-marked items whenever a new journal file is created. The older
  journal entry will be inserted to the current day's file.

  This feature is controlled through the `org-journal-carryover-items'
  variable. To disable this feature set `org-journal-carryover-items' to
  an empty string `""'. Any [agenda tags view match string], tags,
  properties, and todo states are allowed. By default this is
  `TODO=”TODO”'. Which will match TODO items.

  The old carryover items in the previous day's journal are processed by
  the function assigned to `org-journal-handle-old-carryover' variable.
  Default is to remove all of them. You can change this behavior by
  assigning a custom fuction to the variable.  Your function has to take
  one argument, which is a list of old carryover entries. The list is in
  form of ((START_POINT (END_POINT . "TEXT")) … (START_POINT (END_POINT
  . "TEXT"))); and in ascending order of START_POINT.

  For example, you can choose putting a tag on the old carryover entries
  intead of removing them:

  ┌────
  │ (defun my-old-carryover (old_carryover)
  │   (save-excursion
  │     (let ((matcher (cdr (org-make-tags-matcher org-journal-carryover-items))))
  │       (dolist (entry (reverse old_carryover))
  │ 	(save-restriction
  │ 	  (narrow-to-region (car entry) (cadr entry)) 
  │ 	  (goto-char (point-min))
  │ 	  (org-scan-tags '(lambda ()
  │ 			    (org-set-tags ":carried:"))
  │ 			 matcher org--matcher-tags-todo-only))))))
  │ 
  │ (setq org-journal-handle-old-carryover 'my-old-carryover)
  └────

  You can also skip carry over of [Drawers] through the
  `org-journal-skip-carryover-drawers' variable. This is specifically
  useful when you want to skip carry over of previous days clocked
  entries when it is under the drawer `LOGBOOK'. The variable accepts a
  list of drawers names which will be skipped on carry over. Sample
  configuration for skipping `LOGBOOK' drawer:

  ┌────
  │ (setq org-journal-skip-carryover-drawers (list "LOGBOOK"))
  └────


[agenda tags view match string]
<http://orgmode.org/manual/Matching-tags-and-properties.html>

[Drawers] <https://orgmode.org/manual/Drawers.html>


1.6.3 Encryption
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  The journal entry can be encrypted using `org-crypt', to enable it set
  `org-journal-enable-encryption' to `t'.

  You can also encrypt the journal files itself by setting the variable
  `org-journal-encrypt-journal' to `t'. `org-journal' will always search
  for journal files with the `.gpg' extension, and highlights them in
  the calendar, etc., regardless of the value of
  `org-journal-encrypt-journal'.  See the info page `(info
  "(epa)Encrypting/decrypting gpg files")' for more information about
  gpg encryption in Emacs.


1.6.4 Agenda and Scheduling
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  An easy way of keeping track of appointments or future TODOs is to
  simply create a journal entry in the future. Such entries will
  automatically get a timestamp and show up in the current day's journal
  entry once you reach that day.

  • if `org-journal-enable-agenda-integration' is `t', org-journal will
    automatically add the current and all future journal entries to
    `org-agenda-files'.

  There are a few helper functions to deal with such scheduled entries:

  • `org-journal-new-scheduled-entry' - prompts for a date, and creates
    a new journal entry on that date with its timestamp set to the
    date. By default, this is a TODO entry. Set the prefix to avoid the
    TODO.

  • `org-journal-schedule-view' - creates a read-only overview of
    scheduled entries.


◊ 1.6.4.1 iCalendar export

  You can export your scheduled entries to an iCalendar file, and
  subscribe to that file in your calendar application. You need to
  enable the agenda integration for this to work. I also recommend you
  set the following values before exporting:

  ┌────
  │ (setq org-journal-enable-agenda-integration t
  │       org-icalendar-store-UID t
  │       org-icalendar-include-todo "all"
  │       org-icalendar-combined-agenda-file "~/path/to/org-journal.ics")
  └────

  With this done, you can export your agenda, including your scheduled
  entries, with `(org-icalendar-combine-agenda-files)'.


1.6.5 Journal Capture Template
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  You can configure a capture template in order to integrate
  `org-journal' with `org-capture', as in the following example for a
  daily journal:

  ┌────
  │ (defun org-journal-find-location ()
  │   ;; Open today's journal, but specify a non-nil prefix argument in order to
  │   ;; inhibit inserting the heading; org-capture will insert the heading.
  │   (org-journal-new-entry t)
  │   (unless (eq org-journal-file-type 'daily)
  │     (org-narrow-to-subtree))
  │   (goto-char (point-max)))
  │ 
  │ (setq org-capture-templates '(("j" "Journal entry" plain (function org-journal-find-location)
  │                                "** %(format-time-string org-journal-time-format)%^{Title}\n%i%?"
  │                                :jump-to-captured t :immediate-finish t)))
  └────

  If you want to do the same to schedule a task for a future date, you
  can use the following:

  ┌────
  │ (defvar org-journal--date-location-scheduled-time nil)
  │ 
  │ (defun org-journal-date-location (&optional scheduled-time)
  │   (let ((scheduled-time (or scheduled-time (org-read-date nil nil nil "Date:"))))
  │     (setq org-journal--date-location-scheduled-time scheduled-time)
  │     (org-journal-new-entry t (org-time-string-to-time scheduled-time))
  │     (unless (eq org-journal-file-type 'daily)
  │       (org-narrow-to-subtree))
  │     (goto-char (point-max))))
  │ 
  │ (setq org-capture-templates '(("j" "Journal entry" plain (function org-journal-date-location)
  │                                "** TODO %?\n <%(princ org-journal--date-location-scheduled-time)>\n"
  │                                :jump-to-captured t))
  └────


1.6.6 Caching of journal dates
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  Since version 2.0.0 a cache has been added to speed up calendar
  operations. This should drastically improve the performance when using
  encrypted journal files, see `org-journal-encrypt-journal'.

  The caching functionality can be enabled by settings
  `org-journal-enable-cache' to `t'. The cache can be reset by calling
  `org-journal-invalidate-cache'.


1.7 FAQ
───────

1.7.1 Can I use weekly/monthly/yearly journal entries instead of daily ones?
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  Yes, see `org-journal-file-type'.


1.7.2 Can I have multiple journals?
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  At the moment, this is not possible. But it should be possible to
  switch the value of `org-journal-directory' using a custom function or
  directory local variables.


1.7.3 Can I use org-journal with Spacemacs?
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  Yes you can!

  • To use `org-journal' with Spacemacs from the `master' branch, you
    must do this:

    1. `git clone https://github.com/borgnix/spacemacs-journal.git
       ~/.emacs.d/private/journal'
    2. add it to your `~/.spacemacs'. You will need to add `journal' to
       the existing `dotspacemacs-configuration-layers' list in this
       file.

    The manual of the journal layer can be found at
    <https://github.com/borgnix/spacemacs-journal>

  • If you use Spacemacs from the `develop' branch you can enable
    `org-journal' by setting `org-enable-org-journal-support' to `t',
    see [Spacemacs org-journal support].


[Spacemacs org-journal support]
<https://github.com/syl20bnr/spacemacs/tree/develop/layers/+emacs/org#org-journal-support>


1.7.4 Some key-bindings in org-journal conflict with org-mode key bindings
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  Minor modes are supposed to only use key bindings of the form `C-c
  C-?', where `?' can be any letter, and to not overwrite major mode
  bindings. With org-mode already using most interesting keys,
  collisions are inevitable. This means that some org-journal key
  bindings will not work as expected in an org-mode buffer, and also
  that some org-mode key bindings will not work as expected in an
  org-journal buffer.

  When working in an org-mode buffer the following org-journal key
  bindings are overwritten:
  • `C-c C-s' (`org-journal-search') with `org-schedule'
  • `C-c C-f' (`org-journal-open-next-entry') with
    `org-forward-heading-same-level'
  • `C-c C-b' (`org-journal-open-previous-entry') with
    `org-backward-heading-same-level'
  • `C-c C-j' (`org-journal-new-entry') with `org-goto'

  To workaround this, you can use user bindings of the form `C-c ?',
  where `?' can be any letter, to call the org-journal functions. This
  allows you to have a set of keybindings that work the same in org-mode
  and org-journal buffers. However, this is Emacs, and if you don't like
  a key binding, change it!


1.7.5 Opening journal entries from the calendar are not editable
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  Old entries are opened in `view-mode', which has convenient key
  bindings for browsing files. Most notably, you can quickly close
  `view-mode' buffers with `q', scroll them with the `SPC' and `DEL', or
  quit `view-mode' with `e'.


1.7.6 Can I insert some text on a newly created journal file?
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  Yes, you can write a custom function and assign it
  `org-journal-date-format'.


1.7.7 Can I do more powerful things on a newly created journal entry?
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  Yes, there are two hooks that are run when a journal entry is created.
  Each (`org-journal-new-entry') will call
  `org-journal-after-entry-create-hook', and
  `org-journal-after-header-create-hook' is called each time the date
  (the parent headline of each entry) is generated.


1.8 Convenient `org-journal' Snippet Extensions
───────────────────────────────────────────────

[@dhruvparamhans] <https://github.com/dhruvparamhans>

1.8.1 Kill journal buffer after saving buffer (By [@dhruvparamhans])
╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌

  ┌────
  │ (defun org-journal-save-entry-and-exit()
  │   "Simple convenience function.
  │   Saves the buffer of the current day's entry and kills the window
  │   Similar to org-capture like behavior"
  │   (interactive)
  │   (save-buffer)
  │   (kill-buffer-and-window))
  │ (define-key org-journal-mode-map (kbd "C-x C-s") 'org-journal-save-entry-and-exit)
  └────


[@dhruvparamhans] <https://github.com/dhruvparamhans>


1.9 Contributors
────────────────

  See [CONTRIBUTORS].


[CONTRIBUTORS] <file:CONTRIBUTORS>


1.10 Contributing to `org-journal'
──────────────────────────────────

  We format the code using `common-lisp-indent-function' rather than the
  default `lisp-indent-function'. Please set the variable
  `lisp-indent-function' to `common-lisp-indent-function', and format
  the code before creating a PR.

  ┌────
  │ (setq lisp-indent-function 'common-lisp-indent-function)
  │ ;; Markt the whole buffer: C-x h
  │ ;; Call indent-region: C-M-\
  └────


1.11 Changelog
──────────────

  See [CHANGELOG].


[CHANGELOG] <file:CHANGELOG>
