<div style="display:none">
{% raw %}
$$
  \def\galf{{\textit{GF}}}
  \def\set#1{{\{#1\}}}
  \def\finf{{\mathbb{F}}}
  \def\card#1{{|#1|}}
$$
{% endraw %}
</div>

有限体について書きます。

# 一般の体に関する性質

以下は有限体に限らない一般の体に関する性質である:
+ $F$を体とし、$F[X]$を1変数多項式環とする。
+ $F[X]$の任意の多項式$f(X)$について分解体が存在する。
    + 分解体とは、$F$の拡大体$E$で以下を満たすもののうち最小のもの

    $$
        f(X) = c(X - \alpha_1)(X - \alpha_2) \cdots (X - \alpha_n)
        \qquad (c \in F, \alpha_i \in E)
    $$

## 体の標数
体$F$について、以下のような正の整数$n \in \mathbb{N}, n > 0$が存在すれば、そのうちで**最小のもの**を$F$の標数（characteristic）と呼ぶ

$$
\forall x \in F. nx = 0.
$$

そのような$n$がない場合は$F$の標数は0とする。例えば有理数体$\mathbb{Q}$や実数体$\mathbb{R}$の標数は0である。

### 有限体の標数は素数
一方で有限体$G$の標数は非零かつ素数であることが示せる。

まず$G$の標数が非零であることを示そう。
+ $G$の単位元$e$を用いて列 $e, 2e, 3e, \ldots$を考える。
+ $G$は有限体であるから鳩ノ巣原理でこの列の途中で$e, \ldots, k e, \ldots, m e (= k e), \ldots$となる$k < m$が出現する。
+ $(m - k)e = 0$が成立する。
+ 任意の元$g \in G$について$(m - k)g = (m - k)eg = 0g = 0$が成立する。
+ よって標数は1以上$m - k$以下の何らかの値になる。
    + $m - k$は標数の上界しか与えないことに注意

次に$G$の非零な標数$p$が素数であることを示す。
+ 背理法を用いる。合成数なので$p = a b$という$1 < a \leq b < p$なる因数を持つ。
+ $0 = pe = (abe) = (ae)(be)$
+ 体で$xy = 0$ならば$x$か$y$が0になるから$ae = 0$または$be = 0$でなければならない。
+ $ae = 0$であれば任意の$g \in G$について$ag = 0$となり$p$の最小性に反するし、$be = 0$であっても$p$の最小性に反するので、$p$はやはり素数でなければならない。

### 有限体の標数 = 素体の要素数
体$F$に含まれる最小の体を素体と呼ぶ。
$F$の部分体$A, B \subseteq L$の共通部分$A \cap B$は再び体をなすことを利用すれば$K$の存在は明らかである。

有限体$G$は上でみたように標数$p$が素数であるが、
素体$K$の要素数がこれと一致することが示せる。
+ 次で定める部分体が素体となることを示せば良い:

    $$
      Q(G) = \set{ 0 \cdot 1_G,\ 1 \cdot 1_G,\ 2 \cdot 1_G, \ldots, (p-1) \cdot 1_G }
    $$

    + $p$が素数なので$\mathbb{F}_p$との明らかな全単射から体にできる。
+ $K$は素体なので$K \subseteq Q(G)$.
+ $K \supseteq Q(G)$を示す。
+ $G$の任意の部分体は$0_G, 1_G$を含まなくてはならない。
+ $G$の標数が$p$であるから$0 \leq i < j \leq p - 1$について$i \cdot 1_G \neq j \cdot 1_G$となり$G$の部分体はこれらも全て含んでいなければならない。
+ 従って$K \supseteq Q(G)$でなければならない。

## 拡大体とベクトル空間
体$L$と体$K$について$K \subset L$が成立するとき、$L$を$K$の拡大体という。

$L$は$K$-ベクトル空間$V$としてもみることができる。
+ $V$の要素たちは、構造を忘れて集合としてみた$L$
+ $v_1, v_2 \in V$について加算は$v_1 + v_2$
+ 係数$k \in K$とベクトル$v \in V$のスカラー積は$k v \in V$
このように定義した時に$V$はベクトル空間になる。

このような$V$を定義すると次のようなことが示せる。
+ 体$F$を有限体とし、$K$を$F$の部分体とする。
+ $F$は$K$-ベクトル空間としてみることができるため、
ベクトル空間一般の議論から$n$個の基底をとることができる。
+ このような$n$を$[L : F]$とも書く。
+ $F$は$n$個の基底と係数体$K$によって張られるので、
$|F| = |K|^n$ が成立する。

ベクトル空間とみなす議論により次がいえる。

### 有限体$F$の要素数は素数$p$の冪乗$p^n$
$K$を$F$の素体とすると、$|K|$は$F$の標数と一致し素数になることから

$$
\text{$F$が有限体} \implies |F| = p^n.
$$

# 素数冪乗$p^n$要素の有限体を作る
有限体を構成していく上で重要な性質を示していく。

## 有限体の乗法群は巡回群をなす
有限体$F$の積に関する群$F^\star = F \setminus \set{ 0_F }$は巡回群である。
+ $F^{\star}$は$F$の積が可換なので有限アーベル群である
+ [有限アーベル群の構造定理](https://ja.wikipedia.org/wiki/%E6%9C%89%E9%99%90%E3%82%A2%E3%83%BC%E3%83%99%E3%83%AB%E7%BE%A4%E3%81%AE%E6%A7%8B%E9%80%A0%E5%AE%9A%E7%90%86)を適用して以下のように直積分解可能である:
    $$F^{\star} \simeq C_1 \times C_2 \times \cdots \times C_n$$
+ 特に $\card{C_i}$ は $\card{C_{i+1}}$ を割り切るし
  $\card{F^{\star}} = \prod \card{C_i}$
+ $k = \card{C_n}$ とすると、任意の $x \in F^{\star}$ について
  $x^k = 1_F$ で $k \leq \card{F^{\star}}$

ところで $x^k - 1_F$ の根の個数は因数定理から高々 $k$ なので $\card{F^{\star}} \leq k$

結局 $F_{\star} \simeq \mathbb{Z} / k\mathbb{Z}$ という巡回群であることに他ならない。

この系として、有限体$F$の要素数を$q = \card{F}$とすると

$$
\forall x \in F. x^q = x
$$

が成立する。
+ 零元$0_F$については明らか
+ それ以外の要素$x$については$F^{\star}$が巡回群なので$x^{q-1} = 1_F$が成立するため直ちに$x^q = x$となる。

## 有限体を分解体としてみる
有限体$F$の要素数を$q$とし$K$を$F$の部分体とする。
このとき、$X^q - X \in K[X]$は

$$
X^q - X = \prod_{r \in F} (X - r)
$$

として線形分解できる。

+ 既にみたように、任意の$x \in F$について$x^q - x = 0$であるから
因数定理により$X^q - X = c \prod_{r \in F}(X - r)$
+ 主係数の比較から$c = 1$なので証明終了

## $\galf(p^n)$が存在することの証明
$p$は勿論素数である。
$\mathbb{F}_p$は$p$が素数であるから構成可能である。

$q = p^n$とおいて、$X^q - X \in \mathbb{F}_p[X]$を考える。
この単項式に関する分解体を$F$とする。

+ $F$の標数は$p$である。
+ 従って任意の自然数$m$と$a, b \in F$について$(a + b)^{p^m} = a^{p^m} + b^{p^m}$
+ 特に$(a + b)^q = a^q + b^q$

$X^q - X$を$F$で微分すると$q X^{q-1} - 1$となり、$\mathbb{F}_p \subseteq F$では$q = 0$なので$-1$となる。これと$X^q - X$は共通根がないので$X^q - X$に重根が存在しないことになり、相異なる$q$個の根$r_1, r_2, \ldots, r_q$が存在する。

実はこのとき、$\set{ r_1, r_2, \ldots, r_q } \subseteq F$が体になる:
+ $0^q - 0 = 0$なので$0_F$が含まれている。$1_F$も同様。
+ $(r_i r_j)^q - (r_i r_j)$は$r^q_k = r_k$から明らか。
+ $(r_i + r_j)^q - (r_i + r_j)$は$(r_i + r_j)^q = r^q_i + r^q_j$でかつ$r^q_i = r_i$なので明らか。
+ $(r^{-1}_i)^q = (r^q_i)^{-1} = r^{-1}_i$なので逆元も存在する。

したがって要素数$q = p^n$の体が存在することが分かった。

## $\galf(p^n)$が同型を除くと唯一である
$q = p^n$の有限体$F$が存在したとする。
$F$の標数が$p$であると言えるので$\mathbb{F}_p \subseteq F$である。
このとき、

$$
X^q - X \in \mathbb{F}_p[X] = \prod_{f \in F}(X - f)
$$

として分解できるし、特に$F = \mathbb{F}_p(F)$が成立しているわけなので$F$は分解体になっている。

別の有限体$F'$も$X^q - X \in \mathbb{F}_p[X]$の分解体であり、分解体は同型であることから証明が終わる。

# $\galf(p^n)$の具体的な構成

## 有限体の拡大
$\finf_q$の拡大体を$\finf_r$とする。

このとき、

$$
\exists \beta \in \finf_r. \finf_q(\beta) = \finf_r
$$

が成立する。

+ $\finf_r$の乗法群は巡回群であるので、$\alpha$を生成元とする。
    + 体論では原始元とも呼ぶ。
+ $\finf_q(\alpha) \subseteq \finf_r$であり
+ $\finf_q(\alpha)$は$\alpha, \alpha^2, \ldots$を全て含み$0$元も含むので$\finf_q(\alpha) = \finf_r$が成立する。

有限体の乗法群は巡回群にはなるが、非零要素が生成元になるわけではないことに注意したい。例えば$1$はそのような例で、とはいえ0でも1でもない場合の具体的な例があるか分かりません。

また、原始元を加えなくても拡大できる場合もあります。
例えば$\finf_3$を単純拡大して$\finf_9$を作る場合を考えます。
このとき、$\beta$を$\finf_3$上の既約多項式$x^2 + 1$の根とします。
$\beta^4 = 1$であるので、$\beta$は原始元になっていないことが分かります。

ところで$x^2 + 1$の既約多項式を使って$\finf_9$に拡大できる理由とは何なのでしょうか。
もしくは、単純な方法で作れる素数$p$に対する$\finf_p$から$\finf_{p^n}$を作るにはどうすれば良いか、ということを考えていきます。

素数$p$について$\finf_p$の拡大体が$\finf_{p^n}$:
+ $\finf_{p^n}$の標数は$p$であり、素体の要素数$p$となる
+ 素体であるということは部分体であることに他ならない。
+ $\finf_p$は要素数$p$の素体なので示せた。

上の話を合わせると$\finf_2$を拡大して$\finf_{2^n}$を作ることができると言えます。
一方で、$\finf_3$は$\finf_{2^n}$の部分体ではないので$\finf_3$を拡大しても目的の有限体を構成することはできないので注意です。

## 既約多項式を用いた拡大
$\finf_{2}$を拡大して$\finf_{2^n}$を作りたい。

上の方法によれば$\finf_{2^n}$の原始元$\alpha$を形式的に取り、
$\finf_2(\alpha)$を求めれば良いが、ここで大きな問題がある。
それは$\alpha^i, \alpha^j \in \finf_2(\alpha)$に対して
$\alpha^i + \alpha^j$をどのように入れれば良いかの指標が存在しないということである。

そこで原始元$\alpha$を根とする
$n$次の$\finf_{2}$を係数とする既約多項式を用いることで
この問題を回避しつつ$\finf_{2}$から$\finf_{2^n}$を構成できる。

次でみるようにそのような既約多項式は必ず存在することが示せ、
かつ$\finf_{2}$上の多項式が既約かどうかを調べる方が、
恐らく$2^n$要素上に総当り的に体を見つけようとする方が簡単である。

次数$n$の$\finf_{p}$既約多項式$f$が必ず存在し、なおかつ
$\finf_{p^n}$に$f$の根が存在するこを示す。

## 任意次数の既約多項式（特に原始多項式）の存在
ここでは
「有限体$\finf_p$と任意の$n \geq 1$について次数$n$の$\finf_p[X]$原始多項式が存在する」
という重要な定理を示す。

$f$が原始多項式(primitive polynomial)とは
+ 既約多項式であり、
+ その多項式の次数を$n$とすると
+ $\finf_{p^n}$上の原始元を根に持つ。

$\finf_{p}$の有限拡大$\finf_{p^n}$について$[\finf_{p^n} : \finf_{p}] = n$である。
このとき、$\finf_{p^n}$の原始元$\alpha$によって$\finf_{p}(\alpha) = \finf_{p^n}$が成立する。

$\alpha^{p^n} = \alpha$であるから、$\alpha^{p^n} - \alpha = 0$によって$\alpha$は$\finf_{p}$上で代数的である。

このとき（証明は一旦省くが多項式環とイデアルの理論を通して）
+ $\alpha$を根とする最小多項式$g$が存在する。
+ $g$は既約多項式でもある。

$g$の次数がちょうど$n$となることを証明する。

$\alpha^n, \alpha^{n-1}, \ldots, \alpha, 1$は$n+1$本のベクトルであり、$\finf_{p^n}$は$\finf_{p}$-ベクトル空間として見た時にその次元が$n$であるから一次従属でなければならず、

$$
c_n \alpha^n + c_{n-1} \alpha^{n-1} + \cdots + c_1 \alpha + c_0 = 0
$$

とする係数 $c_i \in \finf_{p}$ で何れかが非零なものが存在する。

もし$g$の次数が$n+1$以上であれば、$g$が最小多項式であることに反する。

従って$g$の次数は$n$以下でなければならない。

次に$n$本のベクトル$\set{ \alpha^{n-1}, \alpha^{n-2}, \ldots, \alpha, 1}$が基底になることを証明する。

$\alpha$は原始元であるから、任意の$v \in \finf_{p^n}$について

$$
v = f(\alpha)
$$

とするような$\finf_p[X]$多項式$f(X)$が存在する。
さて、体を係数とする多項式に関する除法定理により、各$f$を$g$で割ると

$$
f(X) = g(X)q(X) + r(X) \quad \text{deg}(r) < \text{deg}(g)
$$

を満たす$q$と$r$が一意に存在する。
さて、$g(\alpha) = 0$であったから$f(\alpha) = r(\alpha)$である。
これは$\finf_{p^n}$が$\alpha^{n-1}, \ldots, \alpha, 1$の線形結合で張ることができることに他ならない。

$n$次元ベクトル空間を$n$本のベクトル空間で張れる時には、それらは線形独立でなければならない。
もし線形従属であるならば$n-1$本のベクトル空間で全体を張れるが、これはそのベクトル空間が$n$次元であることに反する。

従って$\alpha^{n-1}, \ldots, \alpha, 1$の$n$本のベクトルが基底となることが証明できた。

## 既約多項式は必ず解を持つことの証明
上では与えられた次数に対応する原始多項式が存在することをみた。

ここでは「任意の」既約多項式が根を持つことを示す。

$\finf_{p}$上の$n$次既約多項式$f(X)$が$\finf_{p^n}$上に根を持つことを示す。これには

$$
 x^{p^n} - x = f(X)g(X)
$$

として割り切れることを示せば十分である。

$\alpha$を$f$の$\finf_q$上の分解体の根とする。
このとき$[\finf_q(\alpha) : \finf_q] = n$である。

分解体を取ってきたのは根を含ませる形で巨大にしておいて、
その根を取り出したかったから。
分解体がいつでも構成できることは証明しなければならないが、一般の体の理論の話なので一旦skipする。

$f$は最高次数係数で全体を割って単項式にできるが、
この時に$\alpha$の最小多項式になる。
係数で割っても既約性は変わらないので、互除法を使ってあげれば単項式化した後のものが$\alpha$の最小多項式になる。

$\finf_q(\alpha)$を$\finf_q$-ベクトル空間としてみる。
特に$\alpha^{n-1}, \ldots, \alpha, 1$の$n$本のベクトルに注目する。
$f$が$\alpha$の次数$n$の最小多項式なので、
$\alpha^{n-1}, \ldots, \alpha, 1$の線型結合で$0$を作ることができない。言い換えればこれらは線形独立である。

$\finf_q(\alpha)$は$\finf_q$と$\alpha$を含む最小の体である（定義そのもの）。

さて、以下の多項式環の部分集合

$$
\finf_{n-1}[\alpha] = \set{ f \in \finf[\alpha] : \text{deg}(f) \leq n-1}.
$$

は体になることが示せる。ただし
+ 乗算で次数の限界を超えないことは互除法の剰余項から示せる
+ 乗算の逆元が存在することは https://faculty.math.illinois.edu/~r-ash/Algebra/Chapter3.pdf の3.1.7参照
+ 多項式上のExtended Euclidean Algorithmを使う https://en.wikipedia.org/wiki/Extended_Euclidean_algorithm

よって$\finf_q(\alpha)$は$\alpha^{n-1}, \ldots, \alpha, 1$によって生成できる。

これらによって$\alpha^{n-1}, \ldots, \alpha, 1$は$\finf_q(\alpha)$の基底であり、最終的に
$[ \finf_q(\alpha) : \finf_q ] = n$ が示せた。

$\finf_q(\alpha)$は要素数が$q^n$であるから$\finf_q(\alpha) \simeq \finf_{q^n}$である。

## 既約多項式の解のさらなる特徴づけ

ここまでで以下のことが分かっている:
1. $n$次の$\finf_p$係数の既約多項式$f$が存在する。
2. $f$は$\finf_{p^n}$中に根$\alpha$を持つ。

ここでは$f$に相異なる$p^{n-1}$個の解があり、
しかもそれが一つの解の自乗形で与えられることを示す。

$\beta \in \finf_{p^n}$が$f(\beta) = 0$とする。
このとき、$f(\beta^p) = 0$となることを示す。

$f(X)$は次数$n$の多項式なので次のように表示することができる:

$$
f(X) = a_n X^n + \cdots + a_1 X + a_0 (a_i \in \finf_p)
$$

従って

$$
\begin{array}{lcl}
f(\beta^p) & = & a_n \beta^{pn} + \cdots + a_1 \beta^p + a_0 \\
& = & a^p_n \beta^{pn} + \cdots + a^p_1 \beta^p + a^p_0 \\
& = & (a_n \beta^n + \cdots + a_1 \beta + a_0)^p \\
& = & f(\beta)^p = 0.
\end{array}
$$

よって$\alpha, \alpha^p, \alpha^{p^2}, \ldots, \alpha^{p^{n-1}}$は全て$f$の根になる。

次にこれらが全て異なることを証明する。
+ もし$a^{p^j} = a^{p^k}$が成立したとする
+ 両辺に$q^{n-k}$をかけて

  $$
    \alpha^{p^{n-k+j}} = \alpha^{p^n} = \alpha
  $$

  + 最後の等式は$\alpha$が$\finf_{p^n}$の要素なので成立する
+ $g(X) = X^{p^{n-k+j}} - X$とすると$g(\alpha)$なので$f$は$g$を割り切る。
  + これは一応証明が必要
+ このときさらに$n$が$n-k+j$を割り切る。
  + これも証明が必要
+ いま$0 < n - k + j < n$であるから矛盾する。

## これらの系として
$f$を$\finf_{q}$の$n$次既約多項式とする。
$f$の分解体が$\finf_{q^n}$となる。

+ $f$は$q^m$の異なる解を持つため$\finf_{q^n}$でsplitしている
+ 分解体は$\finf_{q}(\alpha, \alpha^p, \alpha^{p^2}, \ldots, \alpha^{p^{n-1}})$であるが、
+ これは上でみた性質から$\finf_{q}(\alpha)$に等しく
+ $\finf_{q}(\alpha)$と$\finf_{q^n}$は既に見ているので示せた。
