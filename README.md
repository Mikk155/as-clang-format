# AngelScript Formatting Enhancement (as-clang-format)

This repository provides a customized version of `clang-format`, specifically optimized for **AngelScript (AS)**. It addresses the long-standing issue where handle symbols (`@`) are incorrectly spaced or attached, ensuring a professional and readable code style for game scripting.

## 🌟 Key Enhancements

* **Smart Handle Spacing**: Correctly formats handle declarations. Based on `PointerAlignment: Left`, it turns `xck::PersonInfo @p` into `xck::PersonInfo@ p`.
* **Generic/Template Support**: Fixes the trailing space issue inside templates. It ensures `cast<xck::PersonInfo@>` instead of `cast<xck::PersonInfo@ >`.
* **Scope/Namespace Awareness**: Accurately recognizes complex types across namespaces, such as `xck::UnitInfo@` or `abc::BuildingInfo@`.
* **Handle Anti-merging**: Prevents consecutive handle symbols from being merged, maintaining `@ @` for clear lexical parsing.

## 🔧 Technical Implementation

The modifications are integrated into the Clang Tooling layer, specifically within `clang/lib/Format/TokenAnnotator.cpp`. We have:
1.  Modified the `spaceRequiredBetween` function to recognize `@` as a pointer-like token (`TT_PointerOrReference`).
2.  Bypassed the default Objective-C rules that previously interfered with AngelScript's handle syntax.
3.  Synchronized handle positioning with the standard `PointerAlignment` configuration.

## 📦 Usage

1.  **Obtain Binary**: Download `as-clang-format.exe` from the GitHub Releases of this repository with the tag ``asclang``.
2.  **Configuration**: Place a `.clang-format` file in your project root.
3.  **Recommended Style Settings**:
    ```yaml
    Language: Cpp
    BasedOnStyle: LLVM
    PointerAlignment: Left  # Results in: Type@ var
    ```

## Building
Go to [build-as-clang.yml](https://github.com/Mikk155/as-clang-format/actions/workflows/build-as-clang.yml) and press "Run Workflow" then a release with the tag ``asclang`` will be updated
> Currently this only builds windows
