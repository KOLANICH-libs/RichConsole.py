RichConsole.py [![Unlicensed work](https://raw.githubusercontent.com/unlicense/unlicense.org/master/static/favicon.png)](https://unlicense.org/)
===============
~~[wheel (GHA via `nightly.link`)](https://nightly.link/KOLANICH-libs/RichConsole.py/workflows/CI/master/RichConsole-0.CI-py3-none-any.whl)~~
~~[![GitLab Build Status](https://gitlab.com/KOLANICH/RichConsole.py/badges/master/pipeline.svg)]( https://gitlab.com/KOLANICH/RichConsole.py/pipelines/master/latest)~~
~~![GitLab Coverage](https://gitlab.com/KOLANICH/RichConsole.py/badges/master/coverage.svg)~~
~~[![GitHub Actions](https://github.com/KOLANICH-libs/RichConsole.py/workflows/CI/badge.svg)](https://github.com/KOLANICH-libs/RichConsole.py/actions/)~~
![N∅ hard dependencies](https://shields.io/badge/-N∅_Ъ_deps!-0F0)
[![Libraries.io Status](https://img.shields.io/librariesio/github/KOLANICH-libs/RichConsole.py.svg)](https://libraries.io/github/KOLANICH-libs/RichConsole.py)
[![Code style: antiflash](https://img.shields.io/badge/code%20style-antiflash-FFF.svg)](https://github.com/KOLANICH-tools/antiflash.py)

**We have moved to https://codeberg.org/KOLANICH-libs/RichConsole.py, grab new versions there.**

Under the disguise of "better security" Micro$oft-owned GitHub has [discriminated users of 1FA passwords](https://github.blog/2023-03-09-raising-the-bar-for-software-security-github-2fa-begins-march-13/) while having commercial interest in success and wide adoption of [FIDO 1FA specifications](https://fidoalliance.org/specifications/download/) and [Windows Hello implementation](https://support.microsoft.com/en-us/windows/passkeys-in-windows-301c8944-5ea2-452b-9886-97e4d2ef4422) which [it promotes as a replacement for passwords](https://github.blog/2023-07-12-introducing-passwordless-authentication-on-github-com/). It will result in dire consequencies and is competely inacceptable, [read why](https://codeberg.org/KOLANICH/Fuck-GuanTEEnomo).

If you don't want to participate in harming yourself, it is recommended to follow the lead and migrate somewhere away of GitHub and Micro$oft. Here is [the list of alternatives and rationales to do it](https://github.com/orgs/community/discussions/49869). If they delete the discussion, there are certain well-known places where you can get a copy of it. [Read why you should also leave GitHub](https://codeberg.org/KOLANICH/Fuck-GuanTEEnomo).

---

>Yo dawg so we heard you like text styles so we put styles in your styles so you can style while you styling.

This is a tool to output "poor" (because it is limited by standardized control codes, which are very limited) rich text into a console. When dealing with control codes there is a problem with nesting styles because you have to restore the state, and the state you have to restore depends on the style of the level much distant from the one you are in. This library solves this problem.

You create a [directed acyclic graph](https://en.wikipedia.org/wiki/Directed_acyclic_graph) structure `RichStr` where each piece of string has its own [style`Sheet`](https://en.wikipedia.org/wiki/Style_sheet_(desktop_publishing)). After you have finished forming the output message you convert it into a string. The library does the rest.

How does it work?
-----------------

The algorithm is damn simple: it just traverses the directed acyclic graph in depth-first way, determines exact style of each string, computes differences between them and emits control codes to apply them.

Requirements
------------
* A terminal supporting color codes.
  * Any Linux distro usually has one
  * Windows:
    * Windows 10 [has built-in support](https://docs.microsoft.com/en-us/windows/console/console-virtual-terminal-sequences)
    * [ansicon](https://github.com/adoxa/ansicon) or [ConEmu](https://github.com/Maximus5/ConEmu) or [MinTTY](https://github.com/mintty/mintty) for older Windows
    * you can call [colorama.init()](https://github.com/tartley/colorama) to enable filtering the output with python, but this is VERY glitchy. It raises exceptions even on simple strings. The good thing in it that it supports more codes than `ansicon`.

Optional requirements
---------------------
This library automatically imports colors and other control codes from the following libraries:
* [`colorama`](https://github.com/tartley/colorama/)
  [![PyPi Status](https://img.shields.io/pypi/v/colorama.svg)](https://pypi.org/pypi/colorama)
  [![Build Status](https://github.com/tartley/colorama/actions/workflows/test.yml/badge.svg)](https://github.com/tartley/colorama/actions/workflows/test.yml)
  ![License](https://img.shields.io/github/license/tartley/colorama.svg)

* [`plumbum.colorlib`](https://github.com/tomerfiliba/plumbum/)
  [![PyPi Status](https://img.shields.io/pypi/v/plumbum.svg)](https://pypi.org/pypi/plumbum)
  [![Build Status](https://github.com/tomerfiliba/plumbum/workflows/CI/badge.svg)](https://github.com/tomerfiliba/plumbum/actions)
  [![Docs](https://readthedocs.org/projects/plumbum/badge/)](https://plumbum.readthedocs.io/en/latest/)
  ![License](https://img.shields.io/github/license/tomerfiliba/plumbum.svg)

* [`colored`](https://gitlab.com/dslackw/colored/)
  [![PyPi Status](https://img.shields.io/pypi/v/colored.svg)](https://pypi.org/pypi/colored)

Tutorial
--------
See [`Tutorial.ipynb`](./Tutorial.ipynb)[![NBViewer](https://nbviewer.org/static/ico/ipynb_icon_16x16.png)](https://nbviewer.jupyter.org/github/KOLANICH-libs/RichConsole.py/blob/master/Tutorial.ipynb).
