<!-- # Build & Release & Upload CI (Reusable Workflow) -->
# Github Reusable Workflow - Build & Release & Upload CI

This reusable workflow builds the project, creates a new release, and uploads the solution files to Azure blob storage.

***Inputs***
- ```node-version``` - **Optional** | number | Default: 16 | Node version.
- ```msbuildtarget``` - **Optional** | string | Default: Solution | The solution directory in the root path where the 'src/Other/Solution.xml' file is located.
- ```delete-old-version``` - **Optional** | boolean | Default: true | Delete old solution file(s) from Azure blob storage or not.
- ```release-solution-package-type``` - **Optional** | choice (unmanaged, managed, both) | Default: managed | The solution package type to add to the created release as assets.
- ```azure-solution-package-type``` - **Optional** | choice (unmanaged, managed, both) | Default: managed | The solution package type to upload to Azure blob storage.
