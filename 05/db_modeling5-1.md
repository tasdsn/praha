Q.1000文字程度の本文を記入して保存できる

A.articles.contentに入れる

=========================

Q.記事を更新すると履歴が保存される

A.article_historiesに履歴を保存する

=========================

Q.特定の記事の履歴を一覧表示できる

A.article_histories.article_idで特定の記事の一覧を取得

==========================

Q.履歴を選択して過去の記事状態に戻す事が可能
A.article_historiesから選択し、articlesを更新する

==========================

Q.最新状態の記事を一覧表示できる
A.articlesにあるものが最新の状態にしておく過去記事に戻した場合にも保持したいのであれば、
article_historiesのupdated_atが最新のものを表示する