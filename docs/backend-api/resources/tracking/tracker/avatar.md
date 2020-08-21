---
title: /avatar
description: /avatar
---

API base path: `/tracker/avatar`

### upload
Upload avatar image for specified tracker.
Then it will be available from `[api_base_url]/[api_static_path]/tracker/avatars/<file_name>`
e.g. `{{ extra.api_example_url }}/static/tracker/avatars/abcdef123456789.png`.

**required subuser rights:** tracker_update

**MUST** be a POST multipart request (multipart/form-data),
with one of the parts being an image file upload (with the name “file”).

File part **mime** type must be one of (see: [source:api-server/src/main/java/com/navixy/common/util/ImageFormats.java ImageFormats.IMAGE_FORMATS]):
*    **image/jpeg** or **image/pjpeg**
*    **image/png**
*    **image/gif**

#### parameters
* **tracker_id** - tracker id
* **file** - image file
* **redirect_target** - (optional) URL to redirect If redirect_target passed return redirect to ?response=

#### response
```js
{
    "success": true,
    "value": <string> // avatar file name
}
```

#### errors
*   201 – Not found in database (when tracker with tracker_id not found in db)
*   208 – Device blocked
*   233 – No data file (if file part not passed)
*   234 – Invalid data format (if passed file with unexpected mime type)
*   254 – Cannot save file (on some file system errors)