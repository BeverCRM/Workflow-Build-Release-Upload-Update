# Github Reusable Workflow - Build & Release & Upload CI
> *Used within Bever*

This is a reusable workflow that builds the project, creates a new release, and uploads the solution files to Azure blob storage.

## Usage

### Pre-requisites
Create a workflow ```.yml``` file in your ```.github/workflows``` directory. An [example workflow](https://github.com/BeverCRM/Workflow-Build-Release-Upload-CI#example-workflow-create-release-and-upload-solution-to-azure-storage-ci) is available below. For more information, reference the GitHub Help Documentation for [creating a workflow file](https://docs.github.com/en/actions/using-workflows#creating-a-workflow-file).

### Inputs
- ```node-version``` - **Optional** | **number** | Default: 16 | Node version.
- ```msbuildtarget``` - **Optional** | **string** | Default: Solution | The solution directory in the root path where the 'src/Other/Solution.xml' file is located.
- ```delete-old-version``` - **Optional** | **boolean** | Default: true | Delete old solution file(s) from Azure blob storage or not.
- ```release-solution-package-type``` - **Optional** | **string** | Default: managed | Options: (none / unmanaged / managed / both) | The solution package type to add to the created release as assets.
- ```azure-solution-package-type``` - **Optional** | **string** | Default: managed | Options: (unmanaged / managed / both) | The solution package type to upload to Azure blob storage.

### Outputs
- ```solution-unique-name``` - **string** | The solution unique name. | *Example: SampleCustomComponent*
- ```solution-version``` - **string** | The solution version. | *Example: 1.0.0*
- ```solution-parsed-version``` - **string** | The solution parsed version. | *Example: 1_0_0*
- ```release-id``` - **string** | Created release ID.
- ```release-name``` - **string** | Created release name. | *Example: v1.0.0*
- ```release-tag-name``` - **string** | Created release tag name. | *Example: v1.0.0*
- ```release-url``` - **string** | Created release URL, the URL users can navigate to in order to view the release. | *Example: https://github.com/BeverCRM/PCF-SampleCustomComponent/releases/tag/v1.0.0*
- ```unmanaged-zip-exists``` - **boolean** | Whether the unmanaged solution exists or not.
- ```managed-zip-exists``` - **boolean** | Whether the managed solution exists or not.

### Example workflow: create-release-and-upload-solution-to-azure-storage-ci
On every *push* or *pull request* on the *release* branch, run this workflow.

```yaml
on:
  push:
    branches: [ release ]
  pull_request:
    branches: [ release ]

name: Create a new release and upload the solution to Azure blob storage CI

jobs:
  main:
    uses: BeverCRM/Workflow-Build-Release-Upload-CI/.github/workflows/build-release-upload-ci.yml@master
```
