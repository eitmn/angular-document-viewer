

# ngx-doc-viewer

This component can be used to show several different document types in an Angular app.

Documents that are publicly available can be shown in an iframe using the google or office document viewer.

Pdf files and word document that are not publicly available can be shown using the mammoth viewer or pdf viewer by passing an objectUrl.

<a href="https://angular-doc-viewer.firebaseapp.com/">View demo</a>

<a href="https://github.com/Marcelh1983/angular-document-viewer/blob/master/changelog.md">Changes</a>

### Install the NPM Module
```sh
npm install ngx-doc-viewer --save
```

### Usage

#### 1. Import `NgxDocViewerModule` 

```ts
@NgModule({
    imports: [NgxDocViewerModule]
  })
  export class AppModule { }
```

#### 2. Add DocViewer to component:

```html
    <ngx-doc-viewer [url]="doc" viewer="google" style="width:100%;height:50vh;"></ngx-doc-viewer>
```

To 

#### API:

Input: 
- url: document url.
- viewer: google (default), office, mammoth or pdf
- queryParams, e.g. to set language. for google: hl=[lang] e.g. hl=nl
- disableContent: 'none' | 'all' | 'popout' | 'popout-hide' = 'none': 
    - none: no overlay
    - all: adds an overlay to the whole iframe, which makes nothing in the document clickable/selectable
    - popout: adds an overlay over googles popout button or office popout and menu which disables just this button/menu but keeps giving the possibility to select text. The popout button is still visible (for google during a few seconds) but not clickable.
    - popout-hide: see popup, instead of an transparent overlay a white one. This really hides the button but you'll see a white block while loading for the google viewer.

There are some issues loading document in the google viewer. See: https://stackoverflow.com/questions/40414039/google-docs-viewer-returning-204-responses-no-longer-working-alternatives. If loading pdf's and Word documents, seems to work now with this hack let me know via a Github issue. 

- googleCheckContentLoaded = true | If true it will check by interval if the content is loaded.
- googleCheckInterval = 3000 | The interval in milliseconds that is checked whether the iframe is loaded.

Output:
- loaded: google only, notifies when iframe is loaded. Can be used to show progress while loading 

### File type support

#### office viewer
.ppt, .pptx, .doc, .docx, .xls and .xlsx

#### google viewer

Only files under 25 MB can be previewed with the Google Drive viewer.

Google Drive viewer helps you preview over 15 different file types, listed below:

* Text files (.TXT)
* Markup/Code (.CSS, .HTML, .PHP, .C, .CPP, .H, .HPP, .JS)
* Microsoft Word (.DOC and .DOCX)
* Microsoft Excel (.XLS and .XLSX)
* Microsoft PowerPoint (.PPT and .PPTX)
* Adobe Portable Document Format (.PDF)
* Apple Pages (.PAGES)
* Adobe Illustrator (.AI)
* Adobe Photoshop (.PSD)
* Tagged Image File Format (.TIFF)
* Autodesk AutoCad (.DXF)
* Scalable Vector Graphics (.SVG)
* PostScript (.EPS, .PS)
* TrueType (.TTF)
* XML Paper Specification (.XPS)
* Archive file types (.ZIP and .RAR)

<a href="https://gist.githubusercontent.com/tzmartin/1cf85dc3d975f94cfddc04bc0dd399be/raw/d4263c8faf7b68f4bbfd33b386ec33ed2bc11e7d/embedded-file-viewer.md">Source</a>

### pdf

.pdf

NOTE: PDF's are shown in the embed tag. Browser support is not guaranteed. If you need to be sure the pdf renders on all browsers you better use PDF.js

### mammoth

.docx

To use mammoth, also add: 
```sh
npm install mammoth --save
```
and make sure mammoth.browser.min.js is loaded. For the angular/cli you would add the following in angular.json:

```json
    "scripts": [
        "node_modules/mammoth/mammoth.browser.min.js"
    ]
```

