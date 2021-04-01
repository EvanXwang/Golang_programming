# golang_gRPC  實作筆記

## 簡介
RPC指的是遠端程序呼叫 (Remote Procedure Call), 它的呼叫包含傳輸協定和編碼(物件序列)協定等   
允許執行於一台電腦上的程式呼叫另一台電腦上的副程式，而開發人員無須額外為這個互動作用程式設計  
就像對本機函數進行呼叫一樣方便。

## 優點
gRPC使用的IDL是Protobuf，Protobuf在用戶端和服務端上都能快速地進行序列化，並且序列化後的結果   
較小，能夠有效地節省傳輸佔用的資料大小，另外，gRPC是以HTTP/2協定為基礎進行設計，因此優勢非常顯著。


## 缺點
1. 可讀性差
2. 不支援瀏覽器呼叫
3. 外部元件支援較差


## 步驟

###初始化demo專案
1. mkdir grpc-demo
2. cd grpc-demo
3. go mod init github.com/go-programming-tour-book/grpc-demo (目錄內會產生go.mod檔)
4. 於grpc-demo目錄裡 , 新增 client 、 proto 、 server 資料夾

###編譯和產生proto檔案
1. 在proto 目錄下新增 helloworld.proto 檔案
2. 在專案根目錄下執行 protoc --go_out=plugins=grpc:. ./proto/*.proto  

QA ：若出現錯誤如下：
   protoc-gen-go: program not found or is not executable
   Please specify a program using absolute path or make sure the program is available in your PATH system variable
   --go_out: protoc-gen-go: Plugin failed with status code 1.
   
   vim ~/.bash_profile  新增二行指令如下：  
   export GO_PATH=~/go  
   export PATH=$PATH:/$GO_PATH/bin
   
   cmd執行　source ~/.bash_profile

3. 執行後會產生此proto檔案 對應的.pb.go檔案  > helloworld.pb.go


###安裝gRPC

1. 在專案下執行   go get -u google.golang.org/grpc@v1.29.1

在gRPC中，一共包含四種呼叫方式：  

● Unary RPC ：一元RPC  
● Server-side streaming RPC ： 服務端流式RPC  
● Client-side streaming RPC ： 用戶端流式RPC  
● Bidirectional streaming RPC ： 雙向流式RPC

   
   
   
