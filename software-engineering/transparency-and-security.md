# Transparency and security

## Source Code Modifications
The whole source code of the OSP Suite is stored and versioned on GitHub.

As of January 2023, GitHub reports having over 100 million users and more than 420 million repositories (including at least 28 million public repositories), making it the largest host of source code in the world.

Among others, GitHub is used by companies like Google or Microsoft for the code hosting, for example [Google](https://github.com/google) and [Microsoft](https://github.com/microsoft)

Source code on the OSP can be modified by the OSP Maintainers only. OSP Maintainers consist of a very limited number of people (and is a subset of OSP Management Team (MT), OSP Sounding Board (SB) and OSP Core Developers (DEV)).

When source code modifications must be done, the procedure is as follows:

* Any user can propose changes for the software by creating a so called [Pull Request (PR)](https://en.wikipedia.org/wiki/Distributed_version_control#Pull_requests)

* Those changes are not automatically accepted into the software

* Instead members of the SB and DEV team review this proposal and decide if proposed changes could be integrated

* In case of positive decision: revalidation of the software with integrated proposed changes is performed

* If the outcome of the revalidation is positive: proposed changes are accepted as part of the official release

This is a well-established procedure used particularly by GitHub for open source and closed source (commercial) software, used by millions of customers.

## Build Process
Building of the OSP Libraries and Setups is realized in a fully automated manner via GitHub Actions CI service [(s. section Software Engineering/Continuous Integration)](./software-engineering.md#continuous-integration).

When building a library or a setup: the corresponding source code from the OSP is transferred into such a build environment and a build process is triggered; resulting build artifacts (libraries/setups) are stored in the GitHub cloud.

This process is fully automated. Particularly:
* Nobody (except core developers (DEV)) can change a standard build environment.
* Nobody can modify source code during build
* Nobody can modify produced build artifacts.

## Transparency

### Source Code

* All source code is public.

* All code changes are tracked and saved in the history, including:

  * Full list of changes
  * Date and time stamp
  * Names of the contributors
  * Names of the Reviewers
  * Name of the person who has integrated the changes (accepted the corresponding PR)
  * Links to associated validation reports
  
Example: https://github.com/Open-Systems-Pharmacology/Suite/commits/master

* Code changes history entries cannot be modified

### Software Builds

* All software builds are tracked and saved in the build history, including:
  * Link to the used version of the source code on GitHub
  * Date and time stamp
  * Full build log
  * Test protocols of all automated tests
  * All produced build artifacts
  
Example: https://github.com/Open-Systems-Pharmacology/Suite/actions

* Build history entries cannot be modified

### Software validation and qualification
An overview of validation steps and links to validation/test reports are published with every OSP Suite release on GitHub (https://github.com/Open-Systems-Pharmacology/Suite/tree/master/validation%20and%20qualification) E.g., the test reports of the OSP Suite version 8 contain more than 10,000 tests.

Qualification reports of the OSP platform are published on GitHub. Examples:

* https://github.com/Open-Systems-Pharmacology/Pediatric_Qualification_Package_GFR_Ontogeny/releases
* https://github.com/Open-Systems-Pharmacology/Pediatric_Qualification_Package_CYP3A4_Ontogeny/releases
* https://github.com/Open-Systems-Pharmacology/Pediatric_Qualification_Package_CYP2C8_Ontogeny/releases