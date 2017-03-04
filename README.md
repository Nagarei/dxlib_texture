# dxlib_texture

Siv3Dを参考にしてDxLibで画像クラスを作る

#目指すもの
```cpp

dxle::texture2d texture{"Image.png"};

// テクスチャを左上座標(20,20)に描画
texture.draw(posLT({20, 20}), false);

// テクスチャ内のピクセル (260, 100) から 幅 200, 高さ 220 の範囲を
// 描画
texture.cut(dxle::pointi{260, 100},dxle::sizei{200,220}).draw(posLT({20, 20}), false);

//↓複雑な動作は組み合わせで表現

// テクスチャ内のピクセル (260, 100) から 幅 200, 高さ 220 の範囲を
// 左右反転して
// 位置 (350, 200) に描く
texture.cut({260, 100}, {200, 220}).mirror().draw(posLT({350, 200}), false);

//↓組み合わせの順番は問わない
//(実装は遅延評価を使ってオーバーヘッドを減らす)

//上の例に同じ
texture.mirror().cut({260, 100}, {200, 220}).draw(posLT({350, 200}), false);

//描画だけでなく複製も同じ手法で行う
//（cut以外は重そうだな...）

// テクスチャ内のピクセル (260, 100) から 幅 200, 高さ 220 の範囲を
// 切り出し、新たなテクスチャを生成
auto new_texture = texture.cut({260, 100}, {200, 220}).clone();

//DxLib::LoadDivGraphに対応する機能（名前を思いつかない）

//引数は(画像,総分割数,分割数,一つのサイズ)
//(引数減らせないかな...)
dxle::texture_pack texture_pack1("animation.png", 8, dxle::sizei{3,3}, dxle::sizei{50,50});
dxle::texture_pack texture_pack2(texture, 8, dxle::sizei{3,3}, dxle::sizei{50,50});
auto texture_pack3 = texture.divide(8, dxle::sizei{3,3}, dxle::sizei{50,50});

//インターフェースあんまり生かせないな...
texture_pack1[0].draw(posLT({20, 20}), false);

```

# License

Boost Software License - Version 1.0
