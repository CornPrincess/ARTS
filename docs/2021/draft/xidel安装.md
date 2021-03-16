# Xidel安装记录

Xidel是一款可以解析http请求的实用工具，[官方文档](https://www.videlibri.de/xidel.html)

## 安装步骤

### homebrew安装

以前 可以使用 homebrew 进行安装，非常方便，直接使用以下命令即可

```shell
brew install xidel
```

但是现在homebrew库已经失效

### 手动编译安装

手动安装时主要参考了对应 [homebrew formula文件](https://github.com/Homebrew/homebrew-core/blob/HEAD/Formula/xidel.rb)

```shell
class Xidel < Formula
  desc "XPath/XQuery 3.0, JSONiq interpreter to extract data from HTML/XML/JSON"
  homepage "https://www.videlibri.de/xidel.html"
  url "https://github.com/benibela/xidel/releases/download/Xidel_0.9.8/xidel-0.9.8.src.tar.gz"
  sha256 "72b5b1a2fc44a0a61831e268c45bc6a6c28e3533b5445151bfbdeaf1562af39c"
  license "GPL-3.0-or-later"

  bottle do
    rebuild 1
    sha256 cellar: :any_skip_relocation, mojave:      "885e1685c81a6abb9767a6e807894a98b5d296952e60fdad6341961ce4dc737e"
    sha256 cellar: :any_skip_relocation, high_sierra: "16eb3dc18004c0be8e384714ef543aa6dfe0b026e4ec0a7b6294dd499606bb12"
    sha256 cellar: :any_skip_relocation, sierra:      "623ba6f72816f4d9cb2055539a023f36a620add9c77a61193fcaea88a08cedf5"
  end

  disable! date: "2020-12-08", because: :unmaintained

  depends_on "fpc"
  depends_on "openssl@1.1"

  def install
    cd "programs/internet/xidel" do
      system "./build.sh"
      bin.install "xidel"
      man1.install "meta/xidel.1"
    end
  end

  test do
    assert_equal "123\n", shell_output("#{bin}/xidel -e 123")
  end
end
```

#### 下载源文件

[ xidel-0.9.8.src.tar.gz](https://sourceforge.net/projects/videlibri/files/Xidel/Xidel 0.9.8/xidel-0.9.8.src.tar.gz/download)

#### 解压文件

```shell
tar -zxvf xidel-0.9.8.src.tar.gz
```

#### 编译源码

```shell
cd ${xidel-repo}/programs/internet/xidel
./build
```

#### 安装

```shell
cd ${xidel-repo}/programs/internet/xidel
./install.sh
```

其中在执行 `./install` 命令时报错

> install /usr/bin/xidel Operation Permission Not Allowed

尝试解决方法：[停止 Mac SIP](https://developer.apple.com/documentation/security/disabling_and_enabling_system_integrity_protection)

停止 SIP后，错误变成了如下信息：

> install: /usr/bin/xidel: Read-only file system

尝试解决办法：`sudo mount -uw /`，该命令失败：`mount_apfs: volume could not be mounted: Permission denied`

尝试将 `${xidel-repo}` 编译生产的 xidel 复制入 `/usr/local/bin` 目录下，但是软件不能正常使用