# Mirko Bronzi’s website

Personal website published at <https://mirkobronzi.github.io/> using GitHub Pages.
The preview workflow below runs locally without publishing changes.

## Preview

From this repository, run:

```sh
sh scripts/preview
```

Open <http://127.0.0.1:4000>. Jekyll rebuilds when content or styles change;
refresh the browser to see the result. Restart the command after changing a
configuration file. Stop it with Ctrl+C.

The helper uses Homebrew Ruby 3.3 when installed at
`/opt/homebrew/opt/ruby@3.3`, with gems scoped to `vendor/bundle`. It binds only
to loopback and applies `_config.local.yml` to disable analytics and comments.
The existing remote theme is fetched from GitHub when Jekyll builds, so an
internet connection is needed. The preview itself stays on this computer.

If dependencies need to be installed again:

```sh
PATH="/opt/homebrew/opt/ruby@3.3/bin:$PATH" BUNDLE_PATH="$PWD/vendor/bundle" bundle install
```

The Gemfile uses GitHub Pages' [documented dependency set](https://pages.github.com/versions/)
and WEBrick for local serving. macOS system Ruby 2.6 is not used for this setup.

## Site files

- `index.html`: introduction and career background, featured publications, and mentorship.
- `_data/publications.yml`: categorized bibliography; `featured: true` selects homepage entries.
- `_pages/publications.html`: full publication page at `/publications/`.
- `_includes/publication.html`: shared compact publication entry.
- `_layouts/research.html` and `assets/css/research.css`: layout and visual design.
- `_pages/year-archive.md`: Writing index, at its existing `/posts/` URL.

Navigation is Home / Publications / Collaboration & mentorship. The publication page groups work into AI
safety, ML, and Data extraction and integration. Earlier writing is accessible
at its existing URLs but is not linked from the homepage. The articles keep their original content, dates, URLs, and
Minimal Mistakes layouts.
No email address or current student availability has been assumed.

The bibliography was checked against linked publication records, DBLP, and
original papers. Mentorship context comes from the linked MATS profile; the page does
not advertise an open application round.

`vendor/`, `.preview/`, generated output, and Bundler state are ignored by Git.
Dependencies, preview scripts, README, and handoff filenames are excluded from
the generated site. Keep any new working notes in an underscore-prefixed file
and verify they are excluded before publishing.

GitHub Pages publishes the repository root from `master`. Pushes to that branch
update the public website.
