# GitHub Actions Ci/Cd pipeline

The `main.yml` file in `.github/workflows` contains the functionallity of the pipeline. 

## Purpose
The pipelines main purpose is to check if commited code compiles in a static environment. It is also capable of performing tests to check code copliance.

## Sections
The configured root sections are:
- name
   - The pipeline's name
- on
   - Triggers to start the pipeline
      - Currently configured to act on pull-requests in the `dev` branch
- jobs
  - Tasks to perform when the pipeline starts

## Jobs
### build-docker - Build and Test
This job performs several steps to build and test yaac.
- Checkout code
   - Retrieves yaac's repo on the correct branch with pull-request and make it the default starting directory.
- Get Go
   - Installs go in the correct version. Should also cache go pkg dependencies.
- Get CMake
   - Installs CMake.
- Build and Cache OpenCV
   - Builds OpenCV and Caches the result for future runs.
- Update pkg list
   - Update apt's package list.
- Install and Cache Fyne Dependencies
   - Install and cache Fyne's dependencies for future runs.
- Install and configure opencv build
   - Install the build/cached OpenCV from it's build folder.
- Build
   - Build yaac.
- Test
   - Perform all tests in `YAAC/test/`
- Upload Artifact
  - Upload the build artefact.


Back to main page [here](https://github.com/DHBW-SE-2023/Wiki/blob/main/README.md).