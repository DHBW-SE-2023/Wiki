# Project Structure
The Structures specific Requirements and developent are discussed [here](https://github.com/DHBW-SE-2023/YAAC/pull/15).

## Structural Layout
The project is structured around [this layout](https://github.com/golang-standards/project-layout). YAAC relies on [Fyne](https://fyne.io/) for it's frontend. Golang prohibits cyclic imports which makes a traditional [MVVM](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93viewmodel) structure where packages import eachother imposible. However, go interfaces allow to circumvent this issue. YAAC implements a structure based on [this](https://jogendra.dev/import-cycles-in-golang-and-how-to-deal-with-them) article. 

### Guide
YAAC contains templates for all internal packages with comments explaing how to setup MVVM correctly.

## Folder Layout
```
root
├─assets
├─cmd
├─yaac
├─docs
├─internal
├─backend
├─frontend
├─mvvm
├─shared
├─pkg
└─test
```

### Description
**assets**
> Other assets to go along with your repository (images, logos, etc).


**cmd**
> Main applications for this project. The directory name for each application should match the name of the executable you want to have (e.g., /cmd/myapp). Don't put a lot of code in the application directory. If you think the code can be imported and used in other projects, then it should live in the /pkg directory. If the code is not reusable or if you don't want others to reuse it, put that code in the /internal directory. You'll be surprised what others will do, so be explicit about your intentions!


**cmd/yaac**
> YAAC's main package


**docs**
> Design and user documents (in addition to your godoc generated documentation).


**internal**
> Private application and library code. This is the code you don't want others importing in their applications or libraries. Note that this layout pattern is enforced by the Go compiler itself.


**internal/backend**
> Backend packages are placed in sufolders of this directory. The naming theme is `yaac_backend_YOURPACKAGE`.


**internal/frontend**
> Frontend packages are placed in sufolders of this directory. The naming theme is `yaac_frontend_YOURPACKAGE`.


**internal/mvvm**
> The MVVM is one single package with it's functionallities split accross files in this folder. 


**internal/shared**
> This is a single package containing information meant to be globally accessible. `yaac_shared` should never import other `yaac` packages.


**pkg**
> Place public/external packages here.


**test**
> Additional external test apps and test data. Feel free to structure the /test directory anyway you want. For bigger projects it makes sense to have a data subdirectory. For example, you can have /test/data or /test/testdata if you need Go to ignore what's in that directory. Note that Go will also ignore directories or files that begin with "." or "_", so you have more flexibility in terms of how you name your test data directory.


# Credits
- https://github.com/golang-standards/project-layout
- https://jogendra.dev/import-cycles-in-golang-and-how-to-deal-with-them


Back to main page [here](https://github.com/DHBW-SE-2023/Wiki/blob/main/README.md).