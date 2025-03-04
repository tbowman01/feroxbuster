<h1 align="center">
  <br>
  <a href="https://github.com/epi052/feroxbuster"><img src="img/logo/default-cropped.png" alt="feroxbuster"></a>
  <br>
</h1>

<h4 align="center">A simple, fast, recursive content discovery tool written in Rust</h4>

<p align="center">
  <a href="https://github.com/epi052/feroxbuster/actions?query=workflow%3A%22CI+Pipeline%22">
    <img src="https://img.shields.io/github/workflow/status/epi052/feroxbuster/CI%20Pipeline/main?logo=github">
  </a>

  <a href="https://github.com/epi052/feroxbuster/releases">
    <img src="https://img.shields.io/github/downloads/epi052/feroxbuster/total?label=downloads&logo=github&color=inactive" alt="github downloads">
  </a>

  <a href="https://github.com/epi052/feroxbuster/commits/master">
    <img src="https://img.shields.io/github/last-commit/epi052/feroxbuster?logo=github">
  </a>

  <a href="https://crates.io/crates/feroxbuster">
    <img src="https://img.shields.io/crates/v/feroxbuster?color=blue&label=version&logo=rust">
  </a>

  <a href="https://crates.io/crates/feroxbuster">
    <img src="https://img.shields.io/crates/d/feroxbuster?label=downloads&logo=rust&color=inactive">
  </a>

  <a href="https://codecov.io/gh/epi052/feroxbuster">
    <img src="https://codecov.io/gh/epi052/feroxbuster/branch/master/graph/badge.svg" />
  </a>
  <!--
  <!-- ALL-CONTRIBUTORS-BADGE:START - Do not remove or modify this section 
    [![All Contributors](https://img.shields.io/badge/all_contributors-15-orange.svg?style=flat-square)](#contributors-)
  <!-- ALL-CONTRIBUTORS-BADGE:END -->
  <a href="https://github.com/epi052/feroxbuster/graphs/contributors">
    <img src="https://img.shields.io/badge/all_contributors-31-orange.svg" />
  </a>

</p>

![demo](img/demo.gif)

<p align="center">
  🦀
  <a href="https://github.com/epi052/feroxbuster/releases">Releases</a> ✨
  <a href="https://epi052.github.io/feroxbuster-docs/docs/examples/">Example Usage</a> ✨
  <a href="https://github.com/epi052/feroxbuster/blob/main/CONTRIBUTING.md">Contributing</a> ✨
  <a href="https://epi052.github.io/feroxbuster-docs/docs/">Documentation</a>
  🦀
</p>

---

<h1><p align="center">✨🎉👉 <a href="https://epi052.github.io/feroxbuster-docs/docs/">NEW DOCUMENTATION SITE</a> 👈🎉✨</p></h1>


## 🚀 Documentation has **moved** 🚀  

Instead of having a 1300 line `README.md` (sorry...), feroxbuster's documentation has moved to GitHub Pages. The move to hosting documentation on Pages should make it a LOT easier to find the information you're looking for, whatever that may be. Please check it out for anything you need beyond a quick-start. The new documentation can be found [here](https://epi052.github.io/feroxbuster-docs/docs/). 

## 😕 What the heck is a ferox anyway?

Ferox is short for Ferric Oxide. Ferric Oxide, simply put, is rust. The name rustbuster was taken, so I decided on a
variation. 🤷

## 🤔 What's it do tho?

`feroxbuster` is a tool designed to perform [Forced Browsing](https://owasp.org/www-community/attacks/Forced_browsing).

Forced browsing is an attack where the aim is to enumerate and access resources that are not referenced by the web
application, but are still accessible by an attacker.

`feroxbuster` uses brute force combined with a wordlist to search for unlinked content in target directories. These
resources may store sensitive information about web applications and operational systems, such as source code,
credentials, internal network addressing, etc...

This attack is also known as Predictable Resource Location, File Enumeration, Directory Enumeration, and Resource
Enumeration.

## ⏳ Quick Start

This section will cover the minimum amount of information to get up and running with feroxbuster. Please refer the the [documentation](https://epi052.github.io/feroxbuster-docs/docs/), as it's much more comprehensive.

### 💿 Installation

There are quite a few other [installation methods](https://epi052.github.io/feroxbuster-docs/docs/installation/), but these snippets should cover the majority of users. 

#### Kali 

If you're using kali, this is the preferred install method. Installing from the repos adds a [**ferox-config.toml**](https://epi052.github.io/feroxbuster-docs/docs/configuration/ferox-config-toml/) in `/etc/feroxbuster/`, adds command completion for bash, fish, and zsh, includes a man page entry, and installs `feroxbuster` itself. 

```
sudo apt update && sudo apt install -y feroxbuster
```

#### Linux (32 and 64-bit) & MacOS

```
curl -sL https://raw.githubusercontent.com/epi052/feroxbuster/master/install-nix.sh | bash
```


#### Windows x86_64

```
Invoke-WebRequest https://github.com/epi052/feroxbuster/releases/latest/download/x86_64-windows-feroxbuster.exe.zip -OutFile feroxbuster.zip
Expand-Archive .\feroxbuster.zip
.\feroxbuster\feroxbuster.exe -V
```

#### All others 

Please refer the the [documentation](https://epi052.github.io/feroxbuster-docs/docs/).

## 🧰 Example Usage

Here are a few brief examples to get you started.  Please note, feroxbuster can do a **lot more** than what's listed below.  As a result, there are **many more** examples, with **demonstration gifs** that highlight specific features, in the [documentation](https://epi052.github.io/feroxbuster-docs/docs/).

### Multiple Values

Options that take multiple values are very flexible. Consider the following ways of specifying extensions:

```
./feroxbuster -u http://127.1 -x pdf -x js,html -x php txt json,docx
```

The command above adds .pdf, .js, .html, .php, .txt, .json, and .docx to each url

All of the methods above (multiple flags, space separated, comma separated, etc...) are valid and interchangeable. The
same goes for urls, headers, status codes, queries, and size filters.

### Include Headers

```
./feroxbuster -u http://127.1 -H Accept:application/json "Authorization: Bearer {token}"
```

### IPv6, non-recursive scan with INFO-level logging enabled

```
./feroxbuster -u http://[::1] --no-recursion -vv
```

### Read urls from STDIN; pipe only resulting urls out to another tool

```
cat targets | ./feroxbuster --stdin --silent -s 200 301 302 --redirects -x js | fff -s 200 -o js-files
```

### Proxy traffic through Burp

```
./feroxbuster -u http://127.1 --insecure --proxy http://127.0.0.1:8080
```

### Proxy traffic through a SOCKS proxy (including DNS lookups)

```
./feroxbuster -u http://127.1 --proxy socks5h://127.0.0.1:9050
```

### Pass auth token via query parameter

```
./feroxbuster -u http://127.1 --query token=0123456789ABCDEF
```

## 🚀 Documentation has **moved** 🚀  

For realsies, there used to be over 1300 lines in this README, but it's all been moved to the [new documentation site](https://epi052.github.io/feroxbuster-docs/docs/). Go check it out! 

<h1><p align="center">✨🎉👉 <a href="https://epi052.github.io/feroxbuster-docs/docs/">DOCUMENTATION</a> 👈🎉✨</p></h1>

## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="https://io.fi"><img src="https://avatars.githubusercontent.com/u/5235109?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Joona Hoikkala</b></sub></a><br /><a href="https://github.com/epi052/feroxbuster/commits?author=joohoi" title="Documentation">📖</a></td>
    <td align="center"><a href="https://github.com/jsav0"><img src="https://avatars.githubusercontent.com/u/20546041?v=4?s=100" width="100px;" alt=""/><br /><sub><b>J Savage</b></sub></a><br /><a href="#infra-jsav0" title="Infrastructure (Hosting, Build-Tools, etc)">🚇</a> <a href="https://github.com/epi052/feroxbuster/commits?author=jsav0" title="Documentation">📖</a></td>
    <td align="center"><a href="http://www.tgotwig.dev"><img src="https://avatars.githubusercontent.com/u/30773779?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Thomas Gotwig</b></sub></a><br /><a href="#infra-TGotwig" title="Infrastructure (Hosting, Build-Tools, etc)">🚇</a> <a href="https://github.com/epi052/feroxbuster/commits?author=TGotwig" title="Documentation">📖</a></td>
    <td align="center"><a href="https://github.com/spikecodes"><img src="https://avatars.githubusercontent.com/u/19519553?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Spike</b></sub></a><br /><a href="#infra-spikecodes" title="Infrastructure (Hosting, Build-Tools, etc)">🚇</a> <a href="https://github.com/epi052/feroxbuster/commits?author=spikecodes" title="Documentation">📖</a></td>
    <td align="center"><a href="https://github.com/evanrichter"><img src="https://avatars.githubusercontent.com/u/330292?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Evan Richter</b></sub></a><br /><a href="https://github.com/epi052/feroxbuster/commits?author=evanrichter" title="Code">💻</a> <a href="https://github.com/epi052/feroxbuster/commits?author=evanrichter" title="Documentation">📖</a></td>
    <td align="center"><a href="https://github.com/mzpqnxow"><img src="https://avatars.githubusercontent.com/u/8016228?v=4?s=100" width="100px;" alt=""/><br /><sub><b>AG</b></sub></a><br /><a href="#ideas-mzpqnxow" title="Ideas, Planning, & Feedback">🤔</a> <a href="https://github.com/epi052/feroxbuster/commits?author=mzpqnxow" title="Documentation">📖</a></td>
    <td align="center"><a href="https://n-thumann.de/"><img src="https://avatars.githubusercontent.com/u/46975855?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Nicolas Thumann</b></sub></a><br /><a href="https://github.com/epi052/feroxbuster/commits?author=n-thumann" title="Code">💻</a> <a href="https://github.com/epi052/feroxbuster/commits?author=n-thumann" title="Documentation">📖</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/tomtastic"><img src="https://avatars.githubusercontent.com/u/302127?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Tom Matthews</b></sub></a><br /><a href="https://github.com/epi052/feroxbuster/commits?author=tomtastic" title="Documentation">📖</a></td>
    <td align="center"><a href="https://github.com/bsysop"><img src="https://avatars.githubusercontent.com/u/9998303?v=4?s=100" width="100px;" alt=""/><br /><sub><b>bsysop</b></sub></a><br /><a href="https://github.com/epi052/feroxbuster/commits?author=bsysop" title="Documentation">📖</a></td>
    <td align="center"><a href="http://bpsizemore.me"><img src="https://avatars.githubusercontent.com/u/11645898?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Brian Sizemore</b></sub></a><br /><a href="https://github.com/epi052/feroxbuster/commits?author=bpsizemore" title="Code">💻</a></td>
    <td align="center"><a href="https://pwn.by/noraj"><img src="https://avatars.githubusercontent.com/u/16578570?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Alexandre ZANNI</b></sub></a><br /><a href="#infra-noraj" title="Infrastructure (Hosting, Build-Tools, etc)">🚇</a> <a href="https://github.com/epi052/feroxbuster/commits?author=noraj" title="Documentation">📖</a></td>
    <td align="center"><a href="https://github.com/craig"><img src="https://avatars.githubusercontent.com/u/99729?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Craig</b></sub></a><br /><a href="#infra-craig" title="Infrastructure (Hosting, Build-Tools, etc)">🚇</a></td>
    <td align="center"><a href="https://www.reddit.com/u/EONRaider"><img src="https://avatars.githubusercontent.com/u/15611424?v=4?s=100" width="100px;" alt=""/><br /><sub><b>EONRaider</b></sub></a><br /><a href="#infra-EONRaider" title="Infrastructure (Hosting, Build-Tools, etc)">🚇</a></td>
    <td align="center"><a href="https://github.com/wtwver"><img src="https://avatars.githubusercontent.com/u/53866088?v=4?s=100" width="100px;" alt=""/><br /><sub><b>wtwver</b></sub></a><br /><a href="#infra-wtwver" title="Infrastructure (Hosting, Build-Tools, etc)">🚇</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://tib3rius.com"><img src="https://avatars.githubusercontent.com/u/48113936?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Tib3rius</b></sub></a><br /><a href="https://github.com/epi052/feroxbuster/issues?q=author%3ATib3rius" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://github.com/0xdf"><img src="https://avatars.githubusercontent.com/u/1489045?v=4?s=100" width="100px;" alt=""/><br /><sub><b>0xdf</b></sub></a><br /><a href="https://github.com/epi052/feroxbuster/issues?q=author%3A0xdf" title="Bug reports">🐛</a></td>
    <td align="center"><a href="http://secure77.de"><img src="https://avatars.githubusercontent.com/u/31564517?v=4?s=100" width="100px;" alt=""/><br /><sub><b>secure-77</b></sub></a><br /><a href="https://github.com/epi052/feroxbuster/issues?q=author%3Asecure-77" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://github.com/sbrun"><img src="https://avatars.githubusercontent.com/u/7712154?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Sophie Brun</b></sub></a><br /><a href="#infra-sbrun" title="Infrastructure (Hosting, Build-Tools, etc)">🚇</a></td>
    <td align="center"><a href="https://github.com/black-A"><img src="https://avatars.githubusercontent.com/u/30686803?v=4?s=100" width="100px;" alt=""/><br /><sub><b>black-A</b></sub></a><br /><a href="#ideas-black-A" title="Ideas, Planning, & Feedback">🤔</a></td>
    <td align="center"><a href="https://github.com/dinosn"><img src="https://avatars.githubusercontent.com/u/3851678?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Nicolas Krassas</b></sub></a><br /><a href="#ideas-dinosn" title="Ideas, Planning, & Feedback">🤔</a></td>
    <td align="center"><a href="https://github.com/N0ur5"><img src="https://avatars.githubusercontent.com/u/24260009?v=4?s=100" width="100px;" alt=""/><br /><sub><b>N0ur5</b></sub></a><br /><a href="#ideas-N0ur5" title="Ideas, Planning, & Feedback">🤔</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/moscowchill"><img src="https://avatars.githubusercontent.com/u/72578879?v=4?s=100" width="100px;" alt=""/><br /><sub><b>mchill</b></sub></a><br /><a href="https://github.com/epi052/feroxbuster/issues?q=author%3Amoscowchill" title="Bug reports">🐛</a></td>
    <td align="center"><a href="http://BitThr3at.github.io"><img src="https://avatars.githubusercontent.com/u/45028933?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Naman</b></sub></a><br /><a href="https://github.com/epi052/feroxbuster/issues?q=author%3ABitThr3at" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://github.com/Sicks3c"><img src="https://avatars.githubusercontent.com/u/32225186?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Ayoub Elaich</b></sub></a><br /><a href="https://github.com/epi052/feroxbuster/issues?q=author%3Asicks3c" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://github.com/HenryHoggard"><img src="https://avatars.githubusercontent.com/u/1208121?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Henry</b></sub></a><br /><a href="https://github.com/epi052/feroxbuster/issues?q=author%3AHenryHoggard" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://github.com/SleepiPanda"><img src="https://avatars.githubusercontent.com/u/6428561?v=4?s=100" width="100px;" alt=""/><br /><sub><b>SleepiPanda</b></sub></a><br /><a href="https://github.com/epi052/feroxbuster/issues?q=author%3ASleepiPanda" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://github.com/uBadRequest"><img src="https://avatars.githubusercontent.com/u/47282747?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Bad Requests</b></sub></a><br /><a href="https://github.com/epi052/feroxbuster/issues?q=author%3AuBadRequest" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://home.dnaka91.rocks"><img src="https://avatars.githubusercontent.com/u/36804488?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Dominik Nakamura</b></sub></a><br /><a href="#infra-dnaka91" title="Infrastructure (Hosting, Build-Tools, etc)">🚇</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/hunter0x8"><img src="https://avatars.githubusercontent.com/u/46222314?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Muhammad Ahsan</b></sub></a><br /><a href="https://github.com/epi052/feroxbuster/issues?q=author%3Ahunter0x8" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://github.com/cortantief"><img src="https://avatars.githubusercontent.com/u/34527333?v=4?s=100" width="100px;" alt=""/><br /><sub><b>cortantief</b></sub></a><br /><a href="https://github.com/epi052/feroxbuster/issues?q=author%3Acortantief" title="Bug reports">🐛</a> <a href="https://github.com/epi052/feroxbuster/commits?author=cortantief" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/dsaxton"><img src="https://avatars.githubusercontent.com/u/2658661?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Daniel Saxton</b></sub></a><br /><a href="#ideas-dsaxton" title="Ideas, Planning, & Feedback">🤔</a> <a href="https://github.com/epi052/feroxbuster/commits?author=dsaxton" title="Code">💻</a></td>
  </tr>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!