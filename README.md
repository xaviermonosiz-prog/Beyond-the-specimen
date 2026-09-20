# Beyond the Specimen

A counter-archive of patient and family narratives connected to psychiatric and neurological illness in Karnataka, built as a companion to the NIMHANS Brain Museum, Bengaluru.

Monosiz Xavier Mallick · 7BAENG · 2333151
*Memory Machines: The Politics of Digital Preservation* (ENG405A-7B)
Supervised by Prof. Renu Elizabeth Abraham

---

## What's in the repo

```
index.html      the entire website — markup, styles, data, behaviour
.nojekyll       tells GitHub Pages to serve the files as-is
images/         put photographs here
README.md       this file
```

There is no build step, no npm install, and no dependencies to install. The only
external requests the page makes are to Google Fonts.

## Running it locally

Double-click `index.html`. That's it.

If you'd rather serve it properly (useful once you add images):

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Putting it on GitHub Pages

1. Create a new repository on GitHub — public, no template.
2. Upload `index.html`, `.nojekyll`, `README.md`, and the `images/` folder to the
   root of the repository. (Web UI: **Add file → Upload files**. Or use git:)

   ```bash
   git init
   git add .
   git commit -m "feat: counter-archive site"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
   git push -u origin main
   ```

3. In the repository, go to **Settings → Pages**.
4. Under *Build and deployment*, set **Source** to `Deploy from a branch`,
   **Branch** to `main`, folder `/ (root)`. Save.
5. Wait a minute or two. The site appears at
   `https://YOUR-USERNAME.github.io/YOUR-REPO/`

`index.html` must sit at the root of the repository, not inside a subfolder, or
Pages won't find it.

## Editing the archive

Everything you'll want to change lives in one place: open `index.html`, scroll to
the `<script>` tag near the bottom, and look for the commented blocks.

### Adding a record

Copy an existing object in the `RECORDS` array and change its fields:

```js
{
  id:"g-08",                          // any unique string
  who:"public",                       // "caregiver" | "professional" | "public"
  tier:"public",                      // "public" shows in full, "restricted" hides the text
  name:"Nurse, district hospital",    // how the contributor asked to be identified
  meta:"7+ years in the field",       // short non-identifying context line
  tags:["cost","stigma"],             // new tags appear in the filter row automatically
  fields:[
    {q:"Question as shown on the page", a:"The answer, as written."}
  ]
}
```

A record with `tier:"restricted"` shows only its name, meta and tags, plus a
`withheldNote` explaining why the account isn't displayed. Its `fields` array
should stay empty — nothing you leave in it will render, but nothing sensitive
should sit in the file at all.

Filters, counts, sorting and the theme list all rebuild themselves from the data.
You never have to touch the interface code to add a contribution.

### Adding pictures

Put image files in `images/`, then set a `src` in one of four places:

| Where it appears | What to edit |
| --- | --- |
| Inside the specimen tag in the hero | `TAG_PHOTO` |
| The Plates section | the `PLATES` array |
| Inside an opened record | that record's `images` array |
| On a card in the grid | that record's `thumb` |

```js
{src:"images/entrance.jpg", alt:"Entrance to the museum", caption:"NIMHANS, Hombegowda Nagar", height:220}
```

Always write `alt` text — it's the record of the image for anyone who can't see it.

Any slot left as `src:""` stays on the page as a dashed empty frame with its
caption intact, so a missing photograph reads as a gap rather than disappearing.

### Changing the words

Section headings and body copy are plain HTML in the `<main>` element. Colours,
type and spacing are CSS custom properties in the `:root` block at the top of the
file — change `--plum`, `--amber`, `--bg` and the rest in one place and the whole
page follows.

## Consent and what is not in this repository

- One caregiver account is withheld pending confirmation of its tier consent. Its
  text is not stored anywhere in this repository.
- Two professionals asked to be fully anonymous and are shown without role,
  setting, or years of experience.
- Contributions that object to the project are kept alongside those that support
  it, tagged `dissent`.

Before committing any new narrative, check that the contributor's consent covers
the tier you're placing it in. A public GitHub repository is the public tier,
including its commit history — material removed in a later commit is still
readable in earlier ones.

## Still missing

- Contributions in Kannada, Tamil, Telugu and Hindi
- Audio and video oral histories
- A named community advisory board
- A community-governed host (the proposal calls for a Mukurtu instance run by a
  university archival studies programme or a Karnataka mental health NGO)

## Sources

- Carroll, Stephanie Russo, et al. "The CARE Principles for Indigenous Data Governance." *Data Science Journal*, vol. 19, no. 1, 2020, art. 43.
- Caswell, Michelle. "'The Archive' Is Not an Archives." *Reconstruction*, vol. 16, no. 1, 2016.
- Christen, Kimberly. "Does Information Really Want to Be Free?" *International Journal of Communication*, vol. 6, 2012, pp. 2870–93.
- Derrida, Jacques, and Eric Prenowitz. "Archive Fever: A Freudian Impression." *Diacritics*, vol. 25, no. 2, 1995, pp. 9–63.
- Mbembe, Achille. "The Power of the Archive and Its Limits." *Refiguring the Archive*, Kluwer, 2002, pp. 19–26.
- Stoler, Ann Laura. *Along the Archival Grain*. Princeton University Press, 2009.
