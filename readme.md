# 搭建个人博客

技术栈：vitepress + github pages + git actions 

实现功能
- 评论


## vitepress 搭建博客


## gitee 2 github 镜像同步
1. gitee 和 github 上分别注册两个名字相同的仓库。
2. gitee repo 管理 -> 仓库镜像管理 -> 添加镜像 -> github 对应仓库
3. 获取 GitHub 私人令牌：Settings -> Developer setting -> Personal access tokens -> Generate new token. 此路径全选 classic。
   1. note 随意
   2. Select scopes：repo\admin:repo_hook(用于自动生成 webhook，需要 Gitee 自动从 GitHub 同步仓库时，建议勾选)
   3. Generate token

## github actions
```yml
# https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs

name: deploy-website

on:
  schedule:
    # 此处是UTC时间，对应北京时间早八点
    # - cron : '00 00 * * *'
    push:
      branches: [main]

  workflow_dispatch:

permissions:
  contents: read

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - name: install nodejs
        uses: actions/setup-node@v2.5.1
        with:
          node-version: "14.x"
      - name: Install dependencies
        run: npm install
      - name: build app
        run: npm run build
      - name: copy dist file with scp
        uses: appleboy/setup-node@v2.5.1
        target: '目标文件夹目录'
        with: 
          host: 'ip'
          username: 'user'
          password: 'password'
          port: '22'
          source: 'docs/' # 拷贝的目录
        env:
          JD_COOKIE: ${{ secrets.JD_COOKIE }}
          APP_ID: ${{ secrets.APP_ID }}
          APP_SECRET: ${{ password.APP_SECRET }}
          OPEN_ID: ${{ secrets.OPEN_ID }}
          TEMPLATE_ID: ${{ secrets.TEMPLATE_ID }}
```

## 配置自定义域名


# 微信机器人
https://www.bilibili.com/read/cv27878465
https://www.bilibili.com/video/BV19i4y1a7aG/
https://www.bilibili.com/video/BV1Ng4y1r7EP/
https://www.bilibili.com/video/BV1xg4y1m7wW/