# Knowledge-of-system-management
linuxなどで構成したシステムを管理する際の心得

## はじめに
Raspberry piでシステムを構築、運用していて体験したことのまとめです

## 心得
***1. 作成したシステムは必ずバックアップを取っておくこと***
  - 理由   
    これは、誰でもわかるとおりシステムがハードやソフト的に破損した場合、復旧するために行うためである。
    また、システムをアップグレードして正常に動作しないとき、すぐにダウングレードしてステーブルの状態に戻す場合のためである。
  - 苦い思い出   
    カーネルやパッケージをアップグレードしたときに、バグのあるパッケージがあったためシステムが正常に動作しなかった。   
    しかも、もとのシステムをバックアップしていなかったため、システムを一から再構築しなければなかった
    
***2. カーネルやパッケージ、OSのアップグレードは定期的ではなく数カ月に一回のみで良い（ただし、緊急性の高いセキュリティアップグレードの場合を除く)***   
  
  **決して新機能や新デザインの誘惑で行ってはならない。システムは安定性が第一である**
  - 理由   
    カーネルやパッケージ、OSのアップグレードは,配信側で検証はされているが、ときにバグが混入している場合がある。また、アップグードしてすぐに不具合の出ないバグもある。   
    定期的にアップグレードしているとどの段階でバグのあるアップグレードをしたかわからなくなるため   
    ただし、sudoやstlなどのセキュリティに関する緊急アップグレードはすぐに行うこと(必ず行う前にバックアップは取っておくこと)
  - 苦い思い出   
    突然、Sambaサーバーへのアクセスが不安定になり、おまけにネットワークプレイヤーのメンテナンスをしていたこともあり、どのシステムがどの段階でで障害が起こっているのかがわからなくなった    
    挙句には、すべてのシステムをステーブルバックアップに戻す羽目になった。
   
***3. バックアップするシステムはバージョン管理を行う***
  - 理由   
  いつ、どのような変更を行ったバックアップかを明確化するため
  ステーブルバックアップを管理するため
  
***4. システムの構築する際に、構築した手順をドキュメントにしておくと良い**** 
  - 理由   
    システムをリニューアルしたり、不具合の切り分けをしたりする際にわかりやすいから
    また、設定を書いておくと後々改善したり修正したりしやすい
   
***5. システム側で設定をエクスポートできるなら使ったほうが良い***
  - 理由   
    使用していてこまめに設定が変わるシステム(Piholeのブロックリストやvolumioのプレイリストなど)は、以前のシステムバックアップに戻した場合、バックアップしたときの設定しか復元できないため。
    システムバックアップとは別に行っておくと、以前のバージョンに戻した後から設定ファイルをインポートすれば使用していた最新の設定に復元することができる。
    
***6. バクレポートを作成する***
  - 理由   
    発見したバグや対処したバグの詳細をレポートにしておくとシステムの再構築する際にスムーズに行うことができる。
