# 11ty-notion-api

> Last Update: 2022-02-16  
> switched to database approach instead of parent root page

[![Netlify Status](https://api.netlify.com/api/v1/badges/743e0288-f4c6-4ba0-9537-e74b2134cf95/deploy-status)](https://app.netlify.com/sites/11ty-notion-cms/deploys)

**Current state**: [https://11ty-notion-cms.netlify.app/](https://11ty-notion-cms.netlify.app/)

Proof-of-concept for fetching pages / blocks from Notion (via official [Notion API beta](https://developers.notion.com/changelog)) with the Eleventy static website builder's global data functionality. Idea is to use this approach to build static websites from a Notion database as a content-rich headless CMS.

> For a slightly different / more elegant approach for processing the blocks (with `getBlock()`) and local asset caching, see @FalconSensei's [post](https://geekosaur.com/post/eleventy-notion-notes-section/).

![](https://pbs.twimg.com/media/E8dX4i5WUAcLcQL?format=png&name=4096x4096)

> See the [Notion Source Document](https://fubits.notion.site/Notion-CMS-DB-Eleventy-3f2bdcd9db7d4264bd2bed28c2b67655)

## Quickstart

- `git clone`
- `npm install`
- create `.env` for `{dotenv}`
  - add `NOTION_API_KEY="your_token"`
  - add `MAIN_PAGE="id-of-notion-database"`
- `npm run dev`

> also add both ENV variables to the Deploy Settings on Netlify

## Building Blocks

1. `src/_data/database.js`: Fetch ~~pages~~ database entries (~pages) from Notion

   - `.cache/**`: cache locally
   - `json/articles.json`: store / track locally (optional)

2. `utils/parsePage.js`: Process the blocks (of `type: supported` or with custom `[shortcodes]`)]) with JS
3. `src/index.njk`: Render / parse the blocks with Eleventy
4. `src/css/notion.css`: Notion-specific CSS rules (i.e. colors)

## TODO

- [x] implement page retrieval
- [ ] abandon `{{- elem | safe -}}`
- [ ] implement [database](https://developers.notion.com/reference/database) retrieval
  - [ ] implement page / db entry metadata (front matter)
- [ ] Eleventy: use a blog template / logic
- [x] figure out how to wrap the parent-less list items in `<ul></ul>`
- [x] implement shortcodes for
  - [x] `[blockquote 'payload']` (now obsolete)
  - [x] `[img 'url' 'figcaption']` (now obsolete)
  - [x] `[footnote 'payload']` (as `<sup></sup>`)
- [x] add formatting for Headings
- [ ] figure out how to enable CSS edge cases such as `text-decoration: underline line-through`
- [ ] implement more block types
  - [x] implement `[code]`
  - [x] implement `[todo]`
  - [x] implement `[callout]`
  - [x] implement `[quote]`
  - [x] implement `[image]`
    - [ ] add local caching / download
  - [ ] implement `[video]`
  - [ ] implement `[embed]`
  - [ ] implement `[file]`
  - [ ] implement internal hyperlinks (within website)
