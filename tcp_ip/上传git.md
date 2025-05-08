1. 检查 SSH 密钥是否存在
ls -al ~/.ssh
查看是否有 id_rsa（私钥）和 id_rsa.pub（公钥）文件。若没有，需生成新密钥：

ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
2. 将公钥添加到 GitHub
复制公钥内容：
cat ~/.ssh/id_rsa.pub
添加到 GitHub：
登录 GitHub → Settings → SSH and GPG keys → New SSH key。
粘贴公钥内容（以 ssh-rsa 开头）。
3. 验证 SSH 连接
ssh -T git@github.com
若显示 You've successfully authenticated 则配置成功。

4. 检查远程仓库 URL
确保远程仓库地址使用 SSH 格式（而非 HTTPS）：

bash
git remote -v
正确格式：git@github.com:your_username/repo_name.git
若为 HTTPS 格式，需修改为 SSH：
bash
git remote set-url origin git@github.com:your_username/repo_name.git
5. 检查 SSH 代理
确保 SSH 代理正在运行并加载密钥：

bash
eval "$(ssh-agent -s)"  # 启动代理
ssh-add ~/.ssh/id_rsa   # 添加私钥
6. 检查文件权限
SSH 密钥文件权限必须严格：

bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_rsa
chmod 644 ~/.ssh/id_rsa.pub
完成以上步骤后，再次尝试 git push。若问题依旧，请提供以下信息进一步排查：

ssh -T git@github.com 的输出。
git remote -v 的结果。