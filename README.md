# public-api-schema
LAPRAS公開ページAPIの仕様書です。

## OpenAPI 定義
- [OpenAPI Specification file](openapi/openapi.yml)
- [OpenAPI Doc](https://lapras-inc.github.io/public-api-schema/)

## URL

```
GET https://lapras.com/public/<:share_id>.json
```

## Response

| key | type | description | example |
| --- | --- | --- | --- |
| name | string  | LAPRAS登録のユーザー名  | `"LAPRAS太郎"`  |
| description | string  | LAPRAS登録のユーザー概要 | `"LAPRAS株式会社のソフトウェアエンジニアです。"` |
| e_score | number | 技術力スコア | `3.4` |
| b_score | number  | ビジネス力スコア | `3.1` |
| i_score | number | 影響力スコア | `2.2` |
| qiita_articles | arrary | Qiita記事 | `[{"title": "hogehoge", "url": "https://qiita.com/hogehoge"}, "tags" ["foo"], "headlines": ["bar"], "stockers_count": 3, "updated_at": "020-07-26T08:10:11"]` |
| zenn_articles | array  | Zenn記事 | `[{"title": "hoge", "url": "https://zenn.dev/hoge", "tags": ["foo"], "posted_at": "2022-10-03T08:36:43"}]`  |
| blog_articles | array | ブログ記事 | `[{"title": "hoge", "url": "https://blog.com/hoge", "tags": ["foo"], "posted_at": "2022-10-03T08:36:43"}]` |
| note_articles | array | note記事 |  `[{"title": "hoge", "url": "https://note.com/hoge", "tags": ["foo"], like_count: 3, "published_at": "2022-10-03T08:36:43"}]`|
| speaker_deck_slides | array | SpeakerDeckスライド | ` [{"title": "hoge", "url": "https://speakerdeck.com/hoge", "tags": ["foo"], "description": "foo", "view_count": 1, "star_count": 2, "presentation_date": "2022-10-03T08:36:43"}]` |
| github_repositories | array | GitHubリポジトリ | `[{"id": 1, "title": "lapras-inc/foo", "url": "https://github.com/lapras-inc/foo", "is_oss": false, "is_fork": false, "is_owner": true, "description": "bar", "stargazers_count": 211, "stargazers_url": "https://github.com/lapras-inc/foo/stargazers", "forks": 22, "contributors_count": 14, "contributors_url": "https://github.com/lapras-inc/foo/graphs/contributors", "contributions": 313, "contributions_url": "https://github.com/klapras-inc/foo/g/commits?author=hoge", "language": "TypeScript", "languages": [{"name": "TypeScript", "bytes": 74882}]}]` |
| teratail_replies | array  | Teratailの回答 | `[{"title": "hoge", "url": "https://teratail.com/hoge", "is_best_answer": true, "tags": ["TypeScript"], "created_at": "2020-07-09T20:22:46"}]` |
| events | array | イベント参加 | `[{"title": "hoge", "url": "https://hoge.connpass.com/event/", "status": 1, "date": "2022-12-03T00:00:00", "is_presenter": false, "is_organizer": false}]` |
| activities | array  | Activity Log | `[{"title": "lapras-inc/hoge", "url": "https://github.com/lapras-inc/hoge", "date": "2022-12-10T11:25:37", "type": "github"}]`  |

## TypeScript Type

```typescript
type Response = {
  name: string; // LAPRAS登録のユーザー名
  description: string; // LAPRAS登録のbio,
  e_score: number; // 技術力スコア,
  b_score: number; // ビジネス力スコア,
  i_score: number; // 影響力スコア,
  qiita_articles: { // Qiita記事
    title: string;
    url: string;
    tags: string[];
    headlines: string[];
    stockers_count: number;
    updated_at: string;
  }[];
  zenn_articles: { // Zenn記事
    title: string;
    url: string;
    tags: string[];
    posted_at: string;
  }[];
  blog_articles: { // ブログ記事
    title: string;
    url: string;
    tags: string[];
    posted_at: string;
  }[];
  note_articles: { // note記事
    url: string;
    title: string;
    tags: string[];
    like_count: number;
    published_at: string;
  }[];
  speaker_deck_slides: { // speaker deckスライド
    title: string;
    description: string;
    url: string;
    star_count: number;
    view_count: number;
    presentation_date: string;
  }[];
  github_repositories: { // githubリポジトリ
    id: number;
    title: string;
    url: string;
    is_oss: boolean;
    is_fork: boolean;
    is_owner: true;
    description: string;
    stargazers_count: string;
    stargazers_url: string;
    forks: number;
    contributors_count: number;
    contributors_url: string;
    contributions: number;
    contributions_url: string;
    language: string;
    languages: {
      name: string;
      bytes: number;
    }[];
  }[];
  teratail_replies: { // teratail回答
    url: string;
    title: string;
    tags: string[];
    is_best_answer: boolean;
    created_at: string;
  }[];
  events: { // connpassイベント
    title: string;
    url: string;
    status: number;
    date: string;
    is_presenter: boolean;
    is_organizer: boolean;
  }[];
  activities: { // ActivityLog
    title: string;
    url: string;
    date: string;
    type:
      | "github"
      | "github_pr"
      | "speaker_deck"
      | "qiita"
      | "zenn"
      | "note"
      | "teratail"
      | "blog"
      | "connpass";
  }[];
};
```
