# KyoshinShindoColorMap
強震モニタのリアルタイム震度での各地点の色を震度に変換するテーブルです。  
テーブルって書いてるくせにMapになってるのは仕様です。

## 解説
強震モニタのリアルタイム震度では、震度0.1刻みで-3から6.9まで合計100段階で色が変化します。(未だ確定しているわけではないので、間違っている可能性もあります。)

その段階を網羅してしまおうということでこの変換テーブルが作成されました。  
防災アプリケーションの今後の発展のために公開しています。

強震モニタの画像での色の取得座標に関しては、[KyoshinShindoPlaceEditor](https://github.com/ingen084/KyoshinShindoPlaceEditor)もご利用ください。

## CSVファイルの仕様
`震度,R値,G値,B値` となっています。

## 他シリアライズ済みファイルについて
CSVの他に、Protobuf(拡張子は.pbf)、MessagePack-CSharp(拡張子は.mp)、Jsonを添付しています。  
.protoファイルは書き方がわからないので適当になっています。  
間違ってはいないはずですが実際の内容は.protoファイルに記述している内容を繰り返したものになっています。

C#でのクラスは以下のようになっています。
```cs
[DataContract, MessagePackObject, ProtoContract]
public class KyoshinShindoColor
{
	[DataMember, Key(0), ProtoMember(1, IsRequired = true)]
	public float Intensity { get; set; }
	[DataMember, Key(1), ProtoMember(2, IsRequired = true)]
	public byte R { get; set; }
	[DataMember, Key(2), ProtoMember(3, IsRequired = true)]
	public byte G { get; set; }
	[DataMember, Key(3), ProtoMember(4, IsRequired = true)]
	public byte B { get; set; }
}
```

## ライセンス
作成: [ingen084](http://twitter.com/ingen084)  
協力: [こんぽ](https://twitter.com/compo031)さん

使用する際の報告は不要ですが(していただけると喜びます)、クレジットの表記はなるべくしていただけると助かります。(モチベがだいぶ上がるので)

## データ/値が間違っている or もっと細かいのあるよ
Issueを立てていただくか、プルリクを送っていただくと対処します。

## 注意事項
震度6.9に関しては概算値から割り出しています。  
このデータの震度は必ずしも正しいとは限りません。  
また、このデータの利用はすべて自己責任で行ってください。