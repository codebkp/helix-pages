# helix-pages

[![CircleCI](https://img.shields.io/circleci/project/github/adobe/helix-pages.svg)](https://circleci.com/gh/adobe/helix-pages)

Helix Pages is the Helix project behind [https://*.project-helix.page/](https://www.project-helix.page/)

## Installation

Clone the current repo and run `hlx up`.

## Deployment and publication

Direct commits to `master` branch are blocked, all changes must come via a PR. Once the PR is merged into `master`, the CI will `hlx deploy` and `hlx publish` the new code.

## Manual publishing

The project requires some extensions of the default VCL provided by Helix. The publish steps requires to include the extensions in [vcl/extensions.vcl](vcl/extensions.vcl). To publish, run:

```bash
 hlx publish --custom-vcl='vcl/extensions.vcl'
```

The patched version of the 3 subroutines adds the parsing of the host url to extract the content owner / repo that would override the one stored in the Fastly dictionary.

## Automatic publishing

Go to your Google Drive account
 * https://drive.google.com/drive/my-drive

Create a new shared folder to hold the website root
 * Click on the button “+ New” > Folder
 * Give the folder a name (e.g., sitename)
 * Double-click the sitename folder to open

Share the folder with helix
 * Select the menu arrow after MyDrive > sitename > Share with others ...
 * Share it with helix.integration@gmail.com
 * Give helix write permission (necessary for ???)
 * Copy the folder URL (e.g., https://drive.google.com/drive/folders/{id} )

Create a domain mount point on GitHub
 * Go to your GitHub home (e.g., https://github.com/username/ )
 * Select Repositories tab and green New button
 * Create a new repository
   * Give it a short name (for the domain)
   * Make it Public
 * Inside repository, create a new file “fstab.json” with content:
```
{ "mountpoints": [ {
      "root": "/",
      "url": "https://drive.google.com/drive/folders/{id}"
} ] }
```
where “url” is the Google Drive folder URL above

Create a file for each page of the site
 * Use drag & drop or the button “+ New” > Google Docs 
 * Change the filename to index (no extension) or a page name (no extension)
 * Be sure to add an image (bug) and make a Heading 1 style title

Type your new website URL into a browser:
```
  https://{repo}-{username}.hlx.page/index.html
```
