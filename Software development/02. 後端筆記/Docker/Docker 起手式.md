#### 為什麼要使用 Docker 

過去當要架設應用程式時，在還不清楚應用程式的效能需求時，就需要先去買一台主機，但這常常需要用推估的，而且可能會浪費了在一台主機的資源和經費。

到了虛擬機器（Virtual machines, VM），它讓我們可以在單一的伺服器上運作多個不同的 App，但它還是有缺點，每一個 VM 都需要完整的 Ｏ S 才能執行，而每一個 OS 都需要 CPU, RAM 等才能運作，亦導致成本的增加。

為了解決 VM 的問題，開始使用容器化技術。它可以在相同的主機上運行多的 container，從而釋放更多的 CPU 和 RAM 讓其他需要的地方使用。

![[部署演進史.png]]

#### Docker 主要功能
- 簡化部署流程
- 跨平台部署
- 建立乾淨測試環境

![[Docker功能.png]]

#### 適用情境
- 公司專案的部署流程繁雜，同時設定檔與參數又多，還得全程手動操作，既費時又難以維持人工的部署品質
- 公司資料庫資料充斥著大量髒資料，導致開發者以及測試人員難以判斷是新功能沒做好，抑或是髒資料的問題
- 公司大多數開發人員使用 Mac 作業系統開發，然而客戶端的環境五花八門，有 Windows、Linux 或是不同版本的 Mac 環境。常常開發好的專案，放到了別的環境後，許多功能就壞了，因此沒辦法準時地按照合約在客戶那上架。

對於開發者來說，透過 Docker 可以確保每一個開發者和每一個伺服器（包含上線、開發和測試）時的開發環境相同。任何人都可以在短時間內設置好專案，不需要再去花許多時間搞設定，安裝套件等等。

#### 關鍵概念

- **Docker Image（Docker 映像檔）**：一個打包好的應用程式，包含了應用程式程式碼，以及運行該應用程式所需的所有東西，如程式庫、工具和設定。Docker 映像檔是靜態的，不會變化。
- **Docker Container（Docker 容器）**：Docker Image 的運行實例。當你啟動一個容器時，它會根據 Docker Image創建一個可運行的環境。容器包含了一個正在運行的應用程式和它的環境。容器是動態的，可以啟動、停止和刪除。
- **Docker Compose**：這是一個工具，用於定義和運行多個 Docker Container。它允許在一個設定文件中定義所有需要的容器，然後使用一個命令來一次性啟動整個應用程式環境。

[[Docker常用指令]]
### Reference: 
[圖解Docker教學＠youtube](https://www.youtube.com/watch?v=0fFO2ez1dWA&list=PLVVMQF8vWNCJnlO0Y34AE_1AgCapldp38&index=15)
[Docker-從入門到實踐](https://philipzheng.gitbook.io/docker_practice/)
[Docker Official Doc](https://docs.docker.com/get-started/overview/)





