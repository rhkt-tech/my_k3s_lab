# greenwich に移動済み 

# my_k3s_lab

Lab用 kubernetes 環境をサッと作るためのdocker compose

## 提供するもの

次の自動インストール

- cert-manager
- cloudflare-operator
- kubernetes-dashobard
- tor-controller

起動後 output/kubeconfig.yaml に kubectl のコンフィグが吐かれるのでこれを利用する。 

## 事前要件

- sysbox-ce 導入済み
- docker compose 導入済み

## 環境固有設定

### NW周り

.env 
```
K3S_TOKEN=xxxxxxxxxxxxxxxxxxxxxxxxxxxxx
CLUSTER_DOMAIN=k3s.local.domain
POD_CIDR=10.254.0.0/17
SVC_CIDR=10.254.128.0/17
NODE_EXT_IP=10.0.0.1
```

### コンテナレジストリの追加

registries.yaml
```yaml
mirrors:
  ghcr.io:
    endoint:
      - "https://ghcr.io"
configs:
  "ghcr.io":
    auth:
      username: xxxxxxxxxxxxxxxxx
      password: xxxxxxxxxxxxxxxxx
```

不要であれば空ファイルでよい 

## 仕組み

### kubernetes のカスタマイズ 

/manifests/* に入れてある yaml が自動でデプロイされるので必要なものを展開済み。

### フォルダについて

- /data: コンテナなど
- /persistent: PVを作る場合に使用
