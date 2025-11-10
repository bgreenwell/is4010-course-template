# Week 14: Publishing and Distribution - Lecture Notes

**Course:** IS4010 - AI-Enhanced Application Development
**Topic:** Publishing and Distribution
**Companion Materials:** [Slides](../IS4010_W14_Publishing_and_Distribution.qmd) | [Final Project](https://github.com/bgreenwell/is4010-course-template)

---

## 📋 Learning Objectives

By the end of this session, you should be able to:
- **Apply** semantic versioning principles to your projects
- **Publish** Rust crates to crates.io
- **Create** GitHub releases with version tags
- **Automate** cross-platform builds with GitHub Actions
- **Distribute** applications via multiple package managers
- **Understand** the complete software deployment lifecycle

---

## Part 1: Semantic Versioning

### What is Semantic Versioning?

**Format**: MAJOR.MINOR.PATCH (e.g., 1.2.3)

**When to increment:**
- **MAJOR**: Breaking changes, incompatible API changes
- **MINOR**: New features, backward-compatible additions
- **PATCH**: Bug fixes, backward-compatible fixes

**Pre-1.0.0 versions:**
- `0.1.0` - Initial development
- `0.x.y` - Still stabilizing API
- `1.0.0` - First stable release

### Version Examples

**Starting out**: `0.1.0`
**Bug fix**: `0.1.0` → `0.1.1`
**New feature**: `0.1.1` → `0.2.0`
**Breaking change**: `0.2.0` → `1.0.0` (when ready)

**Pre-release versions:**
- `1.0.0-alpha.1` - Early testing
- `1.0.0-beta.1` - Feature complete
- `1.0.0-rc.1` - Release candidate

### Why It Matters

- Communicates change impact to users
- Cargo uses it for dependency resolution
- Industry standard practice
- Prevents breaking user code

---

## Part 2: Publishing to crates.io

### Preparing Your Crate

**Required Cargo.toml fields:**
```toml
[package]
name = "my-crate"
version = "0.1.0"
edition = "2021"
license = "MIT OR Apache-2.0"  # Required
description = "Short description"  # Required
```

**Recommended fields:**
```toml
authors = ["Your Name <you@example.com>"]
repository = "https://github.com/username/my-crate"
homepage = "https://github.com/username/my-crate"
documentation = "https://docs.rs/my-crate"
readme = "README.md"
keywords = ["cli", "tool", "utility"]  # Max 5
categories = ["command-line-utilities"]
```

### License Selection

**Common Rust licenses:**
- **MIT OR Apache-2.0**: Rust standard, permissive
- **MIT**: Simple, permissive
- **Apache-2.0**: Patent protection
- **GPL-3.0**: Copyleft (be careful with libraries)

**Recommendation**: Use `MIT OR Apache-2.0` for maximum compatibility

### Documentation Requirements

**README.md should include:**
- What the crate does
- Installation instructions
- Usage examples
- License information

**API documentation:**
```rust
/// Function description.
///
/// # Examples
///
/// ```
/// let result = my_function(42);
/// assert_eq!(result, 84);
/// ```
pub fn my_function(x: i32) -> i32 {
    x * 2
}
```

### Publishing Workflow

**Step 1**: Get API token from [crates.io](https://crates.io/)
**Step 2**: Login locally
```bash
cargo login <your-token>
```

**Step 3**: Dry run
```bash
cargo publish --dry-run
```

**Step 4**: Publish
```bash
cargo publish
```

**Step 5**: Verify at crates.io and docs.rs

### Post-Publication

**What happens:**
- Appears on crates.io
- Documentation builds on docs.rs
- Cannot be deleted (only yanked)
- Anyone can `cargo add your-crate`

**Yanking versions:**
```bash
cargo yank --version 0.1.0  # Mark unavailable
cargo yank --version 0.1.0 --undo  # Undo
```

---

## Part 3: Git Tags and GitHub Releases

### Creating Version Tags

**Annotated tags (recommended):**
```bash
git tag -a v0.1.0 -m "Release version 0.1.0"
git push origin v0.1.0
```

**Tag naming:**
- Prefix with 'v': `v0.1.0`
- Match Cargo.toml version
- Use annotated tags

### GitHub Releases

**Creating a release:**
1. Go to repository → Releases
2. Click "Draft a new release"
3. Select or create tag
4. Add release notes
5. Attach compiled binaries
6. Publish release

**Release notes should include:**
- What's new
- What changed
- Bug fixes
- Breaking changes (if any)

---

## Part 4: CI/CD and Automation

### GitHub Actions for Releases

**Basic release workflow:**
```yaml
name: Release

on:
  push:
    tags:
      - 'v*'

jobs:
  build:
    runs-on: ${{ matrix.os }}
    strategy:
      matrix:
        os: [ubuntu-latest, macos-latest, windows-latest]
    steps:
      - uses: actions/checkout@v4
      - run: cargo build --release
```

### Cross-Platform Builds

**Common targets:**
- `x86_64-unknown-linux-gnu` - Linux
- `x86_64-apple-darwin` - macOS Intel
- `aarch64-apple-darwin` - macOS Apple Silicon
- `x86_64-pc-windows-msvc` - Windows

**Building for targets:**
```bash
rustup target add x86_64-unknown-linux-gnu
cargo build --release --target x86_64-unknown-linux-gnu
```

### Automated Pipeline

**On git tag push:**
1. Run tests
2. Build for all platforms
3. Create GitHub release
4. Upload binaries
5. Publish to crates.io
6. Update documentation

---

## Part 5: Package Manager Distribution

### Homebrew (macOS)

**What**: Package manager for macOS/Linux
**Why**: Popular for CLI tools on Mac

**Basic formula:**
```ruby
class Myapp < Formula
  desc "Description"
  homepage "https://github.com/user/myapp"
  url "https://github.com/user/myapp/archive/v0.1.0.tar.gz"
  license "MIT"

  def install
    system "cargo", "install", "--locked", "--root", prefix, "--path", "."
  end
end
```

**Users install:**
```bash
brew tap username/myapp
brew install myapp
```

### cargo-binstall

**What**: Fast binary installation
**Why**: No compilation needed

**Setup**: Create GitHub Releases with properly named binaries
**Users install:**
```bash
cargo binstall your-crate
```

### Nix (Advanced)

**What**: Reproducible package manager
**Why**: Growing popularity, reproducibility

**Basic flake.nix:**
```nix
{
  description = "My app";
  outputs = { self, nixpkgs }: {
    packages.x86_64-linux.default =
      nixpkgs.legacyPackages.x86_64-linux.rustPlatform.buildRustPackage {
        pname = "myapp";
        version = "0.1.0";
        src = ./.;
      };
  };
}
```

---

## Part 6: Distribution Strategy

### Multiple Distribution Methods

**Recommendation**: Use several methods
- **crates.io**: For Rust users
- **GitHub Releases**: For everyone
- **Homebrew**: For macOS users
- **cargo-binstall**: For fast installs

### Comparison

**crates.io:**
- ✅ Easy for Rust users
- ✅ Automatic documentation
- ❌ Rust-only

**GitHub Releases:**
- ✅ Universal
- ✅ Direct downloads
- ❌ Manual process

**Homebrew:**
- ✅ macOS standard
- ✅ Easy updates
- ❌ macOS only

**cargo-binstall:**
- ✅ Fast (no compilation)
- ✅ Automatic
- ❌ Requires GitHub Releases

---

## Part 7: Career Relevance

### Why These Skills Matter

**Publishing:**
- Portfolio demonstration
- Open source contribution
- Shows distribution knowledge

**CI/CD:**
- Industry standard
- DevOps awareness
- Automation skills

**Versioning:**
- Professional practice
- Communication skill
- API management

### Interview Topics

**Common questions:**
- "Tell me about software you've shipped"
- "How do you handle versioning?"
- "What's your deployment process?"
- "Have you contributed to open source?"

### Portfolio Value

**Published crates demonstrate:**
- Complete project lifecycle knowledge
- Professional development practices
- Initiative and follow-through
- Real-world impact

---

## Part 8: Key Takeaways

### Publishing Checklist

- [ ] Use semantic versioning
- [ ] Complete Cargo.toml metadata
- [ ] Choose appropriate license
- [ ] Write comprehensive documentation
- [ ] Test thoroughly
- [ ] Use `cargo publish --dry-run`
- [ ] Publish to crates.io

### Distribution Checklist

- [ ] Create git tags for versions
- [ ] Set up GitHub Releases
- [ ] Provide cross-platform binaries
- [ ] Consider package managers
- [ ] Automate with CI/CD
- [ ] Maintain clear changelogs

### Professional Practices

- Automate everything possible
- Support multiple platforms
- Document clearly
- Follow semantic versioning
- Build complete pipelines
- Maintain releases actively

---

## Part 9: Application to Final Projects

### Making Your Project Portfolio-Worthy

**Minimum requirements:**
1. Complete Cargo.toml with metadata
2. Comprehensive README
3. LICENSE file
4. Version tags in git
5. GitHub releases

**Professional touches:**
1. Automated CI/CD
2. Cross-platform builds
3. Published to crates.io
4. Package manager support
5. Complete documentation

### Final Project Checklist

**Code quality:**
- [ ] All tests passing
- [ ] No clippy warnings
- [ ] Properly formatted
- [ ] Well documented

**Distribution:**
- [ ] Cargo.toml complete
- [ ] README comprehensive
- [ ] LICENSE chosen
- [ ] Git tags created
- [ ] GitHub release made

**Optional but impressive:**
- [ ] Published to crates.io
- [ ] CI/CD pipeline
- [ ] Cross-platform binaries
- [ ] Homebrew formula

---

## Additional Resources

**Official documentation:**
- [The Cargo Book - Publishing](https://doc.rust-lang.org/cargo/reference/publishing.html)
- [Semantic Versioning](https://semver.org/)
- [Git Tagging](https://git-scm.com/book/en/v2/Git-Basics-Tagging)

**CI/CD:**
- [GitHub Actions for Rust](https://github.com/actions-rs)
- [Cross-compilation Guide](https://rust-lang.github.io/rustup/cross-compilation.html)

**Distribution:**
- [Homebrew Formula Cookbook](https://docs.brew.sh/Formula-Cookbook)
- [cargo-binstall](https://github.com/cargo-bins/cargo-binstall)

**Examples to study:**
- [ripgrep](https://github.com/BurntSushi/ripgrep)
- [bat](https://github.com/sharkdp/bat)
- [fd](https://github.com/sharkdp/fd)

---

## Course Completion

**Congratulations!** You've learned:
- Python programming and OOP
- Rust programming and ownership
- Testing and quality practices
- Version control with Git/GitHub
- CI/CD automation
- Software distribution

**You now understand the complete software development lifecycle from code to production!**

**Apply these skills to your final project and future career.**
