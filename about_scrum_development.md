# スクラムとは

- アジャイル開発を行うためのフレームワーク
- フレームワークなので仕様というか、ガイドラインがある
  - https://www.scrumguides.org/docs/scrumguide/v1/Scrum-Guide-JA.pdf
  - https://www.scrumguides.org/scrum-guide.html
  - IPAの資料(https://www.ipa.go.jp/files/000065606.pdf)
- 何をどうやるかが具体化されているので一番メジャーになったのではないか


# スクラムについて理解するよりもまずはアジャイル

- アジャイルソフトウェア開発宣言
  - https://agilemanifesto.org/iso/ja/manifesto.html
  - https://agilemanifesto.org/iso/ja/principles.html

- アジャイル誕生の歴史
  - 製造業でやっていた分業スタイルをソフトウェア開発に導入 => ウォーターフォール開発
  - ウォーターフォールは今現在の社会では通用しなくなった
    - 最初に全部決めて基本後戻りしないのがウォータフォールだから...
  - その結果、専門分業性をやめて多能工である人をうまく機能するような方法を模索し始めた
  - 各地のチャレンジャーが、自分たちがやってみてうまくいったパターンを持ち込み、方法論としてまとめようとして議論し合意した結果が「アジャイルソフトウェア開発宣言」

- 結局アジャイルって何?
  - 変化に自律的に対応できるチームを作り、ソフトウェア開発に望むこと
    - 大切なのは納期ではなく、人でありプロダクト
    - プロダクト開発はやってみないとわからないことしかないので、スパンを短くして実施=>評価・フィードバック=>改善を繰り返すしかない
    - アジャイルさ = 変化に対応できる度合い

## スクラム以外のアジャイル

- XP(eXtreme Programming)、リーン開発、FDD(Feature Driven Development)
- https://www.slideshare.net/fkino/brief-history-of-agile-movement

# スクラム開発の概要

- スクラムは、スプリントという単位でイテレーション(反復)を繰り返す開発プロセス(1スプリントは1〜4週間のタイムボックス)
- チームは1スプリント内で以下を行う
  - スプリントプランニング
  - デイリースクラム(朝会、昼会、夕会とか呼ばれるやつ)
  - スプリントレビュー(成果物のレビュー)
  - スプリントレトロスペクティブ(そのスプリントの振り返り)
  - 開発作業
- 1スプリント内でやること(スプリントバックログ)はスプリントプランニングで決める(後述)


### スクラムチームに存在する役割

スクラムチームには以下の3つの役割が存在する


- プロダクトオーナー
  - (優先順位を含め)何を開発するか決める人
  - バックログのタスクの追加、削除、優先度決めはプロダクトオーナーの責任
- 開発チーム
  - 開発作業に携わる人
  - データサイエンティスト、プログラマー、デザイナーなどの明示的な役割は定義されていないが、専門的なスキルはあってよく、横断的に活かしてプロダクトに貢献することが推奨される
  - プロダクトの価値を高めていくことに責任を持つ

- スクラムマスター
  - 全体を支援・マネジメントする人
  - スクラム全体をうまく回すことに責任を持つ(スクラムを回すために何でもやる人) 
  - 開発チームを外部からの割り込みから守ったり、メンバーの悩み相談にのったり、開発を妨げる要因を取り除くために外部と交渉したりする


## スクラムイベント

スプリントでは以下の4つのイベントを行う

- スプリントプランニング
  - そのスプリントで何を行うかを決める
  - プロダクトオーナーがバックログの内容を説明し、開発チームがそれを確認してタスクを洗い出す。スクラムマスターはこれらの作業の支援を行う
  - タスクを洗い出す際は見積もりも行い、その結果を持ってスプリントで何を行うかの合意形成を行う
    - タスクの見積もりは人日のような絶対時間ではなく、相対的なポイントを使うことが推奨される
    - https://www.ryuzee.com/contents/blog/4664

- デイリースクラム
  - 開発チームが毎日、同じ時間・場所で開催する
  - 一般的には以下の内容を共有する
    - 昨日やったこと
    - 今日やったこと
    - 困っていること
  - 進捗が良くない場合など、別途スプリントの再計画を見直す場合もある

- スプリントレビュー
  - 実際に成果物を見せて、意見をもらう貴重な場
  - スクラムチーム以外の参加者はプロダクトオーナーが招待する
  - 開発チームはデモを見せながら質問に答える
  - うまく行ったこと、発生した問題やその解決法についても説明する
  - プロダクトオーナーは成果物を精査し、更に必要なことがあればバックログに追加する
  - スクラムマスターは全体的な支援を行う

- スプリントレトロスペクティブ
  - スプリントの振り返り
  - 人・関係・プロセス・ツールの観点から今回のスプリントを検査
  - うまくいった項目や今後の改善が必要な項目を特定・整理
  - スクラムチームの作業の改善実施計画を作成
  - KPT(Keep/Problem/Try)というような振り返り手法を使ってやることが多い


# 参考にさせていただきました

- https://www.slideshare.net/papanda/ss-79465986
- https://medium.com/agile-hiyoko/%E7%B5%90%E5%B1%80%E3%82%B9%E3%82%AF%E3%83%A9%E3%83%A0%E3%81%A3%E3%81%A6%E3%81%AA%E3%82%93%E3%81%AA%E3%81%AE-%E6%97%A5%E6%9C%AC%E3%81%AE%E3%83%91%E3%82%A4%E3%82%AA%E3%83%8B%E3%82%A2%E3%81%8B%E3%82%89%E5%AD%A6%E3%81%B6%E3%82%A2%E3%82%B8%E3%83%A3%E3%82%A4%E3%83%AB%E3%81%AE%E6%AD%B4%E5%8F%B2-f59da5bae93 
- https://blog.engineer.adways.net/entry/2017/08/04/150000
