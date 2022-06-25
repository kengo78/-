# Transformerとは
## Transformerの構成要素
- Source-Target-Attention
2つの系列データ(入力と出力)における時点間毎の関係性を表現する。
- Self-Attention
1つの系列データ内での時点間毎の関係性を表現する
- Multi-head Attention
Attention構造を並列に組み合わせる。これにより同時に複数のパターンの関係性を学習・認識することができ、豊富な情報を持つコンテ期す津込みベクトルを表現する。
- Positional Encoding
系列データにおける順序情報を表現
- Position-wise Feedforward Network
系列データの時点毎に共通の重みを持つFeedforword Networkである
## Transformerの特徴
- 計算速度が速い(大量のデータを学習できる)
Self-Attentionでは依存性がないため、並列計算も可能なので高速
- 広範囲の依存関係をもとに高品質なコンテキスト込みベクトルを表現できる
Self-AttentionやSource-Target-Attentionでは時点間毎の関係を行列表現するので広範囲な依存関係をうまくとらえられつつ、かつMulti-head Attentionにより高い表現力で高品質なコンテキスト込みベクトルを取得できる。
