# rust-builder

A builder image for building static rust binaries for amd64 and arm64 platforms.

# Create a new version

    git tag <rust-version>-nightly-<suffix>
    git push origin <rust-version>-nightly-<suffix>

This will trigger the github action and create and tag a new image.



# Usage

~~~~
FROM ghcr.io/ecociel/rust-builder:<tag> as builder

TBD
