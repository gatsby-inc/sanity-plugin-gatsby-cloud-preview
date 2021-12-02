# Gatsby Preview Sanity Plugin

A plugin that allows access to Gatsby Preview instances via an `Open Preview` button. The button will display in the document actions menu for all content types in your Sanity Studio. 

## Prerequisites

Your Gatsby site must be set up with a Gatsby Cloud instance. Make sure you are using the latest version of Gatsby core (`gatsby@latest`) and have `gatsby-source-sanity@7.3.0` or later installed in your Gatsby site. 

Install this plugin `sanity-plugin-gatsby-cloud-preview` in your Sanity Studio site. 

## Setup and Configuration

You will use the document actions extension to add a new action from this plugin. The document actions extension is available by default in Sanity Studio. 
### 1. Configure document actions in sanity.json

You can add a document actions resolver to your Sanity Studio instance by declaring it in the `sanity.json` file:

```jsx
// sanity.json 
//... 
"parts": [ 
  //... 
  { 
    "implements": "part:@sanity/base/document-actions/resolver", 
    "path": "resolveDocumentActions.js" 
  } 
]
```

The path will point to the document resolver file, which will be configured in the next step. If you do not have existing customizations, this file needs to be created.

### 2. resolveDocumentActions.js

The Open Preview Button will need to be appended on the existing document actions list. If you do not have existing customizations, the Open Preview action can be added as following:

```jsx
// resolveDocumentActions.js

// import the default document actions
import defaultResolve from "part:@sanity/base/document-actions";

import { gatsbyPreviewAction } from "sanity-plugin-gatsby-cloud-preview";

export default function resolveDocumentActions(props) {
  return [...defaultResolve(props), gatsbyPreviewAction];
}
```

If you have existing document actions configuration, you can append `gatsbyPreviewAction` to the return of the `resolveDocumentActions` function.

### 3. Configure Environment variables

Make sure `SANITY_STUDIO_CONTENT_SYNC_URL` is set as an environmental variable for your Studio instance. You can retrieve this URL by navigating to your site's Gatsby dashboard and navigating to Site Settings.

![Screen Shot 2021-11-17 at 12.19.25 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/82ec9e70-0f58-437e-beb9-3d0f1374b982/Screen_Shot_2021-11-17_at_12.19.25_PM.png)

### 4. Run your Studio

You can test content sync by running studio locally or hosting it. If set up correctly, you should see a new "Open Preview" option available under document actions preview:

![Screen Shot 2021-11-12 at 1.28.26 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cad24b8e-2931-463d-bad4-4ae056073242/Screen_Shot_2021-11-12_at_1.28.26_PM.png)

Clicking the button will redirect you to the preview page specific to the post or content. 

# Working with a Gatsby Starter

Gatsby starters have the "Open Preview" button enabled by default. Simply set your `SANITY_STUDIO_CONTENT_SYNC_URL` with the correct value. You should be able to run Studio and see your changes reflected in the Gatsby preview tab out of the box!