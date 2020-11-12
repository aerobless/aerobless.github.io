
## Dependencies: api vs implementation

Gradle has deprecated the `compile` keyword in favor of `api` and `implementation`. So which should be used when?

+ api: equivalent to compile, shares inner libraries,
    + e.g. app -dependsOn-> someLib -api-> innerLib
    + app now has access to innerLib methods
+ implementation: 
    + e.g. app -dependsOn-> someLib -implementation-> innerLib
    + app does not have access to innerLib methods

**Gotchas:**
+ api/implementation are not enforced at runtime, they're only relevant during the build

**Usage strategies:**
+ in a library: use api when the dependencies is necessary for the consumer of the public api of the lib
+ in an app: use implementation