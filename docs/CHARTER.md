# Z Charter / Z憲章
Version: 0.1 (draft) | Established: 2026-10-15 | Status: Guiding principles (implementation not yet begun)

## Vision
**Z: The Last Programming Language / 最後のプログラミング言語** は、AIがプログラムを構築し、人間がその意図・根拠・リスクを理解して検証・承認することを第一目的とする言語構想である。

「最後」は到達目標・哲学を表すもので、他の言語の消滅や完全な正しさを保証する宣言ではない。

### Central formula
**Z = Intent + Implementation + Evidence**

- **Intent（意図）**: 何を達成すべきか。事前・事後条件、不変条件、権限、例外、未確定事項、承認者。
- **Implementation（実装）**: AIが生成する決定的・機械実行可能な処理。人間による直接編集も排除しない。
- **Evidence（根拠）**: テスト結果、形式的証明、型検査、静的解析、状態遷移検査、依存環境、未検証事項、監査証跡。

これらを相互参照可能な第一級データとして保持する。同一であると見せかけない。自然言語での説明は証明ではない。

## Seven constitutional principles
1. **AI-first, human-verifiable**: AIが大量に構築でき、人間が判断に必要な情報を抽出できる設計を優先する。
2. **The spec is not the implementation**: 意図と実装は別物。AIによる推測は承認済みの要求に昇格しない。
3. **Independent verification**: AIの自己評価を証拠とみなさず、独立した決定的な検証器で確認する。
4. **Uncertainty is explicit**: 不明・仮定・矛盾・未検証を明示し、黙って埋めない。
5. **Effects and authority are explicit**: 外部通信、ファイル変更、DB更新、決済、削除等の副作用・権限を追跡する。
6. **Change means behavioral change**: コード行ではなく、要求・振る舞い・権限・根拠への影響で差分を説明する。
7. **Small trusted core, replaceable execution**: Zの意味論と検証条件を独立させ、実行バックエンドを交換可能にする。

## Design stance
- **独立核＋複合実行**: 言語意味論・ZIR（Z Intermediate Representation）・検証規則を独自定義し、初期実行系は既存の環境やツールを活用する。
- **Structured-first**: 原本は型付き構造情報。人間向けソース・日本語仕様ビュー・AI向けAPIは、その投影（view）として扱う。
- **Proof is scoped**: 数学的証明、テスト、レビュー、推測を混同せず、保証の前提と適用範囲を表示する。
- **Traceability**: 要求ID→実装ノード→検証根拠→成果物ハッシュ→承認を結ぶ。
- **Security by construction**: 無許可の副作用、仕様の無断確定、実行可能な未検証成果物を扱う際は失敗側に倒す。
- **Portable, not prematurely universal**: 万能VMを最初から作らず、最小実行系と標準テストセットから進める。

## Non-goals at this stage
- あらゆるプログラムの正しさの完全自動証明。
- 自然言語の曖昧な要求から「本当の意図」を自動推定し確定すること。
- Python等の既存エコシステムの全面置換を初期段階で達成すること。
- 未承認の処理をAIが独断で本番に適用すること。

## Project governance
- この憲章は設計判断の評価基準。改訂は理由・変更履歴・要求への影響を記録する。
- 仕様変更を実装修正に紛れ込ませない。人間の承認が必要な条件は明示する。
- 公開リポジトリで議論可能とする。著作権・ライセンスは別途決定する（公開＝無条件利用許諾ではない）。
- 「Z」は構想上の呼称。既存のZ notationとの名称混同や商標等は正式普及前に確認する。
