# ivy-emms
[![MELPA](https://melpa.org/packages/ivy-emms-badge.svg)](https://melpa.org/#/ivy-emms)

A simple ivy interface to [`emms`](https://www.gnu.org/software/emms/).

![Screenshot](images/ivy-emms.png)

# News

* v0.3: Sort track list.

# Dependencies

This package requires `emms` and `ivy`.

If you want to act on marked candidates, you need a
recent version of `ivy` (MELPA version 20200613.1920 or better).

# Installation

## From MELPA

``` elisp
(package-install 'ivy-emms)
```
or

``` elisp
(use-package ivy-emms
  :ensure t)
```

## Manual
Download `ivy-emms.el`, put it somewhere in your
load-path and then do either:
```elisp
(require 'ivy-emms)
```
or
```elisp
(autoload 'ivy-emms "ivy-emms" nil t)
```

# Usage

First make sure that `emms` is working to your satisfaction
and knows about your music collection.

Do `M-x ivy-emms` to see a formatted list of tracks to
choose from.

Hit `RET` to play the chosen track.

Mark tracks with `C-SPC` and unmark them with `S-SPC`.

Mark several tracks and hit `RET` to play the first track
and queue the rest in the current playlist.

*Warning*: Either action will wipe the current EMMS
playlist.  See below for alternatives.

## Other actions

Hit `M-o` (`ivy-dispatching-done`) to choose and apply alternate
actions.  Currently these are:

|Key|Action|
|---|------|
|`a`| Append track(s) to the current playlist|
|`i`| Play next: insert track(s) into the current playlist after the current track|

## Rebuilding the track-list

Call `ivy-emms` with a prefix argument `C-u M-x ivy-emms` to
rebuild the track list.  Useful if you add new music to EMMS
after loading `ivy-emms`.

# Customisation

## Default actions

You can change the default action for single tracks (what `ivy-emms` does when
you hit `RET`) with:

``` elisp
(setq ivy-emms-default-action #'ivy-emms-add-track)
```
You can also change the default multi-action (for when you
have marked some tracks and then hit `RET`) with something like:

``` elisp
(setq ivy-emms-default-multi-action #'ivy-emms-play-next-multi)
```

Here are all the possibilities:

| What                          | Action               | Multi-action               |
|-------------------------------|----------------------|----------------------------|
| Play/play and queue (default) | `ivy-emms-play`      | `ivy-emms-queue-and-play`  |
| Append to playlist            | `ivy-emms-add-track` | N/A                        |
| Play next                     | `ivy-emms-play-next` | `ivy-emms-play-next-multi` |

There is no multi-action needed for `ivy-emms-add-track`
because the default behaviour of `ivy` is to call the single
track action on each marked candidate in turn which is The
Right Thing.

## Advanced: roll your own track-list

You can change the appearance of the track-list by writing
your own function to generate it:

``` elisp
(setq ivy-emms-make-item-function #'my-amazing-make-item)
```
Your function should take a string as argument (a key in the
`emms-cache-db` hash-table) and return a cons cell with your
formatted search term as car and the string as cdr.

Have a look at `ivy-emms-simple-make-item` for ideas to get started.

# Acknowledgements

This package owes a clear intellectual debt to [`helm-emms`](https://github.com/emacs-helm/helm-emms)
and also to [`ivy-bibtex`](https://github.com/tmalsburg/helm-bibtex) from which I learned how to
work with `ivy`.  I got the idea for easy track (un-)marking from [`org-ref`](https://github.com/jkitchin/org-ref).
