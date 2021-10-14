```shell
@echo

rem "进入zhidian-web目录"
cd D:\zhidianGitLab\zhidian\zhidian-web
rem "拉取代码"
git pull
rem "判断 m_dist文件夹是否存在，存在就删除"
if exist D:\zhidianGitLab\zhidian\zhidian-web\m_dist rd /s /q D:\zhidianGitLab\zhidian\zhidian-web\m_dist
rem "进入移动端mobile文件夹"
cd D:\zhidianGitLab\zhidian\zhidian-web\mobile
rem "执行依赖安装"
call yarn
rem "压缩移动端项目"
call yarn build
rem "返回上一级zhidian-web目录"
cd ..
rem "将移动端dist项目移动并重命名为m_dist"
mv mobile/dist/ m_dist
rem "执行部署到服务器的脚本"
call yarn auto

```

