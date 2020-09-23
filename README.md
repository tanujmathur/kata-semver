# kata-semver

Implement logic to parse and compare semver values

## PART 1: Parsing & Validation Rules

* A normal version number MUST take the form X.Y.Z where X, Y, and Z are non-negative integers, and MUST NOT contain leading zeroes. X is the major version, Y is the minor version, and Z is the patch version. Each element MUST increase numerically. For instance: 1.9.0 -> 1.10.0 -> 1.11.0.

* A pre-release version MAY be denoted by appending a hyphen and a series of dot separated identifiers immediately following the patch version.
  * Identifiers MUST comprise only ASCII alphanumerics and hyphens [0-9A-Za-z-].
  * Identifiers MUST NOT be empty.
  * Numeric identifiers MUST NOT include leading zeroes.
  * Examples: 1.0.0-alpha, 1.0.0-alpha.1, 1.0.0-0.3.7, 1.0.0-x.7.z.92, 1.0.0-x-y-z.–.

* Build metadata MAY be denoted by appending a plus sign and a series of dot separated identifiers immediately following the patch or pre-release version.
  * Identifiers MUST comprise only ASCII alphanumerics and hyphens [0-9A-Za-z-].
  * Identifiers MUST NOT be empty.  
  * Examples: 1.0.0-alpha+001, 1.0.0+20130313144700, 1.0.0-beta+exp.sha.5114f85, 1.0.0+21AF26D3—-117B344092BD.

## PART 2: Precedence Rules

Precedence refers to how versions are compared to each other when ordered.

* Precedence MUST be calculated by separating the version into major, minor, patch and pre-release identifiers in that order (Build metadata does not figure into precedence).

  * Precedence is determined by the first difference when comparing each of these identifiers from left to right as follows: Major, minor, and patch versions are always compared numerically.

  * Example: 1.0.0 < 2.0.0 < 2.1.0 < 2.1.1.

* When major, minor, and patch are equal, a pre-release version has lower precedence than a normal version:
  * Example: 1.0.0-alpha < 1.0.0.

* Precedence for two pre-release versions with the same major, minor, and patch version MUST be determined by comparing each dot separated identifier from left to right until a difference is found as follows:

  * Identifiers consisting of only digits are compared numerically.

  * Identifiers with letters or hyphens are compared lexically in ASCII sort order.

  * Numeric identifiers always have lower precedence than non-numeric identifiers.

  * A larger set of pre-release fields has a higher precedence than a smaller set, if all of the preceding identifiers are equal.

  * Example: 1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-alpha.beta < 1.0.0-beta < 1.0.0-beta.2 < 1.0.0-beta.11 < 1.0.0-rc.1 < 1.0.0.

* Build metadata MUST be ignored when determining version precedence. Thus two versions that differ only in the build metadata, have the same precedence.

## Kata Rules

* Ping Pong Pairing
* TDD, Red -> Green -> Refactor
* Baby Steps (no logic unless required by a failing test)
* Code should express intent
* Frequent commits (once every 15 minutes)