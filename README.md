# Date → Locale Converter

## Contents

- [Overview](#overview)
- [Demo](#demo)
- [Scripts](#scripts)
- [Query String Parameters](#query-string-parameters)
- [License](#license)

## Overview

A simple web app to convert an input date to a locale string.

Built with [Vite](https://vitejs.dev), [Vue Composition API](https://vuejs.org) and [Tailwind CSS](https://tailwindcss.com/).

## Demo

https://furey.com.au/stuff/utils/date/?i=now

## Scripts

Install dependencies:

```console
$ npm ci
```

Develop locally:

```console
$ vite dev
```

Build for production:

```console
$ vite build
```

## Query String Parameters

Optional browser query string parameters:

| Parameter | Description       | Example                                         |
| :-------- | :---------------- | :---------------------------------------------- |
| `i`       | Input Date        | `2022-10-26%2007:30:00.327Z`, `1667020560`, etc |
| `l`       | Output Locale     | `en-GB`, etc                                    |
| `ds`      | Output Date Style | `full`, `long`, `medium`, `short`               |
| `ts`      | Output Time Style | `full`, `long`, `medium`, `short`               |
| `tz`      | Output Time Zone  | `Australia/Sydney`, etc                         |
| `o`       | Show Options      | `true`, `yes`, `1`                              |

Example:

https://furey.com.au/stuff/utils/date/?i=2022-10-26%2007:30:00.327Z&l=en-US&ds=full&ts=full&tz=America/New_York&o=true

## License

ISC License

Copyright (c) 2022, James Furey

Permission to use, copy, modify, and/or distribute this software for any purpose with or without fee is hereby granted, provided that the above copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
