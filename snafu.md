### snafu

snafu 是一个 为错误开始定制错误信息的库。多用于自定义错误类型

#### 例子：

Cargo.toml

```toml
[dependencies]
snafu = { version = "0.4.3", features = ["futures-01"] }
```

Main.rs

```rust
use snafu::Snafu;
use std::fs::File;

#[derive(Debug, Snafu)]
pub enum MyError {
    #[snafu(display("ErrorA occurs. code: {},message:{}", code,message))]
    ErrorA { message: &'static str, code: i32 },
    #[snafu(display("unknown error occurs. code:500"))]
    ErrorB {
        error: std::io::Error,
    },
}

fn method() -> Result<(),MyError> {
    Result::Err(MyError::ErrorA { message: "test error A", code: 501 })
}

fn main() {
    if let Result::Err(e) = method() {
        println!("{}", e);
    }
}
```

