# Firebase Tools Issue #3359
MCVE for https://github.com/firebase/firebase-tools/issues/3359

## Steps to reproduce

1. Delete contents of `us.artifacts.<project name here>.appspot.com` for any existing project (or clone and use this repo).
2. Try `firebase deploy` and it fails:

```console
$ firebase deploy

=== Deploying to 'trial-3f17b'...

i  deploying functions, hosting
Running command: npm --prefix "$RESOURCE_DIR" run lint

> lint
> eslint .

+  functions: Finished running predeploy script.
i  functions: ensuring required API cloudfunctions.googleapis.com is enabled...
i  functions: ensuring required API cloudbuild.googleapis.com is enabled...
+  functions: required API cloudbuild.googleapis.com is enabled
+  functions: required API cloudfunctions.googleapis.com is enabled
i  functions: preparing functions directory for uploading...
i  functions: packaged functions (68.54 KB) for uploading
+  functions: functions folder uploaded successfully
i  hosting[trial-3f17b]: beginning deploy...
i  hosting[trial-3f17b]: found 2 files in public
+  hosting[trial-3f17b]: file upload complete
i  functions: updating Node.js 14 (Beta) function helloWorld(us-central1)...

Functions deploy had errors with the following functions:
        helloWorld(us-central1)

To try redeploying those functions, run:
    firebase deploy --only "functions:helloWorld"

To continue deploying other features (such as database), run:
    firebase deploy --except functions

Error: Functions did not deploy properly.
```

3. Delete `us.artifacts.<project name here>.appspot.com` bucket and retry. It deploys:

```console
$ firebase deploy

=== Deploying to 'trial-3f17b'...

i  deploying functions, hosting
Running command: npm --prefix "$RESOURCE_DIR" run lint

> lint
> eslint .

+  functions: Finished running predeploy script.
i  functions: ensuring required API cloudfunctions.googleapis.com is enabled...
i  functions: ensuring required API cloudbuild.googleapis.com is enabled...
+  functions: required API cloudbuild.googleapis.com is enabled
+  functions: required API cloudfunctions.googleapis.com is enabled
i  functions: preparing functions directory for uploading...
i  functions: packaged functions (68.54 KB) for uploading
+  functions: functions folder uploaded successfully
i  hosting[trial-3f17b]: beginning deploy...
i  hosting[trial-3f17b]: found 2 files in public
+  hosting[trial-3f17b]: file upload complete
i  functions: updating Node.js 14 (Beta) function helloWorld(us-central1)...
+  functions[helloWorld(us-central1)]: Successful update operation.
i  hosting[trial-3f17b]: finalizing version...
Function URL (helloWorld): https://us-central1-trial-3f17b.cloudfunctions.net/helloWorld
+  hosting[trial-3f17b]: version finalized
i  hosting[trial-3f17b]: releasing new version...
+  hosting[trial-3f17b]: release complete

+  Deploy complete!

Project Console: https://console.firebase.google.com/project/trial-3f17b/overview
Hosting URL: https://trial-3f17b.web.app
```
