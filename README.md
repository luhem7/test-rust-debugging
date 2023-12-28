# test-rust-debugging
My notes on setting up rust debugging with VSCode.

# MacOS
## Simple rust binary project
1. Install the rust-analyzer extension. Then install the CodeLLDB extension by Vadim.
2. *IMPORTANT* Delete the `~/.vscode/extensions/vadimcn.vscode-lldb-1.10.0/lldb/bin/debugserver` file as per [this github issue](https://github.com/rust-lang/rust-analyzer/issues/15699).
3. Create a new rust project.
4. Click on the Run and Debug section and generate a new launch.json file. At this point I got a prompt asking me if I wanted to generate a new pre-configured launch.config file based on the Cargo.lock file that is created.
5. If you select yes, it creates a launch.json file similar to `launch_macos_bin.json`
6. I also had to change the VSCode user setting to allow breakpoints anywhere.