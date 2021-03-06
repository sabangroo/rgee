---
title: "NEWS"
output:
  html_document:
    toc: true
    toc_float:
      collapsed: false
      smooth_scroll: false
    toc_depth: 2
vignette: >
  %\VignetteIndexEntry{NEWS}
  %\VignetteEncoding{UTF-8}
---
# rgee 1.0.4
- Add `ee_help` a new Rstudio addins that mimics the help Rstudio interface (F1).
- Fix a bug that makes that `ee_as_sf` only supports `GeoJSON` format.
- If `dsn` is not specified in `ee_as_sf`, it will create a temporary shapefile (in \tmp dir).
- Fix a bug in `ee_imagecollection_to_local` (#87 Thanks @cedlfc44)
- Fix a bug in `ee_image_local` (#88 Thanks @cedlfc44)
- Fix a bug in `ee_create_credentials_drive` (#90 #78 Thanks @cedlfc44)

# rgee 1.0.3
- getPass library removed from `ee_Initialize`.
- New argument `display` in `ee_Initialize` to return the authentication URI. Useful for `rgee` colab users.
- Changes in some diagnostic messages to make possible to use `rgee` in colab.
- `ee_help` returns a HTML file rather than TRUE. It also now supports characters (e.g. `ee_help("ee$Image")`).
- Fix a strange bug when `ee_Initialize` tries to connect to reticulate the first time.
- Fix small bugs in `ee_user_info` and `ee_users`

# rgee 1.0.2
- Earth Engine Python API updated to 0.1.229.
- Fix a bug in `ee_Initialize`, that does not permit users to use `ee_createAssetHome` to define their *Earth Engine Assets home root folder*

# rgee 1.0.1
- Earth Engine Python API updated to 0.1.228.
- `ee_Initialize` now set the global env "RETICULATE_PYTHON" rather than .onLoad

# rgee 1.0.0
- We implement `ee_createAssetHome` to help users to define their *Earth Engine Assets home root folder* without leaving ee_Initialize(). (#70 Thanks @jhollist)
- Fix a bug in `ee_Initialize(drive = TRUE, gcs = TRUE)` which do not permit users save credentials. (#72 Thanks @appelmar).
- Removed `check_ring_dir` argument from `sf_as_ee`. Now `rgee` expect that users fix potential geometry problems before upload geometries to their Earth Engine assets.
- Changes in "welcome to rgee"  message (located in `ee_Initialize`). We delete `stop("Initialization aborted")` and implement `ee_search_init_message`. It will permit to `rgee` to know if the user accepted to create the global var "EARTHENGINE_INIT_MESSAGE" without need to restart the R session.
- Fix minor bugs in `sf_as_ee` and `gcs_to_ee_table`. The argument `command_line_tool_path` was added to give users the option to set the path of the Earth Engine command linetool. This new argument is only relevant to upload files using Google Cloud Storage. New diagnostic message were added.
- Now `sf_as_ee` returns an `ee$Geometry$...` when `x` is a `sfg` or a single sfc object. If `x` is a sf or a `sfc` object with multiple geometries will return an `ee$FeatureCollection`. New unit test for `sf_as_ee`.
- Changes in the documentation of `ee_as_stars` and `ee_as_raster` (#72 Thanks @appelmar).
- Fix minor bugs in `raster_as_ee`, `stars_as_ee` and `gcs_to_ee_image`. The argument `command_line_tool_path` was added to give users the option to set the path of the Earth Engine command linetool. New diagnostic message were added. New unit test added.
- Fixed a bug in `stars_as_ee` that didn't allow to read single-band images.
- `ee_manage_asset_access` has a better approach to determine the user owner of the asset.
- Add a new logical argument called 'strict' to `ee_manage_assetlist`, `ee_manage_copy`,
`ee_manage_move`, `ee_manage_set_properties` and `ee_manage_delete_properties`. If TRUE, 
the existence of the asset will be evaluate before to perform the task. By default TRUE.
- If the `path_asset` is not specified in `ee_manage_assetlist`, rgee will assume that the
path_asset is `ee_get_assethome`.
- `raster_as_ee.R` was created in the /R folder to maintain an order between functions
to upload and download images.
- Fix a bug in the documentation of `print.ee.computedobject.ComputedObject()` (#72 Thanks @appelmar).
- Fix a bug in `ee_install_set_pyenv` now users can set `py_path` without set 
`py_env` and  vice versa.
- `ee_extract` was adapted to work well with changes in `sf_as_ee`.
- R CMD check is more friendly with users, the use of `--run-dontrun` is also 
available (#72 Thanks @appelmar).
- Fix a bug in `ee_get_date_ic`.
- `Map$addLayer` now could display a legend when `eeObject` is an one-band `ee$Image` (By default legend = TRUE).
- New function `ee_get`: Return the element at the specified position in a Earth Engine Collection.
- New function `Map$addLayers`: Create interactive visualizations of ImageCollections.
- Fix a bug: "OverflowError: Python int too large to convert to C long" in `ee_monitoring` (#79 Thanks @andreatitolo).
- Earth Engine Python API updated to 0.1.227.

# rgee 0.6.2
- Earth Engine Python API updated to 0.1.226.
- Fix some typos.
- Fix a minor bug in ee_monitoring.
- Users can mix mapview and EarthEnginemap objects in the same pipeline (see Examples in `Map$addLayer`).
- Add `ee_as_mapview`, a function to convert `EarthEnginemap` objects to  `mapview` objects.
- add a new logical argument called 'strict' to **ee_manage_delete**. If TRUE, the existence of the asset will be evaluate before to perform the task.
- Fix a bug in ee_Initialize, now users without an Earth Engine Assets home root will see a message.
- Fix a minor bug when ee_Initialize change of user, now before to change of user the GCS and GD credentials will be deleted.
- ee_check completely renovated. 
  - New diagnostic messages.
  - Fix a minor bug when testing GCS credentials.
  - The file ee_check.py was deleted.
- Roy Samapriya added as a contributor.  

# rgee 0.6.1
- Fix some typos.
- rgee website update.
- Add citation package option .
- Additional export arguments add to ee_as_stars,ee_as_raster,  ee_imagecollection_to_local and ee_as_sf.

# rgee 0.6.0 
- Earth Engine Python API updated to 0.1.225.
- Fix some typos.
- DESCRIPTION: Moving leaflet, mapview, geojsonio, sf and stars from Import to Suggest. Now users with installation problems can equally use the Earth Engine API although with less operability.
- The 'EarthEngineMap' S4 class was created to avoid incompatibilities with mapview.
- Fix a critical bug in **ee_install** due to the lack of breaks in repeat bucles.
- New function **ee_install_upgrade**.
- New global environment EARTHENGINE_PYTHON was created to help **ee_install_upgrade** to identify the Python environment used by rgee.

# rgee 0.5.4
- Earth Engine Python API updated to 0.1.224.
- Fix a Map typo.
- Fix a bug in ee_as_thumbnail, now the vizparams are checked before to pass to ee$Image$getThumbURL(...).
- ee is now an internal rgee environment.
- ee_reattach was deleted.
- ee_print now display the ee$Image properties: system:id, system:time_start and system:time_end.
- rgee now asks users if they would like to save EARTHENGINE_PYTHON in the .Renviron.

# rgee 0.5.3
- Fix a bug in ee_check_python_packages.
- \donttest changed by \dontrun in the documentation.
- gdal and v8 system dependencies added to GH actions.
- Fix a bug in the paper (`ee_extract` example).
- Fix a minor bug in `ee_extract`, now the argument ... works.
- `ee_table_to_drive`: changed the initial value of the argument folder from NULL to "rgee_backup".
- Fix a minor bug in `ee_monitoring`.
- Fix a minor bug in `ee_manage_cancel_all_running_task`.
- Fix a minor bug in `ee_manage_cancel_all_running_task`.
- Improvement in the documentation of `ee_install`.
- Changes in vignettes, `Best Practices` vignette added.

# rgee 0.5.2
- DESCRIPTION: single quotes in title and description.
- DESCRIPTION: A more compressible description of what rgee does.
- DESCRIPTION: Added web reference to the Earth Engine API.
- \dontrun changed by \donttest in all our examples.
- Added "#' @return" to several functions.
- Added "#' @family" to all the functions.
- Added 'quiet' argument to all the functions that needed.
- Added new contributors to rgee (Kevin Ushey, Tim Appelhans, JJ Allaire, Yuan Tang).
- New environmental variable for rgee "EARTHENGINE_INIT_MESSAGE". It will be used to display a message to new users.
- Earth Engine Python API updated to 0.1.223.
- Documentation updated for ee_print and ee_manage_*.
- Fix a bug in ee_install_set_pyenv that did not permit to create properly
the .Renviron_backup file.

# rgee 0.5.1
- ee_install_* functions were deprecated and replaced by ee_install. ee_install create an isolated Python virtual environment with all rgee dependencies.
- ee_install_set_pyenv can be used to set the EARTHENGINE_PYTHON variable.

# rgee 0.5.0
- **First attempt to submit to CRAN**
- Several typos fixed.
- rgee paper added.
- GitHub actions for automated testing and build the website.
- Due the changes in latest `reticulate` version (1.1.5), the functions `ee_install_earthengine_upgrade` and `ee_install_python_packages` were deprecated and both will remove in rgee 0.5.3.
- Config/reticulate added to DESCRIPTION file.
- .onLoad IMPORTANT CHANGES: Now `rgee` set EARTHENGINE_PYTHON instead of RETICULATE_PYTHON directly and RETICULATE_PYTHON_ENV is no longer required. This change will permit users to avoid problems with other R packages that use Python in the backend (such as tensorflow or keras).
- `ee_search_display` function added.
- Several typos fixed in all the documentation.
- Minor changes in `ee_as_sf` to support ee$FeatureCollections without elements.
- `data.colec.fbf` eliminated from all the examples.
- `rgee` now pass all `goodpractice` checks.
- `ee_get_img_date` and `ee_get_ic_date` are now `ee_get_date_img` and `ee_get_date_ic`.
- A new group of functions was created at `ee_utils.R`. `ee_pyfunc` is now `ee_utils_pyfunc`.
- Added new examples in `README.R`.
