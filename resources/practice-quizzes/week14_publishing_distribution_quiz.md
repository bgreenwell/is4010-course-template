# Week 14 Practice Quiz: Publishing and Distribution

**Course:** IS4010 - AI-Enhanced Application Development
**Topic:** Publishing to crates.io and Software Distribution
**Time:** ~15 minutes
**Questions:** 10 multiple choice

---

## Instructions

Select the best answer for each question. Answers are provided at the end of the quiz.

---

## Questions

### 1. According to semantic versioning principles, which version change should you make when fixing a bug that doesn't affect the API?

a) Increment the MAJOR version (e.g., 1.2.3 → 2.0.0)
b) Increment the MINOR version (e.g., 1.2.3 → 1.3.0)
c) Increment the PATCH version (e.g., 1.2.3 → 1.2.4)
d) Keep the version the same but add a pre-release suffix

---

### 2. What is the recommended license for Rust crates to maximize compatibility with the Rust ecosystem?

a) GPL-3.0
b) MIT OR Apache-2.0
c) BSD-3-Clause
d) Proprietary license

---

### 3. You want to test what will be published to crates.io without actually publishing. Which command should you use?

a) `cargo test --publish`
b) `cargo build --release`
c) `cargo publish --dry-run`
d) `cargo check --publish`

---

### 4. What happens when you "yank" a version of your crate on crates.io?

a) The version is permanently deleted and cannot be used by anyone
b) The version is marked as unavailable for new projects, but existing Cargo.lock files still work
c) The version is moved to a private archive accessible only to the author
d) The entire crate is removed from crates.io

---

### 5. Which Git command creates an annotated tag for version 0.1.0 with a message?

a) `git commit -m "v0.1.0" --tag`
b) `git tag v0.1.0`
c) `git tag -a v0.1.0 -m "Release version 0.1.0"`
d) `git release v0.1.0 -m "Release version 0.1.0"`

---

### 6. You're creating a GitHub Actions workflow that should run only when version tags are pushed. Which trigger should you use?

a) `on: push: branches: [main]`
b) `on: push: tags: ['v*']`
c) `on: release: types: [published]`
d) `on: workflow_dispatch`

---

### 7. Which target platform identifier is used for building Rust applications for macOS with Apple Silicon (M1/M2 chips)?

a) `x86_64-apple-darwin`
b) `aarch64-apple-darwin`
c) `arm64-apple-silicon`
d) `x86_64-unknown-darwin-arm`

---

### 8. What is the primary benefit of using cargo-binstall for users installing your application?

a) It provides automatic security scanning of binaries
b) It downloads pre-built binaries instead of compiling from source, saving time
c) It allows installation without needing Cargo installed
d) It automatically updates the application daily

---

### 9. According to the course materials, which of these is NOT a required field in Cargo.toml for publishing to crates.io?

a) `name`
b) `version`
c) `license`
d) `homepage`

---

### 10. In a professional CI/CD pipeline for Rust applications, what is the recommended order of operations when a version tag is pushed?

a) Publish → Test → Build → Release
b) Build → Publish → Test → Release
c) Test → Build → Publish → Release
d) Release → Build → Test → Publish

---

## Answer Key

<details>
<summary>Click to reveal answers</summary>

### Answers and Explanations

**1. c) Increment the PATCH version (e.g., 1.2.3 → 1.2.4)**
*Explanation:* PATCH version increments are for backward-compatible bug fixes. MAJOR is for breaking changes, MINOR is for new features.

**2. b) MIT OR Apache-2.0**
*Explanation:* This dual license is the Rust community standard, providing permissive terms and patent protection while maximizing compatibility.

**3. c) `cargo publish --dry-run`**
*Explanation:* The `--dry-run` flag shows what would be published without actually uploading to crates.io, allowing you to verify the package contents.

**4. b) The version is marked as unavailable for new projects, but existing Cargo.lock files still work**
*Explanation:* Yanking prevents new projects from using a version but doesn't break existing code that already depends on it. You cannot delete published versions.

**5. c) `git tag -a v0.1.0 -m "Release version 0.1.0"`**
*Explanation:* The `-a` flag creates an annotated tag (recommended), and `-m` provides the message. Annotated tags include metadata like author and date.

**6. b) `on: push: tags: ['v*']`**
*Explanation:* This trigger activates the workflow when any tag starting with 'v' is pushed, which is the conventional format for version tags.

**7. b) `aarch64-apple-darwin`**
*Explanation:* `aarch64` refers to the ARM 64-bit architecture used in Apple Silicon chips. `x86_64-apple-darwin` is for Intel-based Macs.

**8. b) It downloads pre-built binaries instead of compiling from source, saving time**
*Explanation:* cargo-binstall fetches pre-compiled binaries from GitHub Releases, avoiding the time-consuming compilation process. It falls back to `cargo install` if binaries aren't available.

**9. d) `homepage`**
*Explanation:* While `homepage` is recommended for discoverability, only `name`, `version`, `license`, and `description` are strictly required to publish to crates.io.

**10. c) Test → Build → Publish → Release**
*Explanation:* The professional workflow runs tests first to ensure quality, then builds for all platforms, publishes to crates.io, and finally creates the GitHub release with binaries.

</details>

---

## Study Resources

- [Slides: IS4010_W14_Publishing_and_Distribution.qmd](../../../is4010-instructor-materials/slides/IS4010_W14_Publishing_and_Distribution.qmd)
- [Lecture Notes: W14_Publishing_and_Distribution_notes.md](../lecture-notes/W14_Publishing_and_Distribution_notes.md)
- [The Cargo Book - Publishing](https://doc.rust-lang.org/cargo/reference/publishing.html)
- [Semantic Versioning](https://semver.org/)
- [GitHub Actions for Rust](https://github.com/actions-rs)

---

**Good luck with your final project! 🦀**
