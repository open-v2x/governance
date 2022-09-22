# OpenV2x 发布流程

涉及 REPOS:

- [cerebrum](https://github.com/open-v2x/cerebrum)
- [docs](https://github.com/open-v2x/docs)
- [dandelion](https://github.com/open-v2x/dandelion)
- [edgeview](https://github.com/open-v2x/edgeview)
- [roadmocker](https://github.com/open-v2x/roadmocker)
- [centerview](https://github.com/open-v2x/centerview)

## 1. 创建分支

以 open-v2x/docs 为例:

![create-branch](images/create-branch.png)

- `Branch name` 为新分支名称
- `Branch source` 为现有分支，以现有分支为基础拉取分支
- 注意:
  - 拉取分支需要有改项目的相应权限
  - 新分支名，可以参考 openstack 的命名规则，如"stable/wallaby"

## 2. 提交切换分支变更代码

拉取各项目新分支代码，修改分支和 tag 名，再提交到新分支上

参考提交:

- https://github.com/open-v2x/cerebrum/commit/179bed8c7cf6af3095e35102d4aa1abc9fcd3d7e
- https://github.com/open-v2x/docs/commit/98ab54c39631a3f387cbb2a61de55c4970982f90
- https://github.com/open-v2x/dandelion/commit/d96bfd9e47e93df90d658d1ab65b62ca3c94c598
- https://github.com/open-v2x/edgeview/commit/adb90fec3b62da1205701e2786c42ee1faad0072
- https://github.com/open-v2x/centerview/commit/bb13814222057e5a6889d7da7dd88d6f556a519e
- https://github.com/open-v2x/roadmocker/commit/f3341f2f263f2d5030049265504c14712391b1b1

注意事项:

- `.drone.yml` 里面的一些分支和 tag 名，要和新分支名保持一致
- `.github/workflows/` 下 的一些 CI 文件，里面的分支和 tag 名，要和新分支名保持一致
- `.md` 结尾的文件，可以搜索一下，有没有按照分支名和 tag 名定义的地方，也需要和新分支保持一致
- `open-v2x/docs` 项目里面，还需要修改`install.sh`脚本和 depoly 文件夹下的 `yaml` 文件

## 3. 部署测试

### 3.1 部署

等待变更代码合并之后，观察 [Dockerhub](https://hub.docker.com/u/openv2x) 镜像仓库中是否有新分支镜像生成（镜像由 CI 自动 build 和 push）

![dockerhub-openv2x](images/dockerhub-openv2x.png)

待镜像上传完成之后，根据 `open-v2x/docs` 项目新分支下的部署文档，进行安装部署

### 3.2 测试

测试过程略

## 4. 版本发布

## 4.1 Release Note

> 参考: https://github.com/open-v2x/docs/releases/tag/albany-1.0.126

基本包含:

- Release Version: 发布的版本，如:"alabny"
- Release Date: 发布的日期，格式参考:"July 29, 2022"
- Feature List: 功能列表，可以对比上次发版时的提交记录，列出新增功能
- Bug Fix: 缺陷修复，同样可以对比上次发版的提交记录，列出新修复的缺陷问题
- Known Issue: 指的是未解决问题列表，需要提交 issue 到对应项目下

## 4.2 tag 命名规则

> 参考 albany-1.0.126

基本包含:

- 发布版本，如: "alabny"
- API 接口版本: 接口无删减的情况下，数字不变，一般为"1"
- 功能新增: 同一发布版本有功能新增时数字递增
- bug 修复数量: 截止版本发布日期当天的 bug 修复数量

## 4.3 发布

到 `open-v2x/docs` 项目下点击 [Releases](https://github.com/open-v2x/docs/releases) 到 release 列表，新建一个
release

![create-release](images/create-release.png)

1. tag: 选择一个已经存在的 tag ，或者根据新的分支创建一个新的 tag
2. release title: 填写标题，简易扼要
3. release note: 将 release note 全部写入，注意 markdown 格式
4. publish: 发布版本，也可以保存到草稿，后续修改完再发版
