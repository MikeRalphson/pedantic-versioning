# pedantic-versioning 1.0.0.0.0

## A bigly, some would say yuge improvement on semantic versioning

### Summary

Given a version number YUGE.BIGLY.MAJOR.MINOR.PATCH, increment the:

* YUGE version when you make changes no-one has ever seen,
* BIGLY version when you make incredible, incredible changes,
* MAJOR version when you make incompatible API changes,
* MINOR version when you add functionality in a backwards-compatible manner, and
* PATCH version when you make backwards-compatible bug fixes.

Additional labels for pre-release and build metadata are available as extensions to the YUGE.BIGLY.MAJOR.MINOR.PATCH format.

### Introduction

In the **failing** world of software management there exists a dreaded place called “dependency hell.” The bigger your system grows and the more packages you integrate into your software, the more likely you are to find yourself, one day, in this pit of despair.

In systems with many dependencies, releasing new package versions can quickly become a nightmare. If the dependency specifications are too tight, you are in danger of version lock (the inability to upgrade a package without having to release new versions of every dependent package). If dependencies are specified too loosely, you will inevitably be bitten by version promiscuity (assuming compatibility with more future versions than is reasonable). Dependency hell is where you are when version lock and/or version promiscuity prevent you from easily and safely moving your project forward. **Very sad!**

As a solution to this problem, I propose a simple set of rules and requirements that dictate how version numbers are assigned and incremented. These rules are based on but not necessarily limited to pre-existing widespread common practices in use in both closed and open-source software. For this system to work, you first need to declare a public API. This may consist of documentation or be enforced by the code itself. Regardless, it is important that this API be clear and precise. Once you identify your public API, you communicate changes to it with specific increments to your version number. Consider a version format of V.W.X.Y.Z (Yuge.Bigly.Major.Minor.Patch). Bug fixes not affecting the API increment the patch version, backwards compatible API additions/changes increment the minor version, and backwards incompatible API changes increment the major version. Bigly and Yuge changes are self-explanatory.

I call this system “Pedantic Versioning.” Under this scheme, version numbers and the way they change convey meaning about the underlying code and what has been modified from one version to the next.

### Pedantic Versioning Specification (PedVer)

The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in RFC 2119.

Software using Pedantic Versioning MUST declare a public API. This API could be declared in the code itself or exist strictly in documentation. However it is done, it should be precise and comprehensive.

A normal version number MUST take the form V.W.X.Y.Z where V, W, X, Y, and Z are non-negative integers, and MUST NOT contain leading zeroes. V is the yuge version, W is the bigly version, X is the major version, Y is the minor version, and Z is the patch version. Each element MUST increase numerically. For instance: 1.9.0.0.0 -> 1.10.0.0.0 -> 1.11.0.0.0.

Once a versioned package has been released, the contents of that version MUST NOT be modified. Any modifications MUST be released as a new version. Do not release FAKE NPMS!

Yuge version zero (0.w.x.y.z) is for initial development. Anything may change at any time. The public API should not be considered stable.

Version 1.0.0.0.0 defines the public API. The way in which the version number is incremented after this release is dependent on this public API and how it changes.

Patch version Z (v.w.x.y.Z | v > 0) MUST be incremented if only backwards compatible bug fixes are introduced. A bug fix is defined as an internal change that fixes incorrect behavior.

Minor version Y (v.w.x.Y.z | v > 0) MUST be incremented if new, backwards compatible functionality is introduced to the public API. It MUST be incremented if any public API functionality is marked as deprecated. It MAY be incremented if substantial new functionality or improvements are introduced within the private code. It MAY include patch level changes. Patch version MUST be reset to 0 when minor version is incremented.

Major version X (v.w.X.y.z | v > 0) MUST be incremented if any backwards incompatible changes are introduced to the public API. It MAY include minor and patch level changes. Patch and minor version MUST be reset to 0 when major version is incremented.

Bigly version W (v.W.x.y.z | v > 0) MUST be incremented if incredible, incredible changes are introduced.

Yuge version V (V.w.x.y.z | v > 0) MUST be incremented when changes no-one has ever seen are introduced.

A pre-release version MAY be denoted by appending a hyphen and a series of dot separated identifiers immediately following the patch version. Identifiers MUST comprise only ASCII alphanumerics and hyphen [0-9A-Za-z-]. Identifiers MUST NOT be empty. Numeric identifiers MUST NOT include leading zeroes. Pre-release versions have a lower precedence than the associated normal version. A pre-release version indicates that the version is unstable and might not satisfy the intended compatibility requirements as denoted by its associated normal version. Examples: 1.0.0.0.0-alpha, 1.0.0.0.0-alpha.1, 1.0.0.0.0-0.3.7, 1.0.0.0.0-x.7.z.92.

Build metadata MAY be denoted by appending a plus sign and a series of dot separated identifiers immediately following the patch or pre-release version. Identifiers MUST comprise only ASCII alphanumerics and hyphen [0-9A-Za-z-]. Identifiers MUST NOT be empty. Build metadata SHOULD be ignored when determining version precedence. Thus two versions that differ only in the build metadata, have the same precedence. Examples: 1.0.0.0.0-alpha+001, 1.0.0.0.0+20130313144700, 1.0.0.0.0-beta+exp.sha.5114f85.

Precedence refers to how versions are compared to each other when ordered. Precedence MUST be calculated by separating the version into yuge, bigly, major, minor, patch and pre-release identifiers in that order (Build metadata does not figure into precedence). Precedence is determined by the first difference when comparing each of these identifiers from left to right as follows: Yuge, Bigly, Major, minor, and patch versions are always compared numerically. Example: 1.0.0.0.0 < 2.0.0.0.0 < 2.1.0.0.0 < 2.1.1.0.0 When yuge, bigly, major, minor, and patch are equal, a pre-release version has lower precedence than a normal version. Example: 1.0.0.0.0-alpha < 1.0.0.0.0. Precedence for two pre-release versions with the same yuge, bigly, major, minor, and patch version MUST be determined by comparing each dot separated identifier from left to right until a difference is found as follows: identifiers consisting of only digits are compared numerically and identifiers with letters or hyphens are compared lexically in ASCII sort order. Numeric identifiers always have lower precedence than non-numeric identifiers. A larger set of pre-release fields has a higher precedence than a smaller set, if all of the preceding identifiers are equal. Example: 1.0.0.0.0-alpha < 1.0.0.0.0-alpha.1 < 1.0.0.0.0-alpha.beta < 1.0.0.0.0-beta < 1.0.0.0.0-beta.2 < 1.0.0.0.0-beta.11 < 1.0.0.0.0-rc.1 < 1.0.0.
