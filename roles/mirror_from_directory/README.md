# Mirror from file role

A role that mirror operators from a local directory into a container images registry using the `oc-mirror` plugin.

## Parameters

Name                   | Required | Default                                       | Description
---------------------- | -------- | --------------------------------------------- | ------------
mfd_local_registry     | Yes      |                                               | Target registry
mfd_operators_dir      | Yes      |                                               | Directory containing the tarball files generated by oc-mirror
mfd_delete_workspace   | No       | True                                          | Deletes the `oc-mirror` workspace generated during the mirroring
mfd_local_registry_path| No       |                                               | Path/Org in the local registry where the images will be mirrored into

## Outputs

The role involves copying a generated Image Sources manifest and CatalogSources files into a temporary directory. These files can be accessed using the following variables:

- `mdf_image_source_file`: The path to the Image Source file produced.
- `mdf_catalog_source_file`: The catalog manifest for the mirrored operators.
- `mdf_manifests_dir`: The directory with the mirroring artifacts

## Example of usage

```yaml
- name: "Mirror operators from directory"
  include_role:
    name: redhatci.ocp.mirror_from_directory
  vars:
    mfd_local_registry: "<registry>:<port>/<optional_path>"
    mfd_local_registry_path: <my-org>
    mfd_operators_dir: "<tarball_dir>"
```

## Authentication

If registry authentication is required, please pass `DOCKER_CONFIG` as an environment variable to the role pointing to the directory that contains the `config.json` file with the proper authentication strings. See [docker-config](https://www.systutorials.com/docs/linux/man/5-docker-config-json/).
