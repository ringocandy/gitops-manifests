# 概要
- ArgoCDでMetalLBとBINDコンテナを展開するためのManifestです
- App of Apps構成になっているため、root-appを展開することでMetalLBとBINDを同時に展開できます
- 使い方はこちら https://note.com/ringocandy/n/n17272a8757b4

# root-app
- App of Appsのメインアプリ
- dns_single/apps/ 配下のディレクトリにあるアプリを一斉展開する
- 各アプリのNamespaceはディレクトリ名と同じものが使用される
- CreateNamespace=true のため、Namespaceが存在しない場合は新規に作成される

# bind
- bind-deploy.yaml の replicas: 2 に従って常時2コンテナが維持される
- MetalLBにIPv4のVIPが付与され、配下にコンテナがぶら下がる

# metallb-system
- Chart.yaml
  - MetalLB本体はHelmでインストールされる
  - template配下のconfigを参照する
- values.yaml
  - crdsを有効化することでIPAddressPoolやL2Advertisementを使えるようにしている
-  templates/ip-config-v4.yaml
  - LBの構築に必要なIPアドレス情報を記載 
