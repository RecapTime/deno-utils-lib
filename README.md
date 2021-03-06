# Utility Libraries for Recap Time projects in Deno

## Usage

```ts
// Either in mod.ts or straight to your Deno code via mod.ts

// Using Deno's official registry for 3rd-party packages with versioning
// Replace vYYYY.MM.XX with either the latest version or any previous ones.
import { longUrlBuilder, addLink } from "https://deno.land/x/recaptimedotdev_utils@vYYYY.MM.XX/lib/@recaptime-dev/firebase-dynamiclinks-web/mod.ts"

// Docs: https://firebase.google.com/docs/dynamic-links/create-manually
// The dynamicLinkPrefix key should be either your page.link subdomain or an custom domain used for Firebase Dynamic Links.
// longUrlBuilder will return an string where your parameters other than dynamicLinkPrefix are URL-encoded. 
const linkMetadata = longUrlBuilder({
    dynamicLinkPrefix: "https://recaptime.page.link", /* Custom domains: https://firebase.google.com/docs/dynamic-links/custom-domains */
    link: "https://gitpod.io/#gitlab.cm/gitpodify/templates/nodejs-deno",
    st: "Gitpodified Repo Starter Pack | gitpodify.dev",
    sd: "An template repository with TypeScript, some linters and other tools preloaded, alongside Node.js and Deno."
})

// Since our implementation doesn't init like the regular ones, please authenticate using your exisiting
// application's API key, preferably web apps registered to your Firebase project.
await addDynamicLink(Deno.env.FIREBASE_API_KEY, linkMetadata)

// Straight from GitHub/GitLab on main branch - NOT RECOMENDED IF USING LOCKFILE OR VENDORING
import { getCWData } from "https://github.com/RecapTime/deno-utils-lib/raw/main/lib/@community-radar-recaptime/content-warnings/mod.ts"

console.log(getCWData("https://www.youtube.com/watch?v=UKIlwncMbqo"))
// {
//  ok: "true",
//  result: {
//    hasCW: true,
//    reason: "Video flagged due to derealization by Dream Team Wiki admins",
//    addedBy: "https://gitlab.com/ajhalili2006"
//    linkToIssue: null,
//    linkToSource: "https://dreamteam.fandom.com/wiki/Template:ContentWarningData?direction=next&oldid=63721&action=raw",
//    cwShortlink: "https://contentwarnings.page.link/zXbp",
//    cwLonglink: "https://recaptime-contentwarnings.deno.dev/preview?url=https://www.youtube.com/watch?v%3DUKIlwncMbqo"
//  }
// }
```

```js
// dist.js for Node.js and elsewhere in an polyfilled dist.js in each subpackage
import { checkServiceStatus } from "https://cdn.deno.land/recaptimedotdev_utils@vYYYY.MM.XX/lib/@recaptime-dev/provisioning-api/dist.js"

console.log(checkServiceStatus("gitpodify.dev", "cloudsmith"))
// { ok: true, result: { url: "https://api.cloudsmith.io/v1/packages/gitpodify/gitpodified-workspace-images/", httpStatus: 200 } }
```


## Contributing

TBD
