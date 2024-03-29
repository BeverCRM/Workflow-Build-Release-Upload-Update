# Github Reusable Workflow - Build & Release & Upload & Update
> ***Note*** *Used within Bever*

<br>
This is a reusable workflow that builds the project, creates a new release, uploads the solution files to Azure Blob Storage, and updates the Azure SQL Database.

## Usage

### Prerequisites
Create a workflow ```.yml``` file in your ```.github/workflows``` directory. An [example workflow](https://github.com/BeverCRM/Workflow-Build-Release-Upload-Update#example-workflow-publish-on-marketplace-ci) is available below. For more information, reference the GitHub Help Documentation for [creating a workflow file](https://docs.github.com/en/actions/using-workflows#creating-a-workflow-file).

<br>

### Inputs
<table>
  <tr>
    <th>Name</th>
    <th>Required</th>
    <th>Type</th>
    <th>Default</th>
    <th>Options</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>control-title</td>
    <td>Required</td>
    <td>string</td>
    <td>---</td>
    <td>---</td>
    <td>Control title</td>
  </tr>
  <tr>
    <td>control-description</td>
    <td>Optional</td>
    <td>string</td>
    <td>---</td>
    <td>---</td>
    <td>Control description (included in use-default)</td>
  </tr>
  <tr>
    <td>control-youtube-video-url</td>
    <td>Optional</td>
    <td>string</td>
    <td>---</td>
    <td>---</td>
    <td>Control youtube video url</td>
  </tr>
  <tr>
    <td>control-thumbnail-url</td>
    <td>Optional</td>
    <td>string</td>
    <td>---</td>
    <td>---</td>
    <td>Control thumbnail url (included in use-default)</td>
  </tr>
  <tr>
    <td>control-primary-image-url</td>
    <td>Optional</td>
    <td>string</td>
    <td>---</td>
    <td>---</td>
    <td>Control primary image url (included in use-default)</td>
  </tr>
  <tr>
    <td>control-markdown-file-url</td>
    <td>Optional</td>
    <td>string</td>
    <td>---</td>
    <td>---</td>
    <td>Cotnrol markdown file url (included in use-default)</td>
  </tr>
  <tr>
    <td>control-tags</td>
    <td>Optional</td>
    <td>string</td>
    <td>Bever-Controls, PCF</td>
    <td>---</td>
    <td>Control tags (comma separated | added by default `Bever-Controls, PCF, &lt;control unique name&gt;`)</td>
  </tr>
  <tr>
    <td>solution-folder</td>
    <td>Optional</td>
    <td>string</td>
    <td>Solution</td>
    <td>---</td>
    <td>Final solution directory</td>
  </tr>
  <tr>
    <td>pcfproj-prefix</td>
    <td>Optional</td>
    <td>string</td>
    <td>PCF-</td>
    <td>---</td>
    <td>File name prefix of the .pcfproj</td>
  </tr>
  <tr>
    <td>release-solution-package-type</td>
    <td>Optional</td>
    <td>string</td>
    <td>managed</td>
    <td>none, unmanaged, managed, both</td>
    <td>The solution package type to add to the created release as assets</td>
  </tr>
  <tr>
    <td>azure-solution-package-type</td>
    <td>Optional</td>
    <td>string</td>
    <td>managed</td>
    <td>unmanaged, managed, both</td>
    <td>The solution package type to upload to Azure blob storage</td>
  </tr>
  <tr>
    <td>create-new-release</td>
    <td>Optional</td>
    <td>boolean</td>
    <td>true</td>
    <td>---</td>
    <td>Create a new release on GitHub or not</td>
  </tr>
  <tr>
    <td>delete-old-version-from-azure</td>
    <td>Optional</td>
    <td>boolean</td>
    <td>true</td>
    <td>---</td>
    <td>Delete the old solution directory from Azure blob storage or not</td>
  </tr>
  <tr>
    <td>use-default</td>
    <td>Optional</td>
    <td>boolean</td>
    <td>true</td>
    <td>---</td>
    <td>Use default information for control inputs</td>
  </tr>
  <tr>
    <td>node-version</td>
    <td>Optional</td>
    <td>number</td>
    <td>16</td>
    <td>---</td>
    <td>Node version</td>
  </tr>
</table>

<br>

### Outputs
<table>
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Description</th>
    <th>Example</th>
  </tr>
  <tr>
    <td>solution-unique-name</td>
    <td>string</td>
    <td>The solution unique name</td>
    <td>SampleCustomComponent</td>
  </tr>
  <tr>
    <td>solution-version</td>
    <td>string</td>
    <td>The solution version</td>
    <td>1.0.0</td>
  </tr>
  <tr>
    <td>solution-parsed-version</td>
    <td>string</td>
    <td>The solution namespace</td>
    <td>1_0_0</td>
  </tr>
  <tr>
    <td>solution-namespace</td>
    <td>string</td>
    <td>The solution parsed version</td>
    <td>BeverControls</td>
  </tr>
  <tr>
    <td>release-id</td>
    <td>string</td>
    <td>Created release ID</td>
    <td></td>
  </tr>
  <tr>
    <td>release-name</td>
    <td>string</td>
    <td>Created release name</td>
    <td>v1.0.0</td>
  </tr>
  <tr>
    <td>release-tag-name</td>
    <td>string</td>
    <td>Created release tag name</td>
    <td>v1.0.0</td>
  </tr>
  <tr>
    <td>release-url</td>
    <td>string</td>
    <td>Created release URL, the URL users can navigate to in order to view the release</td>
    <td>https://github.com/BeverCRM/PCF-SampleCustomComponent/releases/tag/v1.0.0</td>
  </tr>
</table>

<br>

### Example workflow: publish-on-marketplace-ci.yml
On every *push* (or *pull request merge*) on the *release* branch, run this workflow.

```yaml
name: Create a new release and upload the solution to Azure blob storage CI

on:
  push:
    branches: release

jobs:
  main:
    uses: BeverCRM/Workflow-Build-Release-Upload-Update/.github/workflows/build-release-upload-update-rw.yml@master
    secrets: inherit
    with:
      control-title: Sample Custom Component # required
      # control-description: '' # default
      # control-youtube-video-url: '' # default
      # control-thumbnail-url: '' # included in use-default
      # control-primary-image-url: '' # included in use-default
      # control-markdown-file-url: '' # included in use-default
      # control-tags: Bever-Controls, PCF # added by default
      # solution-folder: Solution # default
      # pcfproj-prefix: PCF- # default
      # release-solution-package-type: managed # default
      # azure-solution-package-type: managed # default
      # create-new-release: true # default
      # delete-old-version-from-azure: true # default
      # use-default: true # default
      # node-version: 16 # default
```

<br>

---

**For more information on how to create a PCF repository see [BeverCRM/Template-PCF](https://github.com/BeverCRM/Template-PCF).**
