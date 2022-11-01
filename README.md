# Github Reusable Workflow - Build & Release & Upload CI
> *Used within Bever.*

This reusable workflow builds the project, creates a new release, and uploads the solution file(s) to Azure blob storage.

**Inputs**
- ```node-version``` - **Optional** | **string** | Default: 16 | Node version.
- ```msbuildtarget``` - **Optional** | **string** | Default: Solution | The solution directory in the root path where the 'src/Other/Solution.xml' file is located.
- ```delete-old-version``` - **Optional** | **boolean** | Default: true | Delete old solution file(s) from Azure blob storage or not.
- ```release-solution-package-type``` - **Optional** | **choice (none / unmanaged / managed / both)** | Default: none | The solution package type to add to the created release as assets.
- ```azure-solution-package-type``` - **Optional** | **choice (unmanaged / managed / both)** | Default: managed | The solution package type to upload to Azure blob storage.

**Outputs**
- ```solution-unique-name``` - **string** | The solution unique name. | *Example: SampleCustomComponent*
- ```solution-version``` - **string** | The solution version. | *Example: 1.0.0*
- ```solution-parsed-version``` - **string** | The solution parsed version. | *Example: 1_0_0*
- ```release-id``` - **string** | Created release ID.
- ```release-name``` - **string** | Created release name. | *Example: v1.0.0*
- ```release-tag-name``` - **string** | Created release tag name. | *Example: v1.0.0*
- ```release-url``` - **string** | Created release URL, the URL users can navigate to in order to view the release. | *Example: https://github.com/BeverCRM/PCF-SampleCustomComponent/releases/tag/v1.0.0*
- ```unmanaged-zip-exists``` - **boolean** | Whether the unmanaged solution exists or not.
- ```managed-zip-exists``` - **boolean** | Whether the managed solution exists or not.
