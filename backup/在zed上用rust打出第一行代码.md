首先`Zed`编辑器、`Rust`本体，我推荐使用`scoop`安装
##### 使用zed，它会送你一个删了又被下回来了的node.js运行时，可以添加到Windows环境变量，物尽其用
#### 最常用的命令 (Cargo)
`cargo run `命令：编译代码 -> 生成二进制文件 -> 立即运行程序
`cargo run` --quiet (或 -q) 只显示程序的输出结果，隐藏 Cargo 的编译进度信息。
`cargo run` --release 以 Release 模式运行。它会进行大量代码优化，运行速度极快，但编译时间稍长。通常用于性能测试。
#### 跑单个 .rs 文件 (rustc)
编译： rustc hello.rs (这会生成一个名为 hello 的可执行文件)
运行： `./hello.exe` (Windows 下是 hello.exe)
```
fn main() {
    println!("Hello, World!");
}
```
“一键编译并运行”：
```
rustc main.rs && ./main
```
#### 标准开发方式（Cargo 项目）
新建项目： 在终端输入 `cargo new my_project`
进入目录： `cd my_project`
写入代码：写在 src/main.rs 里
运行： 此时输入 `cargo run`（注意：不需要加文件名），它就会找到同目录下的 Cargo.toml 并成功运行
**既然已经配置好了 Cargo 环境，那我们来玩点测试。**
修改 `src/main.rs`
为此建立一个“二进制入口”（最简单，适合跑不同的测试）
```
mkdir src/bin
```
```
touch src/bin/test2.rs
```
打开 src/bin/test2.rs
```
use colored::*;
use std::thread;
use std::time::Duration;

fn main() {
    let components = vec![
        ("CPU", "Intel Core i9-14900K / NixOS Optimized", "16 Cores"),
        ("GPU", "NVIDIA RTX 4090 (Nix-Drivers)", "24GB VRAM"),
        ("RAM", "64GB DDR5 6400MHz", "Active"),
        ("OS", "NixOS (WSL2 Kernel)", "Rolling Release"),
    ];

    println!("{}", "\n>>> 正在初始化硬件扫描序列...".on_black().bold());
    thread::sleep(Duration::from_secs(1));

    for (name, model, status) in components {
        print!("扫描 {}... ", name.bright_blue());
        thread::sleep(Duration::from_millis(600)); // 模拟扫描延迟
        println!("{} [{}]", model.bright_white(), status.bright_green());
    }

    println!("\n{}", "====================================".bright_yellow());
    println!("{}", "  所有硬件已通过 Nix 兼容性测试！".on_green().black());
    println!("{}", "====================================\n".bright_yellow());
}
```
运行这个新练习 (test2.rs)
```
cargo run --bin test2
```
新建的`my_project`项目会自带一个`mian.rs`，可写入
```
fn main() {
    println!("Hello, Rust!");
}
```
运行原来的第一个练习 (main.rs)
```
cargo run
```
##### 在项目根目录运行`cargo`命令即可（也就是包含 Cargo.toml 的那个 hello_rust 文件夹）
*在项目文件夹(\my_project)，上一层文件夹(D:\Zed\Rust)里还有最早 跑单个 .rs 文件命令留下`main.rs` `main.exe`单文件，可删。*