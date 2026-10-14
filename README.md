# Z — The Last Programming Language
**AI-first. Human-verifiable. Built by AI, understood and governed by humans.**

> **Z = Intent + Implementation + Evidence**  
> **Z = 意図 + 実装 + 検証根拠**

**日本語** | [GitHub discussions / Issues](https://github.com/zin1985/z-lang/issues)

## Vision / ビジョン
Z（ゼット）は、「AIがプログラムを構築し、人間が意図・影響・正しさの根拠・リスクを確認して承認する」ための新しいプログラミング言語・ツールチェーンの構想です。

既存言語がコード記述を中心に発展してきたのに対し、Zは **何をすべきか (Intent)**、**どう実行するか (Implementation)**、**何を根拠に妥当と判断するか (Evidence)** を、独立し相互参照できる第一級要素として扱います。

> AIにとって本当に便利な言語は、たくさんのコードを簡単に書ける言語ではなく、**間違ったコードを大量に書かずに済む言語**です。

「最後の言語」は設計上の理想であり、既存言語の廃止やあらゆるコードの完全な正しさを保証するものではありません。

## Core principles / 設計原則
1. **AI-first, human-verifiable**: AIが構築し、人間が判断する。
2. **Spec and implementation are separate**: AIが推測した要求は人間が承認するまで未確定。
3. **Independent evidence**: AIの説明だけでなく、独立検証器の機械的な結果を重視。
4. **Unknown is not success**: 未検証・失敗・不明・承認待ちを区別。
5. **Effects and permissions are explicit**: 外部通信、ファイル、DB更新等を追跡可能に。
6. **Review behavior, not just lines**: 人間には仕様変更・振る舞い・危険性の変化を提示。
7. **Independent core, hybrid execution**: 独自ZIRを中核に、実行バックエンドを交換可能にする。

## Documents / 初期資料
- [Z憲章（設計指針）](docs/CHARTER.md)
- [要求仕様一覧（機能32件・非機能10件）](docs/REQUIREMENTS.md)
- [初期アーキテクチャ](docs/ARCHITECTURE.md)
- [ADR-0001: 独立核＋複合実行](docs/ADR-0001.md)
- [ロードマップ M0-M4](docs/ROADMAP.md)
- [ZIR構想サンプル: 会員割引](examples/discount.z.json)

## Initial architecture / 初期構成
```text
Human intent / AI generation
             |
        ZIR (canonical)
       /      |       \
  Intent  Implementation  Evidence
       \      |       /
       Z Validator
             |
     Z Inspector (review)
             |
      Approval / policy
             |
  Pure interpreter -> pluggable backends (future)
```

## Current status / 現在の状態
**Concept / specification draft v0.1, 2026-10-15.**  
リポジトリ作成・憲章・要求一覧・構想設計まで。パーサー、コンパイラ、検証器、CLI、VMはまだ実装していません。サンプルJSONは**設計用の例であり実行可能なZプログラムではありません**。

**Next step:** ZIRの最小スキーマと参照インタプリタを作り、「正しい例と壊れた例」を検証器で識別する。

## Discussion / 参加について
現在は基本思想と初期要求に対する意見を歓迎します。特に意味論、証明の適用範囲、権限、仕様の未確定事項の扱いについての反論は歓迎です。

## Licensing and naming
このリポジトリは**公開**されていますが、ライセンスは**未決定**です。公開されていることは、コードや文章を自由に再配布・改変できるという意味ではありません。OSSライセンスと外部貢献ルールは別途決定予定です。

**Z** は仮のプロジェクト名です。既存の数理的仕様記述言語 **Z notation** と混同されないよう、正式名称・識別子は今後検討します。
