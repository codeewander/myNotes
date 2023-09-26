---
date: 2023.09.23
mindmap-plugin: basic
---
### Why  to use #remote-SSH ?
#### **Access to Specialized Environment 需要特定環境**
When you need to access specific development or testing environments that may differ from your local development setup	
#### **Cross-Platform Development 跨平台開發** 
If you need to develop and test your application on multiple platforms (e.g., Windows, Linux, macOS)
#### **Cloud-Based Development 遠端伺服器開發** 
When you are developing applications that will ultimately run on cloud servers (e.g., AWS, Azure, Google Cloud)
#### **Resource-Intensive Tasks 需要特定電腦資源**
When your development tasks require significant computational power or memory
#### Avoid local configuration 避免本地配置
Some development environments require complex configuration and dependency installations, using remote SSH can avoid the need for cumbersome local configuration and installations.

###  環境說明
1. Cloud: #Azure 
2. Editor: #VSCode 
	需要安裝 [Remote-SSH 套件](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh)
3. Version control service: #Gitlab 

### 步驟及做法
#### Step 1 : 在 Azure 創建新的 Resource group，並在下面新增 一台 VM 
- 點擊新增 Azure virtual machine 
- 選擇 Resource group 
- 設定  Machine name 和 Region (region 的選擇會影響 size 選項和價格方案)
- 選擇驗證方式為SSH public key 
- 設定 Username
- 選擇 SSH public key source 為 Use existing public key 
- 查看本地的 SSH key 
	```
		// 本地 SSH key 通常在 ~/.ssh 目錄下
		cd ~/.ssh  
		// 倘若本地沒有 SSH key 的話則執行下面指令，這會產生一個私鑰和一個公鑰
		ssh-keygen 
		// 複製公鑰檔案
		cat ~/.ssh/id_rsa.pub
	```
- 將公鑰內容貼到 SSH public key 欄位上
- 倘若希望省錢的話，可以在 Management 設定Auto-shutdown 
- 點擊 Review + create 
#### Step 2: VS Code 連線到 VM 
- 打開命令面板，輸入 "Remote-SSH: Connect to Host"
- 選擇 "Add New SSH Host"
- 輸入 Azure VM 的 SSH連接資訊，格式為 username@server_host 
	- server_host : public IP地址 
	- username : 創建 VM 時設定的 username 
		![[VSCode ssh.png]]
-  成功登入後，就會開啟一個新視窗(如果視窗左下角有顯示SSH:server_host 則表示連線成功)
#### Step 3: 檢查是否安裝 Git 
```
	// 查看 git 版本
	git --version
	// 若未安裝 git 則在 ubuntu環境上執行
	sudo apt-get update 
	sudo apt-get install git
```
#### Step 4: 在VM環境上創建 SSH keys (同本地創建一樣的指令)
#### Step 5: 將公鑰內容加到 GitLab SSH keys 中
	- 點擊 Setting => SSH keys 
	- 新增 key ，並將VM上創建的公鑰內容複製貼上
#### Step 6 : Git clone 專案到 VM 上
#### Step 7: 安裝專案相關的dependency


### Reference 
- [使用VSCode Remote透過 SSH 進行遠端開發](https://hackmd.io/@brick9450/vscode-remote)
- [How to use SSH keys with Windows on Azure](https://learn.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows)
- [Generate and store SSH keys in the Azure portal](https://learn.microsoft.com/en-us/azure/virtual-machines/ssh-keys-portal#upload-an-ssh-key)
