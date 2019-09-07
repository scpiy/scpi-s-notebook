#### dinary list

#### 关于ubuntu上的npm更新

更新npm的时候，先后使用了

```
# 升级npm自身
npm install -g npm
```

```
# 升级node.js
sudo npm cache clean -f
sudo npm install -g n
sudo n stable
```

还有一个忘了是什么的命令，用处大概是把npm升级到最新版本，一段操作猛如虎后，使用`npm -v`查看npm的版本发现还是没有更新......当时有点挫败。

然后灵机一动，是不是需要重启一次电脑。**然后reboot一下，问题全部解决。很舒服。**

