# Workflow References

This document contains references to external workflow runs that are relevant to this repository.

## External Workflow Runs

### XPipe Webtop - Docker Push Workflow Failure

**Repository:** xpipe-io/xpipe-webtop  
**Workflow Run:** https://github.com/xpipe-io/xpipe-webtop/actions/runs/20578223451/job/59099982309  
**Date:** 2025-12-29  
**Status:** Failed  

**Description:**
This workflow run failed during the Docker build process when attempting to install the AWS Session Manager Plugin. The failure occurred at line 131-133 of the Dockerfile when executing:

```dockerfile
RUN echo "**** aws ssm ****" && curl "https://s3.amazonaws.com/session-manager-downloads/plugin/latest/ubuntu_64bit/session-manager-plugin.deb" -o "/tmp/session-manager-plugin.deb" && \
  sudo dpkg -i "/tmp/session-manager-plugin.deb" && \
  rm -rf "/tmp/aws" "/tmp/session-manager-plugin.deb"
```

**Error Message:**
```
ERROR: failed to build: failed to solve: process "/bin/sh -c echo \"**** aws ssm ****\" && curl \"https://s3.amazonaws.com/session-manager-downloads/plugin/latest/ubuntu_64bit/session-manager-plugin.deb\" -o \"/tmp/session-manager-plugin.deb\" &&   sudo dpkg -i \"/tmp/session-manager-plugin.deb\" &&   rm -rf \"/tmp/aws\" \"/tmp/session-manager-plugin.deb\"" did not complete successfully: exit code: 1
```

**Relevance:**
This reference documents a common Docker build failure pattern when installing AWS Session Manager Plugin. This can be useful for understanding similar issues in CI/CD pipelines and containerized environments.

**Potential Solutions:**
1. Verify the download URL is still valid
2. Check network connectivity to S3 during build
3. Ensure the base image has necessary dependencies (e.g., `sudo`, `curl`, `dpkg`)
4. Consider using a different installation method or version of the plugin
5. Add error handling and retry logic for network-dependent installation steps
