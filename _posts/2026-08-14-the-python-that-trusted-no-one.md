---
layout: default
title: "The Python that trusted no one"
date: 2026-08-14
author: Gonzalo Barrera Borla
---

# The Python that trusted no one

*A small morsel from the random-facts department: how installing the Google
Cloud SDK silently broke my torrent client's search, two apps that have
absolutely nothing to do with each other.*

Two days ago, qBittorrent's search tab stopped returning results. No errors,
no crashes: every search finished with a cheerful green tick and zero rows.
The obvious suspects — outdated search plugins, sites moving domains, a
Python upgrade — all checked out fine when tested from the terminal. The
same search engine script that returned *nothing* inside the app returned
hundreds of results on the command line.

The trick was watching `ps` while the app searched. qBittorrent wasn't using
the Homebrew Python my terminal uses; it was spawning

```
/Library/Frameworks/Python.framework/Versions/3.14/.../Python -I nova2.py ...
```

a **python.org framework build** I never knowingly installed. Running the
search with *that* interpreter reproduced the bug instantly, and loudly:

```
Connection error: [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify
failed: unable to get local issuer certificate
```

Here's the fact worth keeping: **since Python 3.6, the official python.org
macOS installers bundle their own OpenSSL and do not trust the system
keychain — or anything at all — until you run a one-time script** that ships
with them, `/Applications/Python 3.XX/Install Certificates.command`. It just
pip-installs `certifi` and symlinks its CA bundle into place. Skip it, and
every single HTTPS request from that interpreter fails. If you install
Python by hand you *might* notice the installer's final screen telling you
this. See [bpo-28150](https://bugs.python.org/issue28150) for the classic
bug report, and [this TIL](https://matduggan.com/til-python-3-6-and-up-is-broken-on-mac/)
for a short writeup.

But I didn't install it by hand. The package receipt (`pkgutil --pkg-info
org.python.Python.PythonFramework-3.14`) showed it landed **exactly two days
ago, the same minute the gcloud SDK built its virtualenv** — gcloud had
downloaded the python.org installer and run it non-interactively. No final
screen, no ReadMe, no hint. And qBittorrent, when hunting for a `python3` to
run its search plugins, prefers framework Pythons over Homebrew's.

So the causal chain reads: *update gcloud → it installs a certificate-less
Python → torrent search dies silently*. Nobody would ever guess that from
the symptom. The fix is one line:

```
"/Applications/Python 3.14/Install Certificates.command"
```

Morals, in decreasing order of generality: silent failures deserve loud
reproductions (`ps` doesn't lie about what actually ran); "which Python?" is
always a fair question on a Mac with four of them; and if some tool installs
python.org Python on your behalf, go run that certificates script before
anything HTTPS-shaped mysteriously starves.
