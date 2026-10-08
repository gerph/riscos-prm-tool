# riscos-prm

`riscos-prm` finds entries in the online RISC OS Programmer's Reference
Manuals. It can summarise SWIs and services as readable Markdown, print the
URL of a matching entry, or open other manual pages in a browser.

The tool is a portable Perl script for RISC OS, Debian, Ubuntu, and macOS. It
requires Perl and `wget`; opening pages also requires `host-open`, a text-mode
browser, `xdg-open`, or macOS `open`.

## Usage

Look up an interface or chapter by name:

```sh
riscos-prm OS_UpCall
riscos-prm OS_File 1
riscos-prm CnPV
riscos-prm Service_ErrorStarting
riscos-prm AddTinyDir
riscos-prm Squash
```

SWIs and services may also be selected by hexadecimal number:

```sh
riscos-prm "SWI 33"
riscos-prm "Service 400C0"
```

Use `--url` to print a URL, `--open` to open the page, or `--summary` to
request a Markdown summary. A singular category option such as `--swi` or
`--chapter` restricts a lookup; its plural form lists every indexed name in
that category:

```sh
riscos-prm --url Buffer Manager
riscos-prm --swi OS_Claim
riscos-prm --chapters
```

Run `riscos-prm --help` for the complete option list and more examples.

## Behaviour

Unqualified searches cover chapters, vectors, commands, services, and SWIs.
Names are matched without regard to case or spaces, with allowances for such
details as a leading `*` on a command. SWIs and services are summarised by
default; other entries are opened. When standard output is not a terminal,
the URL is printed instead.

The PRM index and fetched pages are cached below
`$XDG_CACHE_HOME/riscos-prm`, or below `~/.cache/riscos-prm` when
`XDG_CACHE_HOME` is not set. Set `BROWSER` to select the command used to open
pages.

The exit status is 0 for a handled match, 1 when nothing matches, 2 when
several entries match, and 3 when a page cannot be opened or summarised.

More detailed reference documentation is available in
[`prminxml/riscos-prm.xml`](prminxml/riscos-prm.xml).
Release archives also contain a rendered version at `manual/riscos-prm.html`.

## Licence

`riscos-prm` is distributed under the MIT Licence. See [LICENSE](LICENSE).
