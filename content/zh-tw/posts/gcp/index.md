---
slug: gcp
title: gcp
date: 2025-10-28 12:07:45
tags:
- google cloud
- google 
categories:
  - Note
---
slug: gcp

# 臨時抱佛腳-GCP競賽整理
[筆記-觀念釐清](https://hackmd.io/@Eason2392/B1CqW-mkC)

## 22年考古

### 建立VM|VPC

#### create VPC | SubNet | FR | VM |SSH
```=
gcloud compute networks create --help
gcloud compute networks subnets create --help
gcloud compute firewall-rules create --help
gcloud compute instances create --help
gcloud compute ssh --help
```
### 建立SQL DB

```=
gcloud compute networks create --help
gcloud compute networks subnets create --help
```
#### 建立cloud sql | management instance group

```=
gcloud sql instances --help
gcloud compute instance-templates create --help
gcloud compute instance-groups managed create --help
gcloud compute instance-groups managed set-autoscaling --help
gcloud compute instances add-tags --help
```
##### firewall rule for healthy check

```=
gcloud compute firewall-rules create --help
```
##### HTTP load balance

```=
gcloud compute addresses create --help
gcloud compute http-health-checks --help
gcloud compute backend-services create --help
gcloud compute backend-services add-backend url-maps --help 
gcloud compute target-http-proxies create --help 
gcloud compute forwarding-rules create --help 
```

### GCS BUCKET

```=
gcloud builds submit --help
gcloud run deploy --help
```
# 22年解題過程
## 題目1

題目翻譯：
MeiDei演唱會的門票將在幾天內開放售賣。你的朋友想和他/她的家人一起享受這場演唱會，所以他/她急需一對門票。他/她請求你幫他/她準備一台機器，然後他/她將啟動一些魔法腳本，一旦門票開放售賣就自動購買。票務系統位於台灣，你應該將從機器到票務系統的延遲降到最低，並且預算要小。為了保護這台機器，你需要設定只允許你和你的朋友（referee-group@taiwan-52nd-national-skills-competition.today）使用Cloud Shell或cloud命令登錄。你的環境應該擁有：

名為meidei-vpe的VPC網絡
名為meidei-vpc-subnet的子網，位置：亞洲-東部-1，IP範圍：192.168.100.0/24
防火牆規則名稱：allow-ssh-only
虛擬機器名稱：give-me-tickets（2個vCPU、4GB內存、10GB磁盤、Debian GNU/Linux 10（buster），在meidei-vpe-subnet1子網中，區域為亞洲-東部-1）
使用gcloud解決這個問題。

以下是使用gcloud的解答：

bash
Copy code
*創建VPC網絡和子網*
```=
gcloud compute networks create meidei-vpe --subnet-mode=custom
gcloud compute networks subnets create meidei-vpc-subnet --network=meidei-vpe --region=asia-east1 --range=192.168.100.0/24
```
*創建防火牆規則*
```=
gcloud compute firewall-rules create allow-ssh-only --network=meidei-vpe --allow=tcp:22 --source-ranges=[YOUR_IP]/32
```
*啟動虛擬機*
```=
gcloud compute instances create give-me-tickets --machine-type=n1-standard-2 --zone=asia-east1-a --subnet=meidei-vpc-subnet --image-family=debian-10 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-standard --boot-disk-device-name=give-me-tickets
```
*添加SSH訪問權限*
```=
gcloud compute instances add-metadata give-me-tickets --metadata=ssh-keys=[USERNAME]:$(cat ~/.ssh/id_rsa.pub)
```
*允許Cloud Shell或cloud命令登錄*
```=
gcloud compute instances add-metadata give-me-tickets --metadata=enable-oslogin=TRUE
```
*添加參與者（你的朋友）*
```=
gcloud projects add-iam-policy-binding [YOUR_PROJECT_ID] --member=group:referee-group@taiwan-52nd-national-skills-competition.today --role=roles/compute.osLogin
```
請替換命令中的[YOUR_IP]和[YOUR_PROJECT_ID]為你自己的IP地址和項目ID。

## 題目2
題目翻譯：
BPM麵包店的業務蓬勃發展。由於服務能力不足，他們對自己的線上訂單系統感到困擾。他們進行了一些調查，最終決定將本地系統遷移到雲端。經過討論，你負責在GCP上設計一個架構來為BPM麵包店的線上訂單系統提供服務。他們希望系統能夠提供高可用性（能夠處理來自同一源VM的2000個並發請求）並且成本低廉。他們將提供他們網站的源代碼和數據庫的轉儲，你將幫助他們將這些資源遷移到雲環境中。
BPM麵包店提供的資源（您的項目有權讀取這些資源，這些資源存儲在Cloud Storage存儲桶中）：
環境應該包括：
- 名為bpm-vpe的VPC網絡
- 台灣用於Web伺服器的子網，名為bpm-vpc-subnetl（10.0.1.0/24）。
- Google管理的SQL數據庫（MySQL 8.0），標記為problem-number: 2（請確保將problem-number: 2作為用戶定義標籤而不是Cloud SQL實例的名稱），沒有外部IP並僅允許來自Web伺服器的連接。
- 在bpm-vpe-subnetl（區域b）中的管理實例群組，名為bpm-mig：
  - 每個實例沒有外部IP，但需要能夠連接到互聯網；
  - 每個實例的正常使用目的規格為2個vCPU、4GB RAM和10GB Debian GNU/Linux 10（buster）持久性磁碟；
  - 能夠根據CPU利用率閾值（60%）進行擴展/縮減；
  - 須使用最少1個實例且最多2個實例提供流量，並開放端口80以提供Web伺服器的內容。
- 名為http-Ib的HTTP負載均衡器，具有名為htip-Ib-be的後端和名為http-ib-fe的前端（請使用預先準備的保留外部IP bpm-external-ip），用於將來自互聯網的流量負載均衡到Web伺服器。（對於此配置，請注意需要首先啟用健康檢查功能，方法是通過防火牆規則允許從130.211.0.0/22和35.191.0.0/16對實例的端口80進行入站。）

除了上述所需的資源外，您可能需要利用進一步必要的服務來確保您的架構正常運作。

以下是使用gcloud解題的步驟和解釋：

1. **建立VPC網絡和子網：**
   ```bash
   gcloud compute networks create bpm-vpe --subnet-mode=custom
   gcloud compute networks subnets create bpm-vpc-subnet1 --network=bpm-vpe --region=asia-east1 --range=10.0.1.0/24
   ```

2. **建立Google管理的SQL數據庫：**
   ```bash
   gcloud sql instances create [INSTANCE_NAME] --database-version=MYSQL_8_0 --region=[REGION] --no-address --labels=problem-number=2
   ```

3. **建立管理實例群組：**
   ```bash
   gcloud compute instance-templates create bpm-instance-template --machine-type=n1-standard-2 --subnet=bpm-vpc-subnet1 --tags=bpm-mig --image=debian-10 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-standard --boot-disk-device-name=bpm-instance-template
   gcloud compute instance-groups managed create bpm-mig --template=bpm-instance-template --base-instance-name=bpm-instance --size=1 --zone=[ZONE]
   ```

4. **設定HTTP負載均衡器：**
   ```bash
   gcloud compute addresses create bpm-external-ip --global
   gcloud compute firewall-rules create allow-health-check --network=bpm-vpe --allow=tcp:80 --source-ranges=130.211.0.0/22,35.191.0.0/16
   gcloud compute health-checks create http bpm-http-health-check --port=80
   gcloud compute backend-services create htip-Ib-be --protocol=HTTP --health-checks=bpm-http-health-check --global
   gcloud compute backend-services add-backend htip-Ib-be --instance-group=bpm-mig --instance-group-zone=[ZONE] --global
   gcloud compute url-maps create bpm-url-map --default-service=htip-Ib-be
   gcloud compute target-http-proxies create http-lb-proxy --url-map=bpm-url-map --global
   gcloud compute forwarding-rules create http-content-rule --address=bpm-external-ip --global --target-http-proxy=http-lb-proxy --ports=80
   ```

這些步驟將建立所需的基本架構，以實現高可用性並保持成本低廉。請替換適當的變量，如[

## 題目3
Luxubuuu 公司正在為他們的新業務建立一個智能相冊應用程序。該應用程序應該通過利用幾個微服務來建立，這些微服務包括一個用於圖像上傳的網站和一個地標檢測系統。他們決定外包靜態官方網站托管和地標檢測系統，而你被委託處理這個任務。
你需要讓網站可以通過保留的 IP 地址 luxubuuu-external-ip 從互聯網訪問。
網站源代碼的位置（您的項目有權讀取這些資源，這些資源存儲在 Cloud Storage 存儲桶中）：
gs://taiwan-52nd-national-skills-competition-cloud-computing/nsc-q3/website
此外，Luxubuuu 公司希望通過他們精心準備的 Web 用戶界面上傳圖像（上傳的圖像應該被防止公開訪問），並使用特定的應用程序編程接口檢索提取的地標信息。
他們希望採用 SERVERLESS 架構，並且只會為你提供兩個微服務源代碼和相應的 Dockerfile：一個用於上傳圖像，另一個用於檢索地標信息。除了部署這兩個 Docker 映像外，你還負責在幕後構建地標信息提取服務。（提示：你可以利用 Google Vision API 完成這個 LANDMARKS DETECTION 任務。）
提供的 Docker 映像經過良好編碼，但需要你修改一些環境變量：項目 ID、JSON 憑證的路徑、Cloud Storage 的存儲桶名稱、Firestore 的集合名稱和文檔名稱。客戶還指定，發送到 http://<luxubuuu-external-ip>/internal/upload 的請求將使用 upload-service，而發送到 http://<luxubuuu-external-ip>/internal/retrieve 的請求將轉發到 retrieve-service。
upload-service 源代碼位置（您的項目有權讀取這些資源，這些資源存儲在 Cloud Storage 存儲桶中）：
gs://taiwan-52nd-national-skills-competition-cloud-computing/nsc-q3/upload-service
retrieve-service 源代碼位置（您的項目有權讀取這些資源，這些資源存儲在 Cloud Storage 存儲桶中）：
gs://taiwan-52nd-national-skills-competition-cloud-computing/nsc-q3/retrieve-service
請注意，提供的 upload-service 源代碼中有一個硬編碼的 Google Cloud Storage 圖像上傳過程。同樣，提供的 retrieve-service 源代碼中有一個硬編碼的 Firestore。

以下是解決問題的步驟和相應的gcloud指令：

1. **設置網站靜態官方網站托管**：
```bash
gsutil mb gs://luxubuuu-website
gsutil cp gs://taiwan-52nd-national-skills-competition-cloud-computing/nsc-q3/website/* gs://luxubuuu-website
```

2. **設置地標檢測服務**：
這裡我們將使用 Google Vision API 來完成地標檢測任務，這是一個 Serverless 的解決方案。
```bash
gcloud services enable vision.googleapis.com
```

3. **部署微服務 upload-service 和 retrieve-service**：
這裡我們需要修改 Dockerfile 中的環境變量，然後使用 Cloud Build 來部署。
```bash
gcloud builds submit --tag gcr.io/[PROJECT_ID]/upload-service:v1 .
gcloud builds submit --tag gcr.io/[PROJECT_ID]/retrieve-service:v1 .
```

4. **部署 Cloud Function 來處理地標信息提取服務**：
這裡我們使用 Cloud Functions 來處理地標信息的提取。
```bash
gcloud functions deploy landmark-extraction \
  --runtime=nodejs14 \
  --trigger-http \
  --allow-unauthenticated
```

5. **設置 HTTP 負載平衡器轉發請求**：
```bash
gcloud compute addresses create luxubuuu-external-ip --global
gcloud compute backend-buckets create website-bucket --gcs-bucket-name=luxubuuu-website
gcloud compute backend-services create website-backend-service --global \
    --backend-bucket=website-bucket
gcloud compute url-maps create website-url-map --default-backend-service=website-backend-service
gcloud compute target-http-proxies create website-http-proxy --url-map=website-url-map
gcloud compute forwarding-rules create http-content-rule --address=luxubuuu-external-ip \
    --global --target-http-proxy=website-http-proxy --ports=80
```

這樣就完成了在 Google Cloud Platform 上構建 Luxubuuu 公司的智能相冊應用程序的架構設計。
    
## 考題公告
以下是與每個主題相關的gcloud指令以及它們的使用方法：

1. **Pub/Sub (佇列和發佈/訂閱)**：
   - **建立主題（Topic）**：
     ```bash
     gcloud pubsub topics create [TOPIC_NAME]
     ```
   - **訂閱主題（Subscription）**：
     ```bash
     gcloud pubsub subscriptions create [SUBSCRIPTION_NAME] --topic=[TOPIC_NAME]
     ```
   - **發佈訊息**：
     ```bash
     gcloud pubsub topics publish [TOPIC_NAME] --message="[MESSAGE_CONTENT]"
     ```

2. **Cloud Run (運算)**：
   - **部署服務**：
     ```bash
     gcloud run deploy [SERVICE_NAME] --image=[IMAGE_URL] --platform=managed
     ```
   - **列出服務**：
     ```bash
     gcloud run services list
     ```
   - **獲取服務 URL**：
     ```bash
     gcloud run services describe [SERVICE_NAME] --format='value(status.url)'
     ```

3. **Workflows (AWS Step Functions)**：
    
    gcloud services enable workflows.googleapis.com
   - **創建工作流程**：
     ```bash
     gcloud workflows deploy [WORKFLOW_NAME] --source=[WORKFLOW_DEFINITION_FILE]
     ```
   - **執行工作流程**：
     ```bash
     gcloud workflows execute [WORKFLOW_NAME] --data=[INPUT_DATA_FILE]
     ```
   - **列出工作流程**：
     ```bash
     gcloud workflows list
     ```

4. **Dataflow (AWS Kinesis Data Firehose)**：
   - **建立 Dataflow 作業**：
     ```bash
     gcloud dataflow jobs run [JOB_NAME] --gcs-location=[PIPELINE_SPECIFICATION_FILE] --region=[REGION]
     ```
   - **檢視作業狀態**：
     ```bash
     gcloud dataflow jobs describe [JOB_NAME] --region=[REGION]
     ```
   - **停止作業**：
     ```bash
     gcloud dataflow jobs cancel [JOB_NAME] --region=[REGION]
     ```

這些指令可讓你在 Google Cloud Platform 上使用相應的服務，提供了建立、管理和操作這些服務的功能。請根據你的需求和場景使用相應的指令。
    
## 考題資訊
以下是將這些主題相關的流程及gcloud指令進行規劃和佈署的步驟：

1. **具備可擴展性與高可用性的完整 web 應用程式架構**：

   - **規劃**：
     - 使用負載平衡器（如HTTP負載平衡器）將流量分發到多個實例。
     - 將實例部署在多個區域或區域內的多個區域（region），以提高可用性。
     - 使用自動擴展功能，以根據負載自動調整實例數量。
     - 使用故障轉移（Failover）功能來保護應用程式免受區域或區域內的故障。
     - 使用健康檢查來監控實例的狀態，並自動替換失效的實例。

   - **佈署**：
     ```bash
     # 創建負載平衡器
     gcloud compute forwarding-rules create [FORWARDING_RULE_NAME] \
         --load-balancing-scheme=INTERNAL \
         --backend-service=[BACKEND_SERVICE_NAME] \
         --region=[REGION] \
         --ports=80
     
     # 設置自動擴展
     gcloud compute instance-groups managed set-autoscaling [INSTANCE_GROUP_NAME] \
         --max-num-replicas=[MAX_REPLICAS] \
         --min-num-replicas=[MIN_REPLICAS] \
         --target-cpu-utilization=[TARGET_CPU_UTILIZATION]
     
     # 設置故障轉移
     gcloud compute addresses create [FAILOVER_IP_NAME] \
         --region=[REGION] \
         --addresses=[FAILOVER_IP]
     gcloud compute instance-groups managed set-named-ports [INSTANCE_GROUP_NAME] \
         --named-ports=[PORT_NAME]:[PORT_NUMBER]
     gcloud compute health-checks create http [HEALTH_CHECK_NAME] \
         --port=[PORT_NUMBER]
     gcloud compute backend-services add-backend [BACKEND_SERVICE_NAME] \
         --instance-group=[INSTANCE_GROUP_NAME] \
         --health-checks=[HEALTH_CHECK_NAME]
     gcloud compute target-pools create [TARGET_POOL_NAME] \
         --region=[REGION]
     gcloud compute target-pools add-instances [TARGET_POOL_NAME] \
         --instances=[INSTANCE_GROUP_NAME] \
         --instances-zone=[ZONE]
     gcloud compute forwarding-rules create [FAILOVER_RULE_NAME] \
         --region=[REGION] \
         --address=[FAILOVER_IP] \
         --target-pool=[TARGET_POOL_NAME]
     ```

2. **解決現有架構中的問題，建立具備高可用性、可擴充性、安全性和彈性的雲端佈署架構**：

   - **問題**：單點故障（Single Point of Failure）。
   - **解決方案**：使用多個區域/區域內的多個區域部署相同的應用程式，並使用負載平衡器來分發流量。

3. **處理持續性的連入請求**：

   - **規劃**：使用負載平衡器和自動擴展功能來處理大量的持續性連入請求。
   - **佈署**：參考上述具備可擴展性與高可用性的完整 web 應用程式架構的佈署步驟。

4. **提供可擴展的三層式 web 應用程式架構**：

   - **問題**：當流量增加時，傳統的三層式架構可能無法應對。
   - **解決方案**：使用自動擴展功能和負載平衡器來動態調整每個層級的資源，以應對不定量的流量請求。

5. **建立接收、轉換、處理和發佈資訊所需的雲端計算基礎結構**：

   - **規劃**：使用 Google Cloud Dataflow 來處理資訊流。
   - **佈署**：
     ```bash
     gcloud dataflow jobs run [JOB_NAME] \
         --gcs-location=[PIPELINE_SPECIFICATION_FILE] \

