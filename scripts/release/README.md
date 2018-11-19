Notes for release managers
---

This document describes how to make an Mango release.

First, make sure you have:
- Updated the pom.xml for the new version
- Updated the distributions in bin/emr and bin/gce to reflect the new versions.

Setup your environment
1. Copy (or incorporate) the settings.xml file to ```~/.m2/settings.xml```
2. Request the Mango packager private GPG key
3. Edit the username, password, etc in ```~/.m2/settings.xml```

Once your environment is setup, you'll be able to do a release.

Then from the project root directory, run `./scripts/release/release.sh`.
If you have any problems, run `./scripts/release/rollback.sh`.

Once you've successfully published the release, you will need to "close" and "release" it following the instructions at
http://central.sonatype.org/pages/releasing-the-deployment.html#close-and-drop-or-release-your-staging-repository

After the release is rsynced to the Maven Central repository, confirm checksums match and verify signatures.

Be sure to announce the release on the ADAM mailing list and Twitter (@bigdatagenomics).

Additionally, once the release is done, you will need to bump the mango-python and mango-viz development versions on trunk.

Debugging gpg:

To test if you have set up keys correctly, run mvn gpg:sign.

If this fails with error gpg: signing failed: Inappropriate ioctl for device, you can try:
export GPG_TTY=$(tty)
