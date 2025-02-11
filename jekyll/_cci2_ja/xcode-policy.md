---
layout: classic-docs
title: Xcode イメージのリリース、更新、サポート終了に関する CircleCI のポリシーについて
short-title: Xcode イメージのリリース、更新、サポート終了に関する CircleCI のポリシーについて
categories:
  - プラットフォーム
description: Xcode イメージのリリース、更新、サポート終了に関する CircleCI のポリシーについて
order: 31
version:
  - Cloud
---

* 目次
{:toc}

## 概要
{: #overview }
{:.no_toc}

ここでは、Xcode のリリース、更新、サポート終了に関する CircleCI のポリシーについて説明します。 CircleCI では、ベータ版イメージを含め、新しいイメージのリリースを切れ目なくスピーディかつ円滑に行うため、Xcode イメージについて明確なポリシーを定めています。

## Xcode イメージの維持およびサポート終了
{: #xcode-image-retention-and-deprecation }

CircleCI では、Xcode のメジャー バージョンを 4 つまで維持し、新しいバージョンについては複数のイメージを提供することを目標としています。

Xcode 12 が最新のリリース済みメジャー バージョンである執筆時点では、次のようになります。

| Xcode のバージョン | 対応                                                             |
| ------------ | -------------------------------------------------------------- |
| Xcode 12     | すべてのメジャー/マイナー バージョンについて最新のパッチ バージョンを維持します。                     |
| Xcode 11     | すべてのメジャー/マイナー バージョンについて最新のパッチ バージョンを維持します。                     |
| Xcode 10     | 今後の Xcode 12 リリースの発表に応じて、過去の Xcode 10 バージョンに対するサポートを段階的に終了します。 |
| Xcode 9      | Xcode 9 の最後の安定版リリースとなるイメージ 1 つのみを維持します。                        |
| Xcode 8      | 完全に削除されました。                                                    |
{: class="table table-striped"}

今後、Xcode 13 のベータ版イメージがリリースされた場合の対応は次のようになります。

| Xcode のバージョン | 対応                                                                                      |
| ------------ | --------------------------------------------------------------------------------------- |
| Xcode 13     | ベータ版イメージ ポリシーに従いベータ版イメージをリリースおよび更新します。                                                  |
| Xcode 12     | すべてのメジャー/マイナー バージョンについて最新のパッチ バージョンを維持します。                                              |
| Xcode 11     | ベータ期間中はすべての `メジャー/マイナー` バージョンについて最新のパッチ バージョンを維持し、Xcode 13 のリリース サイクル開始後はサポート終了の対象とします。 |
| Xcode 10     | Xcode 13 の GM 版がリリースされ次第、最終リリースを除くすべてのイメージをサポート終了の対象とします。                               |
| Xcode 9      | Xcode 13 の GM 版がリリースされ次第、サポート終了の対象とし、削除します。                                             |
{: class="table table-striped"}

イメージがサポート終了対象および削除対象となった場合、[CircleCI Discuss フォーラム](https://discuss.circleci.com/c/announcements/39)で告知し、最近実行したジョブでサポート終了対象イメージをリクエストした開発者の方々にはメールでも通知を行います。 CircleCI では、サポートが終了する4 週間前には通知するようにしています。

イメージに対するリクエストが、自動で別のメジャー/マイナー バージョンにリダイレクトされることはありません。 そのため、リクエストしたイメージのいずれかが削除された場合、設定ファイルの更新を行わないと、ジョブが失敗するようになります。

## Xcode のパッチ
{: #xcode-patches }

CircleCI では、サポート対象の Xcodeの `メジャー/マイナー` バージョンごとに最新のパッチ バージョンを維持します。 新しいパッチ バージョンがリリースされた場合、過去のパッチ バージョンのサポートを終了し、すべてのリクエストを新しいパッチにリダイレクトします。

通常、パッチには後方互換性が備わっているため、このリダイレクトは新しいパッチのリリースから 24 時間以内に開始されます。 深刻な問題が確認された場合には、ロールバック版をリリースし、暫定的にどちらのバージョンも利用可能にします。

****例: ****

Xcode `12.0.1` がリリースされた時点で、過去のパッチ バージョンである `12.0.0` を削除し、`12.0.0` に対するすべてのリクエストを `12.0.1` にリダイレクトします。

## ベータ版イメージのサポート
{: #beta-image-support }

Xcode の次の安定版がリリースされる前に開発者の方々がアプリのテストを行えるよう、可能な限り早期に macOS Executor で Xcode のベータ版をリリースできるよう尽力します。

ベータ版イメージについては、安定版イメージ (更新されない) とは異なり、GM (安定版) イメージがリリースされ更新が停止するまでは、新規リリースのたびに既存のイメージが上書きされます。 現在ベータ版となっているバージョンの Xcode イメージをリクエストする場合、Apple が新しい Xcode ベータ版をリリースした際、最小限の通知によりそのイメージに変更が加えられることをご了承ください。 これには、CircleCI では制御できない Xcode および関連ツールに関する互換性を損なう変更が含まれる場合があります。

ベータ版イメージに関する CircleCI のお客様サポート ポリシーについては、[サポート センターに関する記事](https://support.circleci.com/hc/ja-jp/articles/360046930351-What-is-CircleCI-s-Xcode-Beta-Image-Support-Policy-)をご覧ください。

## Xcode イメージのリリース
{: #xcode-image-releases }

CircleCI では Apple の Xcode のリリース状況を注意深く追跡し、常に可能な限り迅速に新しいイメージをリリースするよう努めています。 この作業は Xcode と macOS で行われる変更に大きく依存するため、リリースについて SLA として所要時間を公式に定めてはおりません。

新しいイメージがリリースされた際は必ず、[CircleCI の Discuss サイト](https://discuss.circleci.com/c/announcements/39)でリリース告知により通知します。 また、[こちらの Xcode バージョンの表](https://circleci.com/docs/2.0/testing-ios/#supported-xcode-versions)に追記します。

## macOS のバージョン
{: #macos-versions }

各 Xcode イメージは、macOS のクリーン インストールを基盤としています。 CircleCI では、macOS バージョンの更新を Xcode の必要最小バージョンが上がったときにのみ行い、できる限りバージョンを一定に保つようにしています。 Xcode の必要最小バージョンが上がった場合は、macOS のバージョンを最新の安定版バージョンに更新します。

macOS の新しいメジャー バージョン (`10.15` や `11.0` など) がリリースされた場合、重大なバグや問題が発生した際に解決できるように、通常は Xcode のマイナー バージョンが 2 つ以上リリースされた後、そのバージョンの使用を開始します。 このリリースのタイミングは Apple のリリース サイクル次第ですが、必ず事前に [CircleCI Discuss フォーラム](https://discuss.circleci.com/c/announcements/39)で告知します。

## 例外
{: #exceptions }

CircleCI は、どのような場合でも、状況に応じて本記事の説明内容とは異なる措置を講じる権利を保有しています。 本ポリシーの例外を適用する必要がある場合、可能な限り十分な告知を行い、透明性を維持するよう努めます。 そのような場合、[CircleCI Discuss フォーラム](https://discuss.circleci.com/c/announcements/39)に告知を掲載するとともに、可能な限りメールなどでの通知も行います。
