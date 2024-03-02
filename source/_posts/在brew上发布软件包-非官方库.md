---
title: 在brew上发布软件包(非官方库)
donate: false
from: EchoJamie
url: 'https://echojamie.github.io/'
author: EchoJamie
about: "stay hungry, stay foolish.\U0001F98E"
avatar: /image/sidebar/avatar.jpg
comments: true
sticky: 0
tags:
  - brew
categories:
  - brew
abbrlink: 14275f01
description: 将本地开发的go程序, 实现通过brew安装
---

### 前言
最近在维护一个命令行工具, 作为一个深爱zsh的用户, 就想能否把这个命令行工具发布到brew上, 可以方便向别人推荐(chuī bī). 

### 创建安装脚本

1. 打开github仓库, 在Release内找到对应的版本, 右键复制下载链接. 

2. 打开命令行, 用刚刚复制的链接替换`<package-url>`, 并执行.
    ```bash
    brew create <package-url>
    ```

3. 执行完成后, 会要求你输入你的命令的名称, 输入完名称会自动打开一个Ruby文件, 要求你编辑安装脚本. 其中desc会变成仓库的描述信息, url就是刚刚的下载链接

    ```ruby
    # Documentation: https://github.com/Homebrew/brew/blob/master/share/doc/homebrew/Formula-Cookbook.md
    #                http://www.rubydoc.info/github/Homebrew/brew/master/Formula
    # PLEASE REMOVE ALL GENERATED COMMENTS BEFORE SUBMITTING YOUR PULL REQUEST!

    class Isx < Formula
        desc "isxcode organization-specific development tools"
        homepage ""
        url "https://github.com/isxcode/isx-cli/releases/download/v1.1.0/isx_darwin_arm64"
        sha256 "0b16fb5bc6579e71a8a186a691e6b6c10b25c1fc339775621d4c34f4e340a1de"

        # depends_on "cmake" => :build

        def install
            # Remove unrecognized options if they cause configure to fail
            # https://rubydoc.brew.sh/Formula.html#std_configure_args-instance_method
            system "./configure", "--disable-silent-rules", *std_configure_args
            # system "cmake", "-S", ".", "-B", "build", *std_cmake_args
        end

        test do
            # `test do` will create, run in and delete a temporary directory.
            #
            # This test will fail and we won't accept that! It's enough to just replace
            # "false" with the main program this formula installs, but it'd be nice if you
            # were more thorough. Run the test with `brew test otfcc-win32`. Options passed
            # to `brew install` such as `--HEAD` also need to be provided to `brew test`.
            #
            # The installed folder is not in the path, so use the entire path to any
            # executables being tested: `system "#{bin}/program", "do", "something"`.
            system "false"
        end
      end
    ```

4. 修改homepage, sha256以及install方法内代码.
    ```ruby
    # Documentation: https://docs.brew.sh/Formula-Cookbook
    #                https://rubydoc.brew.sh/Formula
    # PLEASE REMOVE ALL GENERATED COMMENTS BEFORE SUBMITTING YOUR PULL REQUEST!
    class Isx < Formula
        desc "isxcode organization-specific development tools"
        homepage "https://github.com/isxcode/isx-cli"
        url "https://github.com/isxcode/isx-cli/releases/download/v1.1.0/isx_darwin_arm64"
        version "1.1.0"
        sha256 "0b16fb5bc6579e71a8a186a691e6b6c10b25c1fc339775621d4c34f4e340a1de"
        license "Apache-2.0"
    
        # depends_on "cmake" => :build
    
        def install
          # Remove unrecognized options if they cause configure to fail
          # https://rubydoc.brew.sh/Formula.html#std_configure_args-instance_method
          # system "./configure", "--disable-silent-rules", *std_configure_args
          bin.install "isx_darwin_arm64" => "isx"
          # system "cmake", "-S", ".", "-B", "build", *std_cmake_args
        end
    
        # test do
          # `test do` will create, run in and delete a temporary directory.
          #
          # This test will fail and we won't accept that! For Homebrew/homebrew-core
          # this will need to be a test that verifies the functionality of the
          # software. Run the test with `brew test isx`. Options passed
          # to `brew install` such as `--HEAD` also need to be provided to `brew test`.
          #
          # The installed folder is not in the path, so use the entire path to any
          # executables being tested: `system "#{bin}/program", "do", "something"`.
          # system "false"
        # end
      end
    ```

5. 测试安装(笔者没有成功😭, 所以跳过了这步)

    ```bash
    brew update
    brew search isx
    brew install isx
    ```

### 创建个人tap
1. 在github上创建一个仓库, 名字为 `homebrew-<your-tap-name>`, 并将刚刚编辑的ruby文件（文件拓展名为.rb）上传到该仓库.

2. 随后验证是否成功. `<username>`替换为你的github用户名, `<your-tap-name>` 替换为你上一步中的tap名称
    ```bash
    brew tap <username>/<your-tap-name>
    brew search isx
    brew install isx
    ```

### 完结撒花🎉

至此, 你的个人命令行工具包就可以通过brew进行安装了, 但实际上并不属于brew官方包, 关于如何创建官方包可以关注作者后续的文章, 也可直接翻阅[brew官方文档](https://docs.brew.sh/Formula-Cookbook). 