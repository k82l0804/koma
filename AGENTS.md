**Build**
- Always run code generation first: `./gradlew codegen` (regenerates all `Default*` generated source files under `koma-core-api/common/src/koma/internal/default/generated`).
- JVM artifacts: `./gradlew buildJvm` → jars appear in `./build/jvm`.
- JavaScript artifacts: `./gradlew buildJs` → CommonJS modules are placed in `./node_modules/`.
- Native build is not a dedicated Gradle task; use the legacy commands from the README:
  - `./gradlew compileKonanKomaExample -Ptarget=native`
  - `./gradlew compileKonanLibkoma -Ptarget=native -Pkonan.home=/path/to/kotlin-native/dist`
  - `./gradlew compileKonanKoma -Ptarget=native`

**Test**
- Run the full test suite: `./gradlew clean test`.
- Run a single test (or test method): `./gradlew :koma-tests:test --tests "<fully-qualified-test-name>"`.

**Project structure**
- Multi‑module Gradle project (see `settings.gradle`):
  - `koma-core-api`
  - `koma-core-ejml`, `koma-core-jblas`, `koma-core-mtj` (JVM back‑ends)
  - `koma-core-js` (JS back‑end, directory `koma-core/js-default`)
  - `koma-logging`, `koma-plotting`
  - `koma-tests`
- Source roots follow the Kotlin Multiplatform layout (`common/src`, `jvm/src`, `js/src`).

**Generated code**
- Many files under `koma-core-api/common/src/koma/internal/default/generated/*` contain the comment `AND RUN ./gradlew :codegen INSTEAD!` – edit the templates in `templates/` and re‑run `codegen` rather than editing generated files directly.

**IDE setup**
- Import the project by opening `settings.gradle` in IntelliJ IDEA (JVM/JS) or CLion (Native).

**Runtime prerequisites**
- JDK 8 must be on `PATH`.
- For native builds, a built Kotlin/Native distribution is required (`-Pkonan.home` points to its `dist` directory).

**Example execution**
- Run the JavaScript example: `node examples/js/example.js`.
- Run the native example after a native build: `./build/native/<your_platform>/komaExample.kexe`.
