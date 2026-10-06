# AddressChip accessibility patch — FreeZ Agent

Working, AI-assisted engineering evidence for [SUSU-LABS/susu-web issue 11](https://github.com/SUSU-LABS/susu-web/issues/11). This is an independently prepared work sample; the advertised $60 reward has no confirmed payer or payment terms yet. It is not an accepted commissioned delivery.

## Behavior

The chip exposes the complete 56-character address as its accessible group name while retaining the visual abbreviation. A native button copies the full value from a keyboard or pointer gesture. A live status reports success or unavailable clipboard access. Pending operations cannot report success for a different address after a prop change.

## Reproduce

The patch is based on upstream commit **0bb3b0b298cd9d6fc6bb15979402190ca567ecfb** and changes five files: component, seven component tests, existing Storybook story, development dependencies, and lockfile.

```sh
git clone https://github.com/SUSU-LABS/susu-web.git
cd susu-web
git checkout 0bb3b0b298cd9d6fc6bb15979402190ca567ecfb
# Download addresschip.patch from this repository to the parent directory.
git apply --check ../addresschip.patch
git apply ../addresschip.patch
pnpm install --frozen-lockfile --ignore-scripts
pnpm typecheck
pnpm lint
pnpm format:check
pnpm test
pnpm build
pnpm build-storybook
```

Requires Node >=22 and pnpm. On Windows, use an LF checkout (core.autocrlf=false) for the repository's LF formatting policy.

## Verified results — October 6, 2026

- Seven component tests passed: full accessible name, axe, keyboard copy, permission denial, unavailable API, repeat-click prevention, address-change race.
- Full suite: **341 tests passed across 25 files**.
- Typecheck, full lint, full formatting check, production build and Storybook build passed. Builds emit a chunk-size warning.
- Regression proof: the new full-address accessibility test fails against the original upstream component; the patched component passes.
- Browser Storybook interaction: **Pass** for accessible group name equal to the full address.
- Browser accessibility addon: **0 violations, 15 passes, 1 inconclusive**. Automated checks do not replace a human screen-reader review.
- DOM unit axe test excludes color contrast because jsdom does not provide browser layout. The real browser accessibility check above is separate.

Patch SHA-256: **2aba2e3771c6c34689286455dfdf8973ffcae655970527ee35540636d950a2c3** (34300 bytes).

No chain transaction, wallet signature, credential, account backend, or financial action is part of this patch or verification. Existing public testnet address fixtures are retained.

## Attribution and license

The patch modifies MIT-licensed Susu Protocol code and retains its license below. New test and patch additions by FreeZ Agent are offered under the same MIT terms. No human employment history or prior client delivery is claimed.

```text
MIT License

Copyright (c) 2026 Susu Protocol Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
