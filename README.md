# r150works.com ランディングページ

R150works 合同会社 公式 LP（Stripe 審査用、既存 r150works.com に配置）。

## 構成

```
r150works-lp/
├── index.html          # メイン LP（会社紹介 + 3プロダクト + 連絡先）
├── tokushoho.html      # 特定商取引法に基づく表記
├── terms.html          # 利用規約（決済条項中心、他章は要弁護士レビュー）
├── privacy.html        # プライバシーポリシー（Stripe 委託条項中心）
├── assets/
│   └── style.css       # 共通スタイル
└── README.md           # このファイル
```

## オーナーが置換する項目（公開前必須）

各 HTML ファイル内の `[REPLACE_*]` プレースホルダーを実値に置換してください:

| プレースホルダー | 置換値の例 | 出現ファイル |
|---|---|---|
| `[REPLACE_REPRESENTATIVE_NAME]` | 代表者氏名（鍋田 修司）| 全ファイル |
| `[REPLACE_POSTAL_CODE]` | 郵便番号（例: 425-0000）| index, tokushoho |
| `[REPLACE_ADDRESS]` | 所在地（番地まで、例: 静岡県焼津市◯◯1-2-3）| index, tokushoho |
| `[REPLACE_PHONE]` | 電話番号（例: 054-XXX-XXXX、なければ「請求により遅滞なく開示」のまま）| tokushoho |
| `[REPLACE_SUPPORT_EMAIL]` | 公開窓口メール（info@r150works.com に統一、2026-05-30 方針）| 全ファイル |
| `[REPLACE_PRIVACY_OFFICER_NAME]` | 個人情報保護管理者氏名（通常は代表者と同一）| privacy |
| `[REPLACE_PRIVACY_OFFICER_EMAIL]` | 個人情報保護管理者メール | privacy |
| `[REPLACE_LAST_UPDATED]` | 最終更新日（例: 2026年5月31日）| 全ファイル |
| `[REPLACE_CORPORATE_NUMBER]` | 法人番号13桁 | index |

## デプロイ手順

### Netlify 推奨（無料、HTTPS 自動）

1. Netlify アカウントでこのディレクトリをドラッグ&ドロップ or GitHub 連携
2. Netlify の Custom Domain 設定で **r150works.com** を追加
3. お名前.com のドメイン管理画面で Netlify の DNS（4本の NS or CNAME）を設定
4. SSL 証明書（Let's Encrypt）が自動発行されるまで待機（5-30分）
5. https://r150works.com で公開確認

### Vercel でも可

同様の手順、`vercel --prod` でデプロイ。

## Stripe 申請時のポイント

申請時に Stripe Dashboard で以下 URL を入力します（オーナーの申請が途中まで進行中、ホームページ欄で中断 = ここから再開）:

| 項目 | URL |
|---|---|
| 事業 URL | https://r150works.com/ |
| 特商法表記 | https://r150works.com/tokushoho.html |
| 利用規約 | https://r150works.com/terms.html |
| プライバシーポリシー | https://r150works.com/privacy.html |
| 商品ページ（KaigoLog）| https://kaigolog.net/（公開準備中） |
| 商品ページ（ShienLog）| https://shienlog.com/（公開準備中） |

※ 2026-06-02 方針転換: LP を **KaigoLog ＋ ShienLog の2本立て**に再編（AnpiLog は FC撤退期の対外展開凍結のため LP から除外、ClinicLog は当面除外）。詳細 → `ai-workspace/50_決定事項ログ.md`（2026-06-02）。

### MCC（業種コード）の選択

- **R150works 全体**: 5734 - Computer Software Stores（低リスク）
- KaigoLog 個別: 8099 - Health Practitioners（中リスク、後で Price 追加時に注意）
- ShienLog 個別: 5734 - Computer Software Stores ベース（障害児通所支援向け SaaS）。要配慮個人情報＋未成年（保護者同意）を扱う旨は申請時に説明、医療行為・診療には非該当を明示

詳細: `ai-workspace/34_決済システム.md` §ハイリスク業種対策

## ドメイン関連メモ（2026-05-26 確定）

- **r150works.com**: 既存取得済（お名前.com）、本 LP の公開先
- **kaigolog.net**: KaigoLog 公式（今週中取得予定）。carelog.jp / .com / .net / .co.jp / .io は全 NG 確認済
- **r150works.jp**: 不要（r150works.com で代替）
- 長期戦略: SinqRelations 設立後に carelog.co.jp 取得チャレンジ、取れれば KaigoLog 本命に昇格

## 公開前チェックリスト

- [ ] すべての `[REPLACE_*]` を実値に置換
- [ ] `[REPLACE_LAST_UPDATED]` を公開日に設定
- [ ] `index.html` の3プロダクト紹介の状態が最新（KaigoLog 開発状況等）
- [ ] `tokushoho.html` の料金が `ai-workspace/30_ビジネス戦略.md` の最新と一致
- [ ] `privacy.html` の個人情報保護管理者氏名・連絡先を設定
- [ ] `terms.html` の決済以外の章を弁護士レビュー（または最小限の確認）
- [ ] kaigolog.net ドメインの取得・DNS 設定完了（または「公開準備中」のままでも可）
- [ ] HTTPS 化確認（r150works.com）

## 関連ファイル

- `ai-workspace/34_決済システム.md` — Stripe 申請の全体スケジュール
- `ai-workspace/40_オーナーToDo.md` — 今週のタスク（5/26-5/31）
- `ai-workspace/42_ドメイン・サブスク管理.md` — ドメイン取得状況
- `claude-code/docs/legal-templates/` — 流用元の3テンプレ
- `claude-code/docs/stripe-application-checklist.md` — Stripe 申請の具体的手順

## 改版履歴

- 2026-05-26: 初版作成（Claude）。3プロダクト構成 + Stripe 審査要件を満たす最小構成
- 2026-05-26（同日更新）: r150works.jp → **r150works.com**（既存ドメイン活用）、carelog.jp → **kaigolog.net**（carelog 系全 NG 確認）に統一
