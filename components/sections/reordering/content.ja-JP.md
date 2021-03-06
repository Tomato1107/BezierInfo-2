# 曲線の次数下げと次数上げ

ベジエ曲線のおもしろい性質のひとつに、「*n*次の曲線は常に、*n+1*次の曲線で完璧に表すことができる」というものがあります。このとき、制御点は新しいものになります。

たとえば3点で定義される曲線があるとき、これを正確に再現するような、4点で定義される曲線を作ることができます。始点と終点はそのままにして、「1/3 始点 + 2/3 制御点」と「2/3 制御点 + 1/3 終点」を新たな2つの制御点に選べば、元の曲線と正確に一致する曲線が得られます。異なっているのは、2次ではなく3次の曲線だという点だけです。

*n*次の曲線を*n+1*次の曲線へと次数上げするための一般の規則は、次のようになります（始点と終点の重みは、元の曲線のものと変わらないことがわかります）。

\[
  Bézier(k,t) = \sum_{i=0}^{k}
                \underset{二項係数部分の項}{\underbrace{\binom{k}{i}}}
                \cdot\
                \underset{多項式部分の項}{\underbrace{(1-t)^{k-i} \cdot t^{i}}}
                \ \cdot \
                \underset{新しい重み}{\underbrace{\left ( \frac{(k-i) \cdot w_i + i \cdot w_{i-1}}{k} \right )}}
  \qquad ただし\ k = n+1。また\ i = 0\ のとき\ w_{i-1}=0
\]

しかし同時にこの規則から、*n*次の曲線を*n-1*次の曲線へと次数下げすることは、一般には**不可能**だという結論も得られます。なぜなら、制御点をきれいに「引き離す」ことができないからです。試してみたところで、得られる曲線は元と同じにはなりません。それどころか、まったくの別物に見えるかもしれません。

下の図では（半分）ランダムな曲線に対して、この規則を試してみることができます。図を選択して上下キーを押すと、次数上げや次数下げができます。

<Graphic title={this.state.order + "次のベジエ曲線"} setup={this.setup} draw={this.draw} onKeyDown={this.props.onKeyDown} />

[SirVer's Castle](http://www.sirver.net/blog/2011/08/23/degree-reduction-of-bezier-curves)には、最適な次元削減で必要になる行列について（数学的ですが）良い解説があります。時間があれば、これを直接この記事の中で説明したいところです。
