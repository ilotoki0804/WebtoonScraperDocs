# WebtoonScraper

**Korean documentation is available.**

Download webtoons easily and quickly from various websites.

[<img src="./image/gui.png" width="70%">](https://www.patreon.com/ilotoki0804)

WebtoonScraper lets you download webtoons easily and quickly from various websites. The app is supported on Windows and macOS, and a CLI environment is provided for Linux.

With WebtoonScraper, you can download webtoons from **Naver Webtoon, Lezhin Comics, Kakao Webtoon, Kakaopage, webtoons.com, Ridibooks Webtoon, Toptoon, Bomtoon, Toomics, Bufftoon, Emanbae, TobeContinued, Jaedam Shorts, Naver Game Original, Naver Blog, and Tistory**. You can also use additional features like image concatenation and episode folder merging.

## How to Use

[![WebtoonScraper donation link](./image/patreon.png)](https://www.patreon.com/ilotoki0804)
You can purchase it as a one-time purchase, or use a membership that gives you free access to all releases on a monthly basis.

By supporting on [Patreon](https://www.patreon.com/ilotoki0804), you can support the developer and access various features:

* WebtoonScraper app and CLI
* Support for downloading webtoons from various platforms
* Episode directory merging and image concatenation features
* Computer webtoon viewer through browser (webtoon.html)

You can purchase it as a one-time purchase, or use a membership that gives you free access to all releases for a month (cancelable at any time).

## Learn More

You can learn about WebtoonScraper through various documentation.

For basic [installation](./installing.md) and [downloading](./downloading-app.md) with WebtoonScraper, refer to the respective documents.

Learn about WebtoonScraper's [download range settings](./download-range.md), [getting cookies](./cookie.md), and [episode folder naming](./directory-name.md).

Check out WebtoonScraper's additional features like [image concatenation](./concatenating.md) and [folder merging](./merging.md).

If you're curious about the support status and usage for each platform in WebtoonScraper, refer to the [platforms](./platforms.md) document.

If you're curious about WebtoonScraper's CLI (Command Line Interface) environment, refer to the [downloading with CLI](./downloading-cli.md) document.

Finally, learn about [how to view saved webtoons](./how-to-view.md).

To learn about responsible use of WebtoonScraper, please refer to [this document](./copyright.md).

## PyPI and Github Version

The core logic and some scrapers of WebtoonScraper are publicly available on [PyPI (WebtoonScraper)](https://pypi.org/project/WebtoonScraper/) and [Github](https://github.com/ilotoki0804/WebtoonScraper).

If you're curious about the technical aspects released on PyPI and Github, refer to [this document](./inside-scraper.md).

## Release Notes

Refer to the [release notes document](./releases.md).

## How to Use

WebtoonScraper is divided into three main types:

* App
* CLI version
* PyPI package

**App** can be used by [supporting on Patreon](https://www.patreon.com/ilotoki0804), support webtoon downloads from *Naver Webtoon, Lezhin Comics, Kakao Webtoon, Kakaopage, webtoons.com, Ridibooks Webtoon, Toptoon, Bomtoon, Toomics, Bufftoon, Emanbae, TobeContinued, Jaedam Shorts, Naver Game Original, Naver Blog, and Tistory*, and can be used without special installation. Supports Windows and macOS.

The **CLI** can be used by [supporting on Patreon](https://www.patreon.com/ilotoki0804), just like the app, and can be used with entering commands. Supports Windows, macOS, and Linux.

The **PyPI package** is the most basic version and can be freely downloaded and used, but requires Python installation and *only supports Naver Webtoon*.

## I Found a Bug!

As with all programs, you may encounter bugs while using WebtoonScraper. In that case, you can create a [Github issue](https://github.com/ilotoki0804/WebtoonScraper/issues/) or contact via [Patreon DM](https://www.patreon.com/ilotoki0804). You'll usually receive a reply within a day.

When explaining bugs, providing the following information can help with faster fixes:

* The string output when running `webtoon --version`. If it's not the latest version, please update to the latest version before reporting and check if it's resolved!
* The program you used (PyPI package, CLI, app)
* The URL of the webtoon you attempted to download
* Operating system (Windows/Mac/Linux)
* (For CLI/package) The string output after attempting to download with the `-v` flag added (e.g., `webtoon -v download "<url>"`)