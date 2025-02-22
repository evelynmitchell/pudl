===============================================================================
Run a Versioned Release
===============================================================================

So the time has come and we would like to release a ``stable`` version of our
data/code out into the world. By the end of this, we'd like for:

* the release notes to have a fully dated release
* the git tag ``vYYYY.MM.DD`` to identify a specific version
* the ``stable`` Git branch to refer to the same commit as that tag
* Our data outputs corresponding to that tag on Zenodo,
  ``pudl.catalyst.coop/stable`` buckets in GCS/AWS, and Kaggle
* Our code corresponding to that tag on PyPI
* The conda package to be updated with the newest code
* Updated ``stable`` and ``vYYYY.MM.DD`` documentation on ReadTheDocs


Here's how to do it!

1. Tell the rest of the team you're planning on releasing a new version of the
   code in #team. Remind them that any changes to the release notes *after* the
   next nightly build has passed need to go into a new version.

2. The night before you plan to release, update the release notes with a
   paragraph or two explaining what this new release is, and attach a specific
   date to the release.

3. Wait for the nightly build to pass with your release notes updates.

4. If the nightly build passes, push a git tag ``vYYYY.MM.DD`` that points at
   the commit which just passed the nightly build. This will kick off another build.

5. If *that* build passes, verify the following:

   * GCS/AWS distribution buckets have the appropriate data
   * ``stable`` and ``vYYYY.MM.DD`` point at the same Git ref
   * ReadTheDocs for ``stable`` and ``vYYYY.MM.DD`` versions have the latest
     changes in the release notes
   * PyPI has the most current version of our code

6. Verify that the Zenodo draft deposition has all the expected data (raw FERC
   databases, PUDL database, everything the right size).

7. Update the Zenodo metadata to include the description from the release
   notes, and update the various links.

8. Publish the Zenodo deposition! Wahoo! You're now done!

9. Except... within 24 hours after the PyPI version is updated, we'll get [a PR
   in the PUDL conda-forge feedstock
   repo](https://github.com/conda-forge/catalystcoop.pudl-feedstock/pulls) from
   the :user:`regro-cf-autotick-bot` updating our ``conda`` packaging. If
   PUDL's direct dependencies have changed in this release, we need to update
   them in the conda packaging recipe in that PR.
