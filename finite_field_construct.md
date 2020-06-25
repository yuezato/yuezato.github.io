<div style="display:none">
{% raw %}
$$
  \def\modeq#1{\mathrel{{\equiv_{#1}}}}
  \def\modp#1{\mathop{{+}_{#1}}}
  \def\modm#1{\mathop{{\cdot}_{#1}}}
  \def\modd{\mathop{\%}}
  \def\tuple#1{\langle#1\rangle}
  \def\set#1{\{#1\}}
  \def\galf{{\mathit{GF}}}
$$
{% endraw %}
</div>

# $\galf(2^n)$ を具体的に構成する

## 素数$p$についての $\galf(p)$ の具体的な構成
素数$p$についての $\galf(p)$ の定義は以下の通り:
1. 要素は $\set{0, 1, 2, \ldots, p-1}$ で与えられる。
2. 加算 $x \modp{p} y$ の定義は自然数上でそれを行って$p$の剰余を取る。乗算 $\modm{p}$ も同様:

    $$
       \begin{aligned}
        x \modp{p} y = (x + y) \modd p, \\
        x \modm{p} y = (x * y) \modd p.
       \end{aligned}
    $$

    + ここで ${+}$ と $\cdot$ はそれぞれ自然数上の加算と乗算である。
4. 減算 $x \mathrel{ {-}_p } y$ は逆元との加算 $x \modp{p} (-y)$ で定める。
    + $y$に対する逆元$-y$は $y + -y \modeq{p} 0$ とするもの。
    + 下で証明するが、このようなものは唯一つに定まる。
5. 除算$x / y$は$x \modm{p} y^{-1}$で定める。
    + 逆元$y^{-1}$は$y \cdot y^{-1} \modeq{p} 1$となるものである。
    + 下で証明するが、$p$が素数であることから唯一存在することが保証される。

---

本当に体になるかどうか確認してみる。

次の一般の性質を使う

  $$
    x_1 \modeq{p} y_1, x_2 \modeq{p} y_2 \implies
    \begin{cases}
      x_1 + x_2 \modeq{p} y_1 + y_2, \\
      x_1 \cdot x_2 \modeq{p} y_1 \cdot y_2.
    \end{cases}
  $$

$a, b, c \in \galf(p)$とする。
加算の結合則 $(a \modp{p} b) \modp{p} c = a \modp{p} (b \modp{p} c)$.

$$
\begin{aligned}
(a \modp{p} b) \modp{p} c &= ((a + b) \modd p + c) \modd p \\
                          &= ((a + b) + c) \modd p \qquad & \because a + b \modd p \modeq{p} a + b \\
                          &= (a + (b + c)) \modd p & \text{自然数での結合則} \\
                          &= (a + (b + c) \modd p) \modd p \\
                          &= a \modp{p} (b \modp{p} c)
\end{aligned}
$$

乗算の結合則 $(a \modm{p} b) \modm{p} c = a \modm{p} (b \modm{p} c)$も同様である。


加算の可換性は

$$
a \modp{p} b = (a + b) \modd p = (b + a) \modd p = b \modp{p} a.
$$

乗算の可換性 $a \modm{p} b = b \modm{p} a$ も同様。

$0$が加算の単位元になることは

$$
a \modp{p} 0 = (a + 0) \modd p = a \modd p = a
$$

より明らか。$1$が乗算の単位元になることも同様である。

$a$の加算に関する逆元$-a$を次で定義する:

$$
a = 0 \implies -a=0,\quad
a \neq 0 \implies p - a.
$$

このとき$a \modp{p} -a = 0$は明らか。また逆元は唯一つである。
実際$a \modp{p} b = a \modp{p} c = 0$ とすると
$(a + b) \modd{p} = (a + c) \modd{p}$より
$((a + b) - (a + c)) \modd{p} = 0$で
これから$b \modd{p} = c \modd{p}$となるが、$b, c \in \galf(p)$でこれが成立するには$b = c$でなければ
ならない。

$a \neq 0$の乗算に関する逆元$a^{-1}$を以下を満たす数として定義する:

$$
(a \cdot a^{-1}) \modd{p} = 1.
$$

このような$a^{-1}$が $\set{0, 1, 2, \ldots, p-1}$ にただ一つ存在することは、
次のベズーの等式から保証される。

ベズーの等式 https://en.wikipedia.org/wiki/B%C3%A9zout%27s_identity とは、

$$
\forall a, b \in \mathbb{Z}.\ \exists x, y \in \mathbb{Z}.\ ax + by = \text{gcd}(a, b).
$$

証明は難しくないのでWikipediaなどを参考にしてもらうとして、
今回は$a$と$p$が互いに素であるので次が成立する

$$
\exists x, y \in \mathbb{Z}.\ ax + py = 1.
$$

これを元に乗算に関する逆元の候補が存在することを示す。
$ax + py = 1$より$ax = 1-py$であるから両辺の$p$での剰余をとると

$$
a (x \modd{p}) = 1
$$

となる。

次に一意性を確認する。
$a x' = 1$とする$x' \in \set{0, 1, \ldots, p}$が存在したとすると
$a x' \modeq{p} a (x \modd{p})$より$x' \modeq{p} (x \modd{p})$となり$x' = x \modd{p}$となる。

よって乗算の逆元が存在することが示せた。



加算と乗算の分配法則

$$
a \modm{p} (b \modp{p} c) = (a \modm{p} b) \modp{p} (a \modm{p} c)
$$

は下の計算から成立する:

$$
\begin{aligned}
a \modm{p} (b \modp{p} c) = (a + (b \cdot c) \modd{p}) \modd{p} = \\
(a + (b \cdot c)) \modd{p} = \\
(a \cdot b + a \cdot c) \modd{p} = \\
((a \cdot b) \modd{p} + (a \cdot c) \modd{p}) \modd{p} = (a \modm{p} b) \modp{m} (a \modm{p} c).
\end{aligned}
$$

---

## XORとANDで定まる$\galf(2)$
要素数$2$の体が存在することは分かっているので、具体的に$\galf(2)$を構成する。

加算は以下のようになり定義することになり、XORに一致していると分かる。
| + | 0 | 1 |
|---|---|---|
| 0 | 0 | 1 |
| 1 | 1 | 0 |

これによって $-0 = 0,\ -1 = 1$ となることに注意する。

次に乗算は以下で、今度はANDに一致する。
| $\cdot$ | 0 | 1 |
|---|---|---|
| 0 | 0 | 0 |
| 1 | 0 | 1 |

これによって $1^{-1} = 1$ となることに注意する。

## $\galf(2^n)$の既約多項式を用いた構成
次に素体ではない場合の構成をみる。

念のために、上でみたような何でも剰余をとる方法では体にならないことを確認する。
例えば$\galf(2^2)$で剰余をとると、元$2$の乗算に関する逆元$2^{-1}$が存在しない:

$$
2 \modm{4} 0 = 0,\ 2 \modm{4} 1 = 2,\ 2 \modm{4} 2 = 0,\ 2 \modm{4} 3 = 2.
$$

参考: https://mathtrain.jp/galoisfield

この節ではまず既約多項式を用いた構成を述べる。
次の節で省メモリ実装が可能になる「原始多項式」を用いた構成を述べる。
原始多項式を用いた構成の方が教科書などでは一般的かと思うが、
いきなり原始多項式を使って構成すると分配法則を証明するところで結構面倒くさくなると思うので、
このように段階的にやる。

有限体の理論から以下の性質を利用する:
+ $\galf(2)$を係数とする$n$次既約多項式$P(X)$が存在する。
+ 既約多項式は根$\alpha \in \galf(2^n)$を持つ。
+ $\galf(2^n)$を$\galf(2)$上の$n$次元ベクトル空間としてみると$\alpha^0, \alpha^1, \ldots, \alpha^{n-1}$は基底になる。
    + すなわち

    $$
      \galf(2^n) = \set{ p(\alpha) : \deg(p) \leq n-1 \text{ or } p = 0}.
    $$


さて加算と乗算を導入するが、
これには素数$p$に関して剰余を取る操作を中心に$\galf(p)$を作ったようにして、
今度は既約多項式$P(\alpha)$で剰余をとることで$\galf(2^n)$を構成する。

プログラムで実装する際には多項式の係数表示

$$
\galf(2^n) = \set{ \tuple{c_{n-1}, c_{n-2}, \ldots, c_1, c_0} :  c_i \in \galf(2) }.
$$

を用いると便利である。各タプル$\tuple{c_{n-1}, \ldots, c_1, c_0}$は次のことを意味する:

$$
c_{n-1} \alpha^{n-1} + \cdots + c_2 \alpha^2 + c_1 \alpha + c_0.
$$


まず加算を定義する:
+ 加算$p \oplus q$は$\galf(2)$-多項式の加算で定義すれば良い。
+ 加算$p$の逆元$-p$は一意に存在するが、$p \oplus p = 0$なので$p$そのもので良い。

乗算$\otimes$については$P(\alpha)$で剰余をとる必要がある。
すなわち$p, q \in \galf(2^n)$について

$$
p \otimes q = (p \cdot q) \modd{P}
$$

とする。
$P(\alpha)$が$n$次多項式であるから、その剰余項の次数は$n-1$以下または零で、
$\galf(2^n)$に属する。

乗算の逆元$p^{-1}$を考える。$\galf(p)$の時にBezout identityを用いたように、
体を係数とする1変数多項式上のBezout identityを用いれば良い。

+ 参考リンク https://en.wikipedia.org/wiki/Polynomial_greatest_common_divisor

体$K$を係数とする1変数多項式$K[x]$上のBezout identityは
$\mathbb{Z}$上のそれと類似した以下のようなものである:

非零な$a, b \in K[x]$について

$$
ax + by = \gcd(a, b)
$$

とする$x, y \in K[x]$が存在する。一応証明しておくと、$\mathbb{Z}$の場合と殆ど同じだが

+ $S = \set{ v = as + bt : \deg(v) \geq 0 }$の$\deg$に関する最小元の一つを$d$とする。
    + $\deg$に関する最小元なので$d \neq d'$かつ$\deg d = \deg d'$とするような$d' \in S$もあるかもしれないことには注意しておく。
    + 集合$S$は線型結合から$\deg 0 < 0$として$0$を除外した感じ
    + $\deg(0)$は通常は負値として定義されることにも注意
+ $a = qd + r$で$r = 0$または$0 \leq \deg r < \deg d$である。
+ $r = 0$なら$d$は$a$を割り切る。
+ $r \neq 0$の場合は

    $$r = a - qd = a - q(as + pt) = a(1 - qs) + p(-t)$$

  から$r \in S$である。
  ところがこの場合は$d$の$\deg$に関する最小性に反するので矛盾。
+ 結局$d$は$a$を割り切るが、同様の議論で$d$は$b$も割り切る。
+ よって$d$は$a, b$を両方割り切る。

最大公約多項式（$d$は全ての公約多項式によって割ることができる）は

+ $c$を公約多項式とし、$a = cu$, $b = cv$とする。
+ $d = cux + cvy = c(ux + vy)$なので$c$は$d$を割り切る。

さて、Bezout identityを使うと、$n-1$次以下の多項式$p$と$n$次既約多項式$P$は互いに素なので

$$
p x + P y = 1
$$

となる多項式$x, y \in \galf(2)[\alpha]$が存在する。
このとき両辺を$p$で割って

$$
p (x \modd{P}) = 1
$$

であるから$p \otimes (x \modd {P}) = 1$でもあり逆元候補が存在する。

もし$\galf(2^n)$中に

$$
p \otimes x = p \otimes y = 1
$$

とする$x \neq y$が存在したとすると

$$
(p \cdot x) \modd{P} = (p \cdot y) \modd{P} \implies
(p \cdot (x - y)) \modd{P} = 0
$$

$p$と$P$が互いに素なので$x - y$を$P$が割り切るしかないが、
$x - y$の次数は高々$n-1$なので$x = y$でなければならない。

従って$p \in \galf(2^n)$かつ$p \neq 0$ならば逆元$p^{-1}$が存在することを示せた。

結合法則

$$
p \otimes (q \oplus r) = (p \otimes q) \oplus (p \otimes r)
$$

も明らかである。

# 原始多項式を用いた$\galf(2^n)$の構成
既約多項式を用いた構成によって$\galf(2^n)$を構成できるが、
実装を考えると幾つか問題がある:
+ 乗算をするたびに剰余を取る必要がある
+ 乗算に関する逆元を求める操作が重い

これらの問題は一般的なテクニックとしては乗算表を一度構成しておいて、
計算時には表の参照で済ませるというものであるが、
表のサイズが相当大きくなるので現実的ではない。
例えば$n=16$の場合には要素を16bit=2byteで表現するとしても

$$
(2^{16}) \times (2^{16}) \times 2 \text{Byte} = 8192 \text{MiB}
$$

ということになる。乗算が可換になるとしても焼石に水だ。

そこで原始多項式を用いて乗算を簡略化する方法を考える。

使う性質は次の通り:
+ $\galf(2)$係数$n$次原始多項式$P(X)$が必ず存在する。
+ $\galf(2^n)$に存在する原始根を$\alpha$と書く。つまり
    + $P(\alpha) = 0$
    + $\alpha$が$\galf(2^n) - \set{ 0 }$を乗算に関する巡回群とする生成元
    + $1, \alpha, \alpha^2, \ldots, \alpha^{2^n-2}, \alpha^{2^n-1} = 1, \ldots$として巡回

さて、原始多項式は既約多項式でもあるから、
上でみた方法によって$\galf(2^n)$を具体的に構成することができる。
ただし、乗算については以下の方法によって行う。

さて$P(\alpha)$で剰余を取ることによって以下の写像を定める:

$$
\Psi : \mathcal{A} = (\set{0, 1, \alpha, \ldots, \alpha^{2^n-2}}) \to \galf(2^n).
$$

$\Psi$が単射であることを確認する。
$x, y \in \mathcal{A}$ かつ $x \neq y$ について$P(\alpha)$で割ると

$$
\begin{aligned}
x = a P(\alpha) + \Psi(x), \\
y = b P(\alpha) + \Psi(y).
\end{aligned}
$$

と表現される。
$P(\alpha) = 0$であるから$x \neq y$ならば$\Psi(x) \neq \Psi(y)$ となる。

$\mathcal{A}$と$\galf(2^n)$は要素数が等しいので$\Psi$の単射性から全射性も導かれる。


$\Psi$を用いて$\galf(2^n)$上に積を次のように導入する:

$$
p \odot q = \Psi(\Psi^{-1}(p) \cdot \Psi^{-1}(q)).
$$

すなわち、一度$\mathcal{A}$の指数表記上に持っていって簡単な計算を行い、
その後で引き戻すというものである。

当然次のことを確認しておく必要がある:

$$
p \otimes q = p \odot q.
$$

右辺については

$$
\begin{aligned}
(\Psi^{-1}(p) \cdot \Psi^{-1}(q)) \modd{P} = \\
(\Psi^{-1}(p) \modd{P} \cdot \Psi^{-1}(q) \modd{P}) \modd{P} = \\
(p \cdot q) \modd{P}
\end{aligned}
$$

となるので明らかである。

途中で$
(p \cdot q) \modd{P} = (p \modd{P} \cdot q \modd{P}) \modd{P}
$を使ってることに注意。

$\odot$の逆元については
$\Psi^{-1}(p) = \alpha^i$であれば$\Psi(\alpha^{2^n-1-i})$として与える。

$$
\begin{aligned}
p \odot \Psi(\alpha^{2^n-1-i}) = \\
\Psi(\alpha^i) \odot \Psi(\alpha^{2^n-1-i}) = \\
(\alpha^i \cdot \alpha^{2^n-1-i}) \modd{P} = 1 \modd{P} = 1.
\end{aligned}
$$

まとめると
+ 全単射を用いて乗算を定義する
+ これは既存の乗算と同じ計算結果をもたらす
+ この乗算は指数加算$\alpha^i \cdot \alpha^j = \alpha^{i+j}$と
+ 乗算の逆元も容易に求められる。
    + 拡張ユークリッド互除法を使う必要がない。

$\galf(2^n)$で$\Psi$と$\Psi^{-1}$を実装する時にどれだけのメモリが必要になるかというと

$$
2 \times (2^n \times \frac{n}{8} \text{Byte})
$$

である。$n = 16$（すなわち$\galf(2^16)$の要素が2バイト長）の時に$0.25$MiBになる。
$n = 32$ では $32,768$MiB になってしまうのでこの方法は使えないだろう。
