# Ruby 本地预览手册（Jekyll）

本文用于在 Windows + PowerShell 环境下，完成 s-note 的本地预览。  
仓库结构为 `docs/` 作为 GitHub Pages 发布源目录。

## 环境配置

### 1. 安装 Ruby 3（推荐 3.3.x）

1. 打开 RubyInstaller 下载页：<https://rubyinstaller.org/downloads/>
2. 下载并安装 `Ruby+Devkit 3.3.x (x64)`。
3. 安装时勾选将 Ruby 加入 PATH。
4. 安装结束后执行 `ridk install`，按推荐选项完成 MSYS2 工具安装。

### 2. 验证安装

新开 PowerShell，执行：

```powershell
ruby -v
gem -v
bundle -v
where.exe ruby
where.exe bundle
```

`ruby -v` 应显示 `3.x.x`。  
如果仍命中旧版本 Ruby，可在当前终端临时调整 PATH（按实际安装目录修改）：

```powershell
$env:Path="C:\Ruby33-x64\bin;C:\Ruby33-x64\msys64\usr\bin;$env:Path"
ruby -v
```

### 3. 准备项目依赖

进入仓库根目录：

```powershell
cd <仓库根目录>
```

首次建议设置 bundler 本地安装路径与镜像：

```powershell
bundle config set path vendor/bundle
bundle config set mirror.https://rubygems.org https://gems.ruby-china.com
```

安装依赖：

```powershell
bundle install
```

验证依赖：

```powershell
bundle check
```

出现 `The Gemfile's dependencies are satisfied` 即表示依赖正常。

## 预览操作

### 1. 本地构建验证（可选但推荐）

```powershell
cd <仓库根目录>
bundle exec jekyll build --source docs --baseurl "/s-note"
```

构建成功后会在根目录生成 `_site/`。

### 2. 启动本地预览服务

```powershell
cd <仓库根目录>
bundle exec jekyll serve --source docs --baseurl "/s-note"
```

浏览器访问：

- <http://127.0.0.1:4000/s-note/>

### 3. 常用故障处理

- **端口占用**

```powershell
bundle exec jekyll serve --source docs --baseurl "/s-note" --port 4001
```

- **依赖报错或版本漂移**

```powershell
bundle install
bundle check
```

- **终端识别到错误 Ruby 版本**

```powershell
$env:Path="C:\Ruby33-x64\bin;C:\Ruby33-x64\msys64\usr\bin;$env:Path"
ruby -v
```

## 说明

- 站点源目录为 `docs/`，请始终使用 `--source docs`。
- 项目站点使用 `baseurl: "/s-note"`，本地预览请带 `--baseurl "/s-note"` 以贴近线上路径。
