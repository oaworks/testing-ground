# testing-ground

A stable environment to test ShareYourPaper outside our normal infrastructure. Each page is a pretend library website that loads the embed with one set of institution settings (`config`). GitHub Pages serves them at `https://oaworks.github.io/testing-ground/<path>`, with no build step: changes pushed to `master` go live within a minute or two.

This repo also tested InstantILL and embedOA, which have both been retired: `instantill/` and `embedoa/` are kept for reference only, and their Ghost Inspector tests are archived.

## Layout

- `shareyourpaper/dev/`: the dev embed (`dev.shareyourpaper.org/embed.js`) against the beta API. Tests use these.
- `shareyourpaper/live/`: the live embed, mostly copies of real institutions’ set-ups.
- `local-embed/`: a copy of `embed.js`, for trying out unreleased code.

## Pages used by Ghost Inspector

All tests below are in the [ShareYourPaper Website](https://app.ghostinspector.com/suites/698f58e862ccce610d71b1f5) suite, which runs daily.

| Page | Config | Tests |
|---|---|---|
| [`dev/default`](https://oaworks.github.io/testing-ground/shareyourpaper/dev/default) | `owner` | [dark deposit (library default)](https://app.ghostinspector.com/tests/698f58e862ccce610d71b1ff), [go back (general)](https://app.ghostinspector.com/tests/698f58e862ccce610d71b204), [redeposit (library default)](https://app.ghostinspector.com/tests/698f58e862ccce610d71b20d) |
| [`dev/default-with-owner`](https://oaworks.github.io/testing-ground/shareyourpaper/dev/default-with-owner) | `owner` | [url update on entry & restart (embed)](https://app.ghostinspector.com/tests/698f58e862ccce610d71b214) |
| [`dev/community`](https://oaworks.github.io/testing-ground/shareyourpaper/dev/community) | `owner`, `community` | [AAM upload to community](https://app.ghostinspector.com/tests/698f58e862ccce610d71b1fa) |
| [`dev/pilot-mode-on`](https://oaworks.github.io/testing-ground/shareyourpaper/dev/pilot-mode-on) | `owner`, `pilot` | [pilot mode](https://app.ghostinspector.com/tests/698f58e862ccce610d71b20b) |
| [`dev/with-policy`](https://oaworks.github.io/testing-ground/shareyourpaper/dev/with-policy) | `owner`, `ror` | [oa policy response override](https://app.ghostinspector.com/tests/698f58e862ccce610d71b20a) |

## Adding a page

Copy a page in `shareyourpaper/dev/` and change its `config`. Use `example.edu` for any addresses or links. Add the page to the table above once a Ghost Inspector test uses it.

## Running locally

From the repo root, serve the parent folder so URLs keep the `/testing-ground/` prefix:

```
cd .. && python3 -m http.server 8000
```

Then open e.g. `http://localhost:8000/testing-ground/shareyourpaper/dev/default.html`. Include `.html`, which GitHub Pages lets you leave out.

To try unreleased embed code, point a page’s script tag at a `shareyourpaper` checkout in the same parent folder (`/shareyourpaper/content/embed.js`), and change it back before committing. Ghost Inspector runs in the cloud, so it can only test the GitHub Pages copy.
