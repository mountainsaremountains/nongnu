[file:http://melpa.org/packages/tangotango-theme-badge.svg]

This is an emacs color theme based on the tango palette colors.


[file:http://melpa.org/packages/tangotango-theme-badge.svg]
<http://melpa.org/#/tangotango-theme>


1 Screenshots
═════════════

  Here is a screenshot of the color theme with an emacs-lisp file :

  <https://github.com/juba/color-theme-tangotango/raw/master/screenshots/tangotango_elisp.png>

  One with a Gnus summary and article buffers :

  <https://github.com/juba/color-theme-tangotango/raw/master/screenshots/tangotango_gnus.png>

  And one with an org-mode buffer :

  <https://github.com/juba/color-theme-tangotango/raw/master/screenshots/tangotango_org.png>


2 Installation instructions
═══════════════════════════

2.1 Package.el
──────────────

  `tangotango-theme' is available in [MELPA]. You can add this
  repository by following its [installation instructions].

  To install `tangotango-theme', just do :

  ┌────
  │ M-x package-install tangotango-theme
  └────


  You can then try it with `M-x load-theme'. If you want to load it
  automatically on startup, add the following to your init file :

  ┌────
  │ (load-theme 'tangotango t)  
  └────


[MELPA] <http://melpa.milkbox.net>

[installation instructions] <http://melpa.milkbox.net/#installing>


2.2 Manual (Emacs 24)
─────────────────────

  Emacs 24 features native color theming, and as such you don't need any
  third party package or extension.

  1. Download `tangotango-theme.el' from [github] and save it to your
     `~/.emacs.d' directory
  2. Try it with `M-x load-theme'
  3. If you like it, just add the following line to your `.emacs' :

  ┌────
  │ (load-theme 'tangotango t)
  └────


  If you prefer to place your theme files in another directory, you can
  just add something like the following in your `.emacs' before loading
  the theme :

  ┌────
  │ (add-to-list 'custom-theme-load-path "~/.emacs.d/color-theme-tangotango")
  └────


[github]
<https://github.com/juba/color-theme-tangotango/raw/master/tangotango-theme.el>


2.3 Emacs 23
────────────

  With Emacs 23 you need to use the `color-theme' package :

  1. Download and install the `color-theme' emacs package either via
     your linux distribution or [via the source tarball]
  2. Download and install `color-theme-tangotango.el' from [github]
  3. Make sure that both `color-theme.el' and
     `color-theme-tangotango.el' are in your load path

  There are several ways to load the tangotango color theme from your
  `.emacs', as documented on [emacswiki]. The way I currently use should
  work for a daemonized emacs and allows the selection of different
  themes for GUI or console based frames :

  ┌────
  │ (require 'color-theme)
  │ (setq color-theme-load-all-themes nil)
  │ 
  │ (require 'color-theme-tangotango)
  │ 
  │ ;; select theme - first list element is for windowing system, second is for console/terminal
  │ ;; Source : http://www.emacswiki.org/emacs/ColorTheme#toc9
  │ (setq color-theme-choices 
  │       '(color-theme-tangotango color-theme-tangotango))
  │ 
  │ ;; default-start
  │ (funcall (lambda (cols)
  │     	   (let ((color-theme-is-global nil))
  │     	     (eval 
  │     	      (append '(if (window-system))
  │     		      (mapcar (lambda (x) (cons x nil)) 
  │     			      cols)))))
  │     	 color-theme-choices)
  │ 
  │ ;; test for each additional frame or console
  │ (require 'cl)
  │ (fset 'test-win-sys 
  │       (funcall (lambda (cols)
  │     		 (lexical-let ((cols cols))
  │     		   (lambda (frame)
  │     		     (let ((color-theme-is-global nil))
  │ 		       ;; must be current for local ctheme
  │ 		       (select-frame frame)
  │ 		       ;; test winsystem
  │ 		       (eval 
  │ 			(append '(if (window-system frame)) 
  │ 				(mapcar (lambda (x) (cons x nil)) 
  │ 					cols)))))))
  │     	       color-theme-choices ))
  │ ;; hook on after-make-frame-functions
  │ (add-hook 'after-make-frame-functions 'test-win-sys)
  │ 
  │ (color-theme-tangotango)
  └────


  Note that I also had to add a (color-theme-tangotango) line at the end
  of my `.gnus' file in order to apply the color theme to Gnus.


[via the source tarball] <http://www.nongnu.org/color-theme/#sec5>

[github]
<http://github.com/juba/color-theme-tangotango/raw/master/color-theme-tangotango.el>

[emacswiki] <http://www.emacswiki.org/emacs/ColorTheme>
