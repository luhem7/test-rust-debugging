# test-rust-debugging
My notes on setting up rust debugging with VSCode.

# MacOS with Intel processor
## Common Steps for all
1. Install the rust-analyzer extension. Then install the CodeLLDB extension by Vadim.
2. *IMPORTANT* Delete the `~/.vscode/extensions/vadimcn.vscode-lldb-1.10.0/lldb/bin/debugserver` file as per [this github issue](https://github.com/rust-lang/rust-analyzer/issues/15699).
3. Change the VSCode user setting to allow setting breakpoints anywhere.
4. Create the rust project using cargo.
5. Follow the steps below for each kind of cargo project.

### Workspace with a single binary package
1. Click on the Run and Debug section and generate a new `launch.json` file. At this point I got a prompt asking me if I wanted to generate a new pre-configured launch.config file based on the Cargo.lock file that is created.
2. If you select yes, it creates a `launch.json` file similar to `launch_macos_bin.json`
3. Set a breakpoint and run the Debug Executable launch configuration. It should start a debugging session with the execution halted at the breakpoint. You should be able to issue debug command to CodeLLDB using the _Debug Console_ View in the bottom pane of VSCode.

### Workspace with multiple packages
These steps are for setting up the `launch.json` config to debug a specific binary package in a workspace that has multiple packages. You can copy these steps to create new launch configs for different binary packages in the same workspace.
1. Click on the Run and Debug section and generate a new `launch.json` file. However you will need to edit this file to both:

    a. Point the configuration to both the _specific_ Cargo.toml file for building your binary package.

    b. Tell CodeLLDB what the name of the executable is that it needs to debug.

    You can use the `launch_macos_multi.json` file as a template. (Cargo should build all packages in the workspace if you don't specify the `manifest-path` option, but CodeLLDB seems to really want it)

2. Set a breakpoint and run the Debug Executable launch configuration. It should start a debugging session with the execution halted at the breakpoint. You should be able to issue debug command to CodeLLDB using the _Debug Console_ View in the bottom pane of VSCode.

### Additional Notes
- The [User Manual for CodeLLDB](https://github.com/vadimcn/codelldb/blob/master/MANUAL.md) has a lot of great information on setting up VSCode to use this extension. In particular, there is a section for [Rust Language Support](https://github.com/vadimcn/codelldb/blob/master/MANUAL.md#rust-language-support) which was helpful to setup debugging.
- The `cwd` option doesn't seem to work? All the above steps are written assuming that we have to run them from the root of the project repo.