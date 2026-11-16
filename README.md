# 負担バトル｜男と女、どっちの負担が大きい？

Xで表示回数100万を超えた「男の方が負担が大きい」「女の方が負担が大きい」系ポストを集め、AIが主張の向きを判定し、いいね数の合計でバトル形式に可視化する静的サイト。

- `index.html` … サイト本体（HTML/CSS/JSのみ、ビルド不要）
- `posts.json` … 表示データ（`data/posts.tsv` から生成）
- `data/posts.tsv` … 収集データ（side: M=男の負担派 / F=女の負担派）

データ更新：`data/posts.tsv` を編集して以下で `posts.json` を再生成。

```bash
python3 -c "import csv,json;r=list(csv.DictReader(open('data/posts.tsv'),delimiter='\t'));json.dump({'collectedAt':'YYYY-MM-DD','posts':[{'side':x['side'],'url':'https://x.com/'+x['path'],'handle':'@'+x['path'].split('/')[0],'name':x['name'],'date':x['date'],'likes':int(x['likes']),'reposts':int(x['reposts']),'replies':int(x['replies']),'views':int(x['views']),'text':x['text']} for x in r]},open('posts.json','w'),ensure_ascii=False,indent=0)"
```

Vercel に GitHub 連携でデプロイ（Framework: Other、ビルドコマンドなし）。
