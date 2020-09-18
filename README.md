# GitHub運用マニュアル(仮)


## リポジトリ作成に関して

### リポジトリ命名規則

- 案件番号のPrefixはトルツメ (Bitbucketなどからimportする場合)
- 原則として `小文字のケバブケース`* (e.g. dx2, infini-production, ms-frontend)


### オプション設定 (Options)


**1. Features**

- Allow ForkingはDisabled
![](https://paper-attachments.dropbox.com/s_DEFD74B03744E445DF4463E84A3E0750A54F20348801396CDC651088D5C76423_1571977396774_+2019-10-25+12.18.56.png)


**2. Merge button**

- Allow squash merging のみにチェックを入れておくとmaster / developのコミットが綺麗になるため推奨
- Automatically delete head branches にチェックを入れておくとPRをマージ後、マージされたブランチを自動で削除してくれるため便利
![](https://paper-attachments.dropbox.com/s_DEFD74B03744E445DF4463E84A3E0750A54F20348801396CDC651088D5C76423_1571977427645_+2019-10-25+12.19.04.png)



### アクセスコントロール  (Collaborators & teams)
**Public Repositoryの場合**

設定不要 (デフォルトでOK)

**Private Repositoryの場合**

- Teamsにリポジトリにアクセス可能なTeamを `Write` 権限で追加
- TCを個別に `Admin` 権限で Collaborators に追加 (Organization OwnerはデフォルトでほぼAdmin権限と同等)
- NDVN・4DThai・3FC Teamを必要に応じて `Write` 権限で追加
![](https://paper-attachments.dropbox.com/s_DEFD74B03744E445DF4463E84A3E0750A54F20348801396CDC651088D5C76423_1572424495529_+2019-10-30+17.34.01.png)


### 💡TIPS💡
Private Repository へのデフォルトのアクセス権は以下で設定している。(未設定の場合、Organization MemberであればどのリポジトリにもWrite権限を持つ設定がされている)

![](https://paper-attachments.dropbox.com/s_DEFD74B03744E445DF4463E84A3E0750A54F20348801396CDC651088D5C76423_1571994945089_+2019-10-25+18.15.32.png)

