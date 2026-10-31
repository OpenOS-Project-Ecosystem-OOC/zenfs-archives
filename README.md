# ZenFS Archive Backends

[![AI agent ready](https://img.shields.io/badge/AI_agent-ready-2ea44f?style=flat-square)](https://github.com/Interested-Deving-1896/fork-sync-all/blob/main/DOCS/ai-agent-badges.md)
[![Open in Codex](https://img.shields.io/badge/Open_in-Codex-000000?style=flat-square&logo=openai&logoColor=white)](https://chatgpt.com/codex)
[![Open in Claude Code](https://img.shields.io/badge/Open_in-Claude_Code-d97757?style=flat-square&logo=anthropic&logoColor=white)](https://claude.ai/code)
[![Open in GitHub Copilot](https://img.shields.io/badge/Open_in-GitHub_Copilot-181717?style=flat-square&logo=githubcopilot&logoColor=white)](https://github.com/copilot)
[![Open in Cursor](https://img.shields.io/badge/Open_in-Cursor-111111?style=flat-square)](https://cursor.com/agents)
[![Use with Gemini CLI](https://img.shields.io/badge/Use_with-Gemini_CLI-4285f4?style=flat-square&logo=googlegemini&logoColor=white)](https://github.com/google-gemini/gemini-cli)
[![KDE Eco](https://img.shields.io/badge/KDE%20Eco-certified-brightgreen?logo=kde&logoColor=white&style=flat-square)](https://eco.kde.org/) [![Blue Angel](https://img.shields.io/badge/Blue%20Angel-DE--UZ%20215-0055a4?style=flat-square)](https://www.blauer-engel.de/en/certification/criteria)

[ZenFS](https://github.com/zen-fs/core) backends for archive files.

This packages adds some backends that allow you to create _readonly_ file systems:

- `Zip` for `.zip` files (PK Zip).
- `Iso` for `.iso` files (ISO 9660).
- `Tar` for `.tar` files. The POSIX/USTAR format is the most compatible, but gnu/oldgnu format tar files are also supported.

For more information, see the [API documentation](https://zenfs.dev/archives).

Please read the ZenFS core documentation!

## Installation

```sh
npm install @zenfs/archives
```

## Usage

The easiest way to get started is by looking at these examples

#### `Zip`

```js
import { configure, fs } from '@zenfs/core';
import { Zip } from '@zenfs/archives';

const res = await fetch('http://example.com/archive.zip');

await configure({
	mounts: {
		'/mnt/zip': { backend: Zip, data: await res.arrayBuffer() },
	},
});

const contents = fs.readFileSync('/mnt/zip/in-archive.txt', 'utf-8');
console.log(contents);
```

#### `Iso`

```js
import { configure, fs } from '@zenfs/core';
import { Iso } from '@zenfs/archives';

const res = await fetch('http://example.com/image.iso');

await configure({
	mounts: {
		'/mnt/iso': { backend: Iso, data: await res.bytes() },
	},
});

const contents = fs.readFileSync('/mnt/iso/in-image.txt', 'utf-8');
console.log(contents);
```

The `Iso` implementation uses information from [the OS Dev Wiki](https://wiki.osdev.org/ISO_9660) and [ECMA 119](https://www.ecma-international.org/wp-content/uploads/ECMA-119_4th_edition_june_2019.pdf).

### `Tar`

Same as the `Iso` backend, you pass in the file data as a `Uint8Array`.

## License

[@zenfs/archives](https://github.com/zen-fs/archives) is licensed under the [LGPL 3.0 or later](https://www.gnu.org/licenses/lgpl-3.0.html) and [COPYING.md](https://github.com/zen-fs/archives/blob/main/COPYING.md).
Copyright © James Prevett and other ZenFS contributors.
