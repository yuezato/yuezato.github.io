{% raw %}
$$
   \def\dc{{\rm DC}}
   \def\bold#1{{\bf #1}}
   \def\inode{{{\sf x}_{in}}}
   \def\onode{{{\sf x}_{out}}}
   \def\source{{\sf S}}
$$
{% endraw %}   

# Network Coding for Distributed Storage Systems読む

## 記法
あくまでも論文で用いられている記法で、
グラフ理論及びネットワーク符号理論で一般的なものかどうかは
気にしていないことに注意されたい。
+ $\mathcal{G}$: information flow graph
+ $\mathcal{M}$: file size
+ $n \in \mathbb{N}$: アクティブノード数
+ $\alpha \in \mathbb{R}_{\geq 0}$: 各ノードでのデータサイズ
+ $d$: repairする際に通信するノード数 $(d \leq n-1)$
+ $\beta \in \mathbb{R}_{\geq 0}$: repairする際に各ノードからもらうデータサイズ
+ $\gamma = d \cdot \beta$: repairする際に必要な総データサイズ

## Information Flow Graph
Information flow graph(以下IFGと書くことにする)とは
+ Directed Acyclic Graphで
+ 特に単一の始点 $S$ を持ち
+ 対になるストレージノード $\inode^i$ と $\onode^i$ を持ち
+ 複数の終点 $\dc_1, \dc_2, \ldots$ を持つ。
    + この論文では終点は単一だと思うので $\dc$ とだけ書く。

辺には正の実数の重みがついており、繋ぎ方と併せて直感的な意味は以下の通り
+ $S \xrightarrow{\infty} \inode^i$: 始点から $\infty$ ストレージノードへの重みは $\infty$ のみで、これは最小カットを考えるための便宜的なもの
+ $\onode^i \xrightarrow{\infty} \dc$: 同様
+ $\inode^i \xrightarrow{\alpha} \onode^i$: 直感的にはノード $i$ の蓄えているデータ量
+ $\onode^i \xrightarrow{\beta} \inode^j (i \neq j)$: 直感的には、ノード$j$をrepairする際に、ノード $i$ からノード $j$ へ送るデータ量

## 最小カット
[最小カット最大フローの記事](./mincutmaxflow)参考のこと。

## 補題1
グラフ $\mathcal{G}$ 中の
始点 $S$ から データコレクター $\dc$ への最小カットは
$\mathcal{M}$ 以上でなければならない。

\[
C(\source; \dc) \geq \mathcal{M}
\]

---
<b>証明.</b>
カットセット一般の意味は、データのreconstructに使える情報量である。
従って、最小カットセットは再構成に利用できる最小の情報量を示していることになる。最小カットセット値は起こりうる最も厳しい条件で情報を再構成する状況を考えているのがこの補題である。

最小フローを考えるよりも最大流を考えた方がイメージしやすい気もする。

注意:
この論文 https://arxiv.org/pdf/1301.1549.pdf によると
$k$個のノードが $\dc$ に $\infty$ で接続されているという条件が
定義として加えられている。

$\dc$ の役割は元のデータを復元することにあるので、repairだけでなくreconstrucの面倒をみるところまで考えなくてはならない。

+ 圧縮アルゴリズムが途中で使われれば、最小カット以下でも再構成が可能ではないかという疑問に答える必要がある
+ 線形変換でやる場合に全ノードからrepairしないとrobustでないことの説明を与える。
