# ivy-emms

A simple ivy interface to [`emms`](https://www.gnu.org/software/emms/).

![Screenshot](images/ivy-emms.png)

# Dependencies

This package requires `emms` and `ivy`.

If you want to act on marked candidates, you need a
recent version of `ivy` (MELPA version 20200613.1920 or better).

# Installation

To install, just put `ivy-emms.el` somewhere in your
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

Then do `M-x ivy-emms` to see a formatted list of tracks to
choose from.

Hit `RET` to play the chosen track.  If you have marked
several tracks, the first will be played and the rest put in
the playlist.

*Warning*: Either action will wipe the current EMMS
playlist.  See below for alternatives.

## Other actions

Hit `M-o` (`ivy-dispatching-done`) to choose and apply alternate
actions.  Currently these are:

|Key|Action|
|---|------|
|`a`| Add track(s) to the end of the current playlist|
|`i`| Insert track(s) into the current playlist right after the current track|


# Acknowledgements

This package owes a clear intellectual debt to [`helm-emms`](https://github.com/emacs-helm/helm-emms)
and also to [`ivy-bitex`](https://github.com/tmalsburg/helm-bibtex) from which I learned how to
work with `ivy`.
