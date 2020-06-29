$$
\gdef\bec#1{{\mathbf{#1}}}
$$

# 記法

この頁ではことわりがなければ 体$K$ 上の行列を考えます。

太文字 $\bec{a}$ で行ベクトルをあらわします。

$k \in K$ について

$$
k \cdot \bec{a} =
k \cdot (a_1, a_2, \ldots, a_n) =
(k a_1, k a_2, \ldots, k a_n)
$$

として積を導入しときます。

$(h, w)$-行列というのは次のような高さが$h$で幅が$w$の行列です

$$
\begin{pmatrix}
\bec{a}_1 \\
\bec{a}_2 \\
\vdots \\
\bec{a}_h
\end{pmatrix} =
\begin{pmatrix}
a_{11} & a_{12} & \ldots & a_{1w} \\
a_{21} & a_{22} & \ldots & a_{2w} \\
\vdots & \vdots & a_{ij} & \vdots \\
a_{h1} & a_{h2} & \ldots & a_{hw}
\end{pmatrix}.
$$

$A_{ ij }$ で $i$ 番目の行ベクトルの
$j$ 番目の要素 $a_{ i j }$ を表します。

# Gauss–Jordan eliminationによる逆行列の計算

手順としては

```ruby
for i in 1..n {
  M[i][i]が零元だと掃き出しが出来ないので
  M[k][i] != 0 となるような k>i 行目の列ベクトルとi行目を入れ替える。 # 入れ替え (1)
  （入れ替えた後の行列もそのままMと書くことにする）

  もしそのようなkがなければ逆行列は存在しないので計算終了 (★)

  M[i] = M[i] / M[i][i] としてM[i][i]を1にしておく # 正規化 (2)

  for j in 1..n {
    if i != j then
      M[j] -= M[j][i] * M[i]; # 掃き出し (3)
    end
  }
}

(★)でexitせずここまで来たならば M は単位行列になっている
```

この疑似プログラムの正当性として

* 計算が正常終了する ==> 正則行列
* 正則行列 ==> 計算が正常終了する

を証明する。

そのために行の入れ替え操作(1)と、
体の要素を行に掛ける操作(2)と、
ある行に別の行を足し込む操作(3)が
基本行列と呼ばれる逆行列で表現できることを証明しておく。

$(n, n)$-行列 $M$ の $i$-行ベクトルと $j$-行ベクトルを入れ替える操作 $A_{i \leftrightarrow j}$ は $i < j$ とすると

$$
A_{i \leftrightarrow j} =
\begin{pmatrix}
\bec{c}_1 \\
\bec{c}_2 \\
\vdots \\
\bec{c}_j \\
\vdots \\
\bec{c}_i \\
\vdots \\
\bec{c}_n
\end{pmatrix}
$$

と書ける。ただし

+ $\bec{c}_k = (0\ 0\ \ldots 1\ \ldots 0)$ は先頭から$k$番目が値$1$を持つような列ベクトルで
+ $A_{i \leftrightarrow j}$は上から$i$番目に $\bec{c}_j$ があり、$j$番目に $\bec{c}_i$ が存在している。

単位行列は

$$
I_n = \begin{pmatrix}
\bec{c}_1 \\
\vdots \\
\bec{c}_i \\
\vdots \\
\bec{c}_j \\
\vdots \\
\bec{c}_n
\end{pmatrix}
$$

と書けることに注意する。

$C_{i \leftarrow j} A$ が $A$ の$i$行目と$j$行目を入れ替えることは、

$$
A = \begin{pmatrix}
\bec{a}_1 \\
\vdots \\
\bec{a}_n
\end{pmatrix}
$$

としてみると

$$
C_{i \leftarrow j} A = \begin{pmatrix}
1 \cdot \bec{a}_1 + 0 \cdot \bec{a}_2 + \cdots + 0 \cdot \bec{a}_n \\
0 \cdot \bec{a}_1 + 1 \cdot \bec{a}_2 + \cdots + 0 \cdot \bec{a}_n \\
\vdots \\
0 \cdot \bec{a}_1 + \cdots + 1 \cdot \bec{a}_j + \cdots + 0 \cdot \bec{a}_n \\
\vdots \\
0 \cdot \bec{a}_1 + \cdots + 1 \cdot \bec{a}_i + \cdots + 0 \cdot \bec{a}_n \\
\vdots \\
0 \cdot \bec{a}_1 + \cdots + 1 \cdot \bec{a}_n
\end{pmatrix} =
\begin{pmatrix}
\bec{a}_1 \\
\bec{a}_2 \\
\vdots \\
\bec{a}_j \\
\vdots \\
\bec{a}_i \\
\vdots \\
\bec{a}_n
\end{pmatrix}
$$

となることから明らかである。

また $A_{i \leftarrow j} A_{i \leftarrow j} = I$ であるから $A_{i \leftarrow j}$ は正則行列である。

次に指定した行$i$を$k$倍する操作であるが、これは

$$
C_{k \cdot i} \begin{pmatrix}
\bec{a}_1 \\
\bec{a}_2 \\
\vdots \\
\bec{a}_n
\end{pmatrix} =
\begin{pmatrix}
\bec{c}_1 \\
\bec{c}_2 \\
\vdots \\
k \cdot \bec{c}_i \\
\vdots \\
\bec{c}_n
\end{pmatrix} \begin{pmatrix}
\bec{a}_1 \\
\bec{a}_2 \\
\vdots \\
\bec{a}_n
\end{pmatrix} =
\begin{pmatrix}
\bec{a}_1 \\
\bec{a}_2 \\
\vdots \\
k \cdot \bec{a}_i \\
\vdots \\
\bec{a}_n
\end{pmatrix}
$$

とすれば良い。

$$
C_{k \cdot i} \ C_{k^{-1} \cdot i} = I_n
$$

であるから $C_{k \cdot i}$ も逆行列を持つ。

$i$行目の$k$倍を$j$行目に足す操作であるが、これには

$$
C_{j += k \cdot i} \begin{pmatrix}
\bec{a}_1 \\
\vdots \\
\bec{a}_i \\
\vdots \\
\bec{a}_j \\
\vdots \\
\bec{a}_n
\end{pmatrix} =
\begin{pmatrix}
\bec{c}_1 \\
\vdots \\
\bec{c}_ i \\
\vdots \\
k \cdot \bec{c}_i + \bec{c}_j \\
\vdots \\
\bec{c}_n
\end{pmatrix}
\begin{pmatrix}
\bec{a}_1 \\
\vdots \\
\bec{a}_i \\
\vdots \\
\bec{a}_j \\
\vdots \\
\bec{a}_n
\end{pmatrix}
= \begin{pmatrix}
\bec{a}_1 \\
\vdots \\
\bec{a}_i \\
\vdots \\
k \cdot \bec{a}_i + \bec{a}_j \\
\vdots \\
\bec{a}_n
\end{pmatrix}
$$

とすれば良い。

$$
C_{j += k \cdot i} \ C_{j += (-k) \cdot i} = I_n
$$

であるから、これもまた逆行列になる。

さて、計算が正常終了する場合というのは

$$
C_1 C_2 \cdots C_n A = I
$$

とするような基本操作列 $C_1, C_2, \ldots, C_n$ が存在することになり、
行列 $(C_1 C_2 \cdots C_n)$ が $A$ の逆行列になる。

一方で計算が異常終了した場合に $A$ が正則でない場合を考える。
この対偶をとれば、$A$が正則であれば手続きが正常終了することがいえる。

さて、計算が異常終了する場合というのは

$$
(C_1 C_2 \cdots C_n) A = \begin{pmatrix}
a_{11}=1& 0 & \cdots & 0 & a_{1, i+1} & \cdots \\
0 & a_{22}=1 & \cdots & 0 & a_{2, i+1} & \cdots \\
\vdots & \vdots & & \vdots & \vdots & \\
0 & 0 & \cdots & a_{ii}=1 & a_{i, i+1} & \cdots \\
0 & 0 & \cdots & 0 & 0 & \cdots\\
{\huge 0}  & {\huge 0} & \cdots & {\huge 0}  & {\huge 0} & \cdots
\end{pmatrix}
$$

とする基本行列たち $C_1, C_2, \ldots, C_n$ があるということになる。

このとき、右辺から基本行列をかけると今度は列に関する変形ができるため、
$a_{i, i+1}$から始まる列を全て0にできる。
この行列は明らかに正則行列ではないので証明が終わるが、もう少し泥臭くやっておく。

まず右辺の行列をブロック行列でもう少し見やすくしておく

$$
\left(
\begin{array}{c|c|c}
I_i & \bec{a} & P \\\hdashline
{\large 0} & \bec{0} & Q
\end{array}
\right)
$$

ここだけは$\bec{a}, \bec{0}$を行ベクトルでなく列ベクトルとして使っています。

このとき相異なる列ベクトル $\bec{v}, \bec{w}$ で

$$
((C_1 C_2 \cdots C_n) A) \bec{v} =
((C_1 C_2 \cdots C_n) A) \bec{w}
$$

とするものがあることをみる。

列ベクトル側もブロック表記すると、

$$
\left(
\begin{array}{c|c|c}
I_i & \bec{a} & P \\\hdashline
{\large 0} & \bec{0} & Q
\end{array}
\right)
\left(
\begin{array}{c}
\bec{x} \\\hdashline
z \\\hdashline
\bec{y}
\end{array}
\right) =
\left(
\begin{array}{c}
I_i \bec{x} + z \bec{a} + P \bec{y} \\\hdashline
Q \bec{y}
\end{array}  
\right)
$$

と書けて次が成立する:

$$
\left(
\begin{array}{c|c|c}
I_i & \bec{a} & P \\\hdashline
{\large 0} & \bec{0} & Q
\end{array}
\right)
\left(
\begin{array}{c}
\bec{x} \\\hdashline
z \\\hdashline
\bec{y}
\end{array}
\right) =
\left(
\begin{array}{c}
I_i \bec{x} + z \bec{a} + P \bec{y} \\\hdashline
Q \bec{y}
\end{array}  
\right) =
\left(
\begin{array}{c|c|c}
I_i & \bec{a} & P \\\hdashline
{\large 0} & \bec{0} & Q
\end{array}
\right)
\left(
\begin{array}{c}
\bec{x} + z \bec{a} \\\hdashline
0 \\\hdashline
\bec{y}
\end{array}
\right)
$$

すなわち任意の $z \neq 0$ で、変形済み行列が正則でない証拠になる。

# Gaussian-Eliminationによる解の計算

列ベクトル$y$と正則$A$が与えられた時に

$$
y = A x
$$

を満たす列ベクトル$x$を求めたい。
上でみたように逆行列をGJEによって求めて、 $A^{-1}y$ を計算してしまう手もあるが、
もう少し計算回数を減らす方向としてGaussian Elimination(GE)がある。

こちらも基本変形行列を用いる。

$$
P_1 P_2 \cdots P_m A =
\begin{pmatrix}
a_{1,1} & a_{1,2} & a_{1,3} & \cdots & a_{1,n-1} & a_{1,n} \\
0 & a_{2,2} & a_{2,3} & \cdots & a_{2,n-1} & a_{2,n} \\
0 & 0 & a_{3,3} & \cdots & a_{3, n-1} & a_{3,n} \\
\vdots & \vdots & \vdots & & \vdots & \vdots \\
0 & 0 & 0 & \cdots & a_{n-1,n-1} & a_{n-1,n} \\
0 & 0 & 0 & \cdots & 0 & a_{n, n}
\end{pmatrix} = U
$$

によって左下に零元が集まるようにして、右上三角行列 $U$ を作る。

各$P$は基本行列であるから

$$
A x = y \iff ((P_1 P_2 \cdots P_m) A) x = (P_1 P_2 \cdots P_m) y
$$

なので

$$
U \begin{pmatrix}
x_1 \\
\vdots \\
x_{n-1} \\
x_n
\end{pmatrix}
= \begin{pmatrix}
z_1 \\
\vdots \\
z_{n-1} \\
z_n
\end{pmatrix}
$$

の形を解けば良い。

これを解く時に、$U$を下から上に向かって見ていく。すなわち

+ $a_{n, n} x_n = z_n$ とする $x_n = \frac{z_n}{a_{n,n}}$ を取れば良い。
+ $a_{n-1, n-1} x_{n-1} + a_{n-1, n} x_n = z_{n-1}$ とする $x_{n-1}$を取れば良いが、既に$x_n$が確定しているのですぐに求まる。
+ このようにして $x_n, x_{n-1}, \ldots, x_2, x_1$ の順番に確定させていく。

上の手順で解ベクトル$x$が求まることが分かる。

$0$にする箇所が減ることに加えて、逆行列を求めたあとに行列積を行う必要がない。

# Vandermonde行列

$$
V(h, w) =
\begin{pmatrix}
1 & a_1 & \ldots & a^{w-1}_1 \\
1 & a_2 & \ldots & a^{w-1}_2 \\
\vdots & \vdots & & \vdots \\
1 & a_h & \ldots & a^{w-1}_q
\end{pmatrix}
, i \neq j \implies a_i \neq a_j
$$

または転地形式

$$
V(h, w) =
\begin{pmatrix}
1 & 1 & \ldots & 1 \\
a_1 & a_2 & \ldots & a_w \\
\vdots & \vdots & & \vdots \\
a^{h-1}_1 & a^{h-1}_2 & \ldots & a^{h-1}_w
\end{pmatrix}
, i \neq j \implies a_i \neq a_j
$$

をヴァンデルモンド行列（Vandermonde matrix）と呼ぶ。

正方ヴァンデルモンド行列$V(n, n)$の行列式はいつでも非零で、すなわち逆行列が存在する:

$$
\forall n \geq 1. \det V(n, n) \neq 0.
$$

$GF(q)$上のヴァンデルモンド行列について注意するべきことは、
その部分正方行列に非正則（行列式値が零、可逆でない）なものを持つことである。

$GF(7)$について

$$
\begin{pmatrix}
1 & 2 & 2^2 & 2^3 \equiv_7 1 \\
1 & 4 & 4^2 \equiv_7 2 & 4^3 \equiv_7 1
\end{pmatrix}
$$

の部分正方行列

$$
\begin{pmatrix}
1 & 2^3 \equiv_7 1 \\
1 & 4^3 \equiv_7 1
\end{pmatrix}
$$

は非正則行列です。

サイズ$n$の正方Vandermonde行列の行列式は

$$
\det V = \prod_{1 \leq i < j \leq n} (a_j - a_i)
$$

で与えられるのですが、
（証明はググれば出ます: 参考 https://proofwiki.org/wiki/Vandermonde_Determinant）
$\det V$が非零になるためには $a_j - a_i$ が全て非零である必要があります。

「Vandermonde行列の正方部分行列もまた非零になる」というのは
ググると結構いろんなテキストに出てくるのですが、上のように
具体的な反例も出てきます。これはどういうことでしょうか？

部分行列$V'$を取った場合にも、
因子定理(https://proofwiki.org/wiki/Polynomial_Factor_Theorem)により$V' = (a^k_j - a^k_i)P(\ldots)$の形式で書ける（ハズ）なので、これが非零になるためには

1. Vandermonde行列の要素 $a_1, a_2, \ldots, a_n$ が相異なる。すなわち $a_j - a_i \neq 0$ という一般的な条件に加えて
2. $a^k_j - a^k_i \neq 0$という追加の条件が必要になります。

実数体や複素数体では $a \neq b \implies a^k \neq b^k$ が自動的に導けるのですが、一般の体ではこれが成立せず、実際に上で見たように$GF(7)$では$2 \neq 4$だが$2^3 = 4^3$となってしまいます。

# MDS生成行列としてのVandermonde行列

$(n, n+k)$-生成行列$M$による作用

$$
v = w M
$$

は$n$-要素ベクトル$w$を冗長拡大して$(n+k)$-要素ベクトルに変換しているとみることができる。
このとき、変換後のベクトルから高々$k$まで要素が欠落しても元のデータが復元出来る場合に
$M$をMDS生成行列と呼ぶ。$k+1$以上の要素が欠落すると復元できない。

$(n, n+k)$ヴァンデルモンド行列

$$
V = \begin{pmatrix}
1 & 1 & \cdots & 1 & \cdots & 1 \\
a_1 & a_2 & \cdots & a_n & \cdots & a_{n+k}\\
a^2_1 & a^2_2 & \cdots & a^2_n & \cdots & a^2_{n+k} \\
\vdots & \vdots & & \vdots & & \vdots \\
a^{n-1}_1 & a^{n-1}_2 & \cdots & a^{n-1}_n & \cdots & a^{n-1}_{n+k}
\end{pmatrix}
$$

を考える。

ヴァンデルモンド行列の任意の部分正方行列は可逆ではないが、
「$(n, n)$正方行列は可逆」ということは証明できる。
例えば

$$
V' = \begin{pmatrix}
1 & 1 & \cdots & 1 \\
b_1 & b_2 & \cdots & b_n \\
\vdots & \vdots & & \vdots \\
b^{n-1}_1 & b^{n-1}_2 & \cdots & b^{n-1}_n
\end{pmatrix}
$$

という $\{ b_1, b_2, \ldots, b_n \} \subset \{ a_1, a_2, \ldots, a_{n+k} \}$ を
満たす正方部分行列は正方ヴァンデルモンド行列であるから明らかに可逆である。

$(n, n+k)$-ヴァンデルモンド行列$V$を用いたデータ$w$の符号化は

$$
v = wV
$$

とするだけで良い。

復号を考える。
$v'$を$v$から$k$個の要素が欠落した行ベクトルとする。
このとき、欠落した要素のindexに対応する列ベクトルを$V$から除去して得られる正方行列を$V'$とすると

$$
v' = w V'
$$

が成立する。さて$V'$は上でみたように可逆であるので逆行列$V'^{-1}$が存在し、このとき

$$
w = v' V'^{-1}
$$

によって復号が成功する。

# 実装方針1

$GF(2^{16})$の有限体実装があるとする（1 objectが2バイトになるので実際にありがち）。
このときに、$160_{\text{Byte}}$のファイルを情報ブロック10のparity4で符号化・復号化するにはどうしたら良いか？

$(10, 14)$のヴァンデルモンド行列を使いたいので、
16バイト相当の$GF(2^{128})$上の行列演算があれば自然だが、$GF(2^{16})$しかない。

そこで $16_{\text{Byte}}/2_{\text{Byte}} = 8$ 分割した上で、
そのそれぞれで符号化と復号化を行うことにする。

1. 160バイトのデータ$D$を先頭から20バイトずつ8個に分割$d_1, d_2, \ldots, d_8$する。
2. $d_i$は20バイトなので$GF(2^{16})$上の$10$-要素ベクトルとして見られる。
3. $d_i V_{10, 14}$で得られる28バイトの$14$-要素ベクトルを集めた
   $(d_1 V_{10, 14}, d_2 V_{10, 14}, \ldots, d_8 V_{10, 14})$が符号化済みのデータに相当する。
4. 復号する時には要素ごとに行えば良い。

#  実装方針2

実装方針1とは異なるより実践的な方法がある。

実装方針1ではVandermonde行列を用いたが、systematic MDS matrixを用いた場合には
単位行列部分が揃っていたとしてもデータの復元のために

```
orig[10*i+0] = block0[i]
orig[10*i+1] = block1[i]
orig[10*i+2] = block2[i]
...
orig[10*i+9] = block9[i]
```

というようなメモリ上のgatherを行わなければならない。

ここでは

```
orig[0..=16] = block0
orig[16..=32] = block1
...
orig[144..=160] = block9
```

というような局所性がもう少しだけマシになる方法を考えるとする。

まず160バイトのデータをデータブロック数である10個に等分割する。
16バイト/ブロックを、$(uint16_1, uint16_2, ..., uint16_8)$ という $GF(2^{16})$  の8-tupleで表現する。

このとき


$$
M \begin{pmatrix}
\vec{v}_1 \\
\vec{v}_2 \\
\vdots \\
\vec{v}_{10}
\end{pmatrix} =
\begin{pmatrix}
\vec{w}_1 \\
\vdots \\
\vec{w}_{13} \\
\vec{w}_{14}
\end{pmatrix}
$$


という符号化になる。8-tupleに対する有限体の要素との演算は


$$
\begin{aligned}
g \odot (g_1, g_2, \ldots, g_8) = (g \cdot g_1, g \cdot g_2, \ldots, g \cdot g_8), \\
g \oplus (g_1, g_2, \ldots, g_8) = (g + g_1, g + g_2, \ldots, g + g_8). \\
\end{aligned}
$$


としてcomponentwizeに定義する。このようなtuple上への拡張をしたときに、正則行列 $P$ について


$$
P^{-1} (P \bec{v}) = (P^{-1} P) \bec{v}
$$


を証明すればdecodeできることが証明できる。


$$
\begin{aligned}
\begin{pmatrix}
\vec{a}_1 \\
\vec{a}_2 \\
\vdots \\
\vec{a}_n
\end{pmatrix} \left(\begin{pmatrix}
\vec{b}_1 \\
\vec{b}_2 \\
\vdots \\
\vec{b}_n
\end{pmatrix} \begin{pmatrix}
\bec{c}_1 &
\cdots &
\bec{c}_n
\end{pmatrix}\right) = \\
\begin{pmatrix}
\vec{a}_1 \\
\vec{a}_2 \\
\vdots \\
\vec{a}_n
\end{pmatrix}
\begin{pmatrix}
\begin{pmatrix}
\vec{b}_1 \\
\vec{b}_2 \\
\vdots \\
\vec{b}_n
\end{pmatrix} \cdot \bec{c}_1 & \cdots &
\begin{pmatrix}
\vec{b}_1 \\
\vec{b}_2 \\
\vdots \\
\vec{b}_n
\end{pmatrix} \cdot \bec{c}_n
\end{pmatrix} = \\
\begin{pmatrix}
\begin{pmatrix}
\vec{a}_1 \\
\vec{a}_2 \\
\vdots \\
\vec{a}_n
\end{pmatrix}
\cdot
\left(
\begin{pmatrix}
\vec{b}_1 \\
\vec{b}_2 \\
\vdots \\
\vec{b}_n
\end{pmatrix} \cdot \bec{c}_1\right) & \cdots &
\begin{pmatrix}
\vec{a}_1 \\
\vec{a}_2 \\
\vdots \\
\vec{a}_n
\end{pmatrix}
\cdot
\left(
\begin{pmatrix}
\vec{b}_1 \\
\vec{b}_2 \\
\vdots \\
\vec{b}_n
\end{pmatrix} \cdot \bec{c}_n\right)
\end{pmatrix}
\end{aligned}
$$

$$
\begin{pmatrix}
\vec{a}_1 \\
\vec{a}_2 \\
\vdots \\
\vec{a}_n
\end{pmatrix} \cdot \left(
\begin{pmatrix}
\vec{b}_1 \\
\vec{b}_2 \\
\vdots \\
\vec{b}_n
\end{pmatrix} \cdot
\bec{c}\right) =
\begin{pmatrix}
\vec{a}_1 \\
\vec{a}_2 \\
\vdots \\
\vec{a}_n
\end{pmatrix} \cdot
\begin{pmatrix}
\vec{b}_1 \ast \bec{c} \\
\vec{b}_2 \ast \bec{c} \\
\vdots \\
\vec{b}_n \ast \bec{c}
\end{pmatrix}
$$


このとき最終的な列ベクトルの $i$ 要素目の値は


$$
\vec{a}_i \ast
\begin{pmatrix}
\vec{b}_1 \ast \bec{c} \\
\vec{b}_2 \ast \bec{c} \\
\vdots \\
\vec{b}_n \ast \bec{c}
\end{pmatrix}
$$



$$
\left(\begin{pmatrix}
\vec{a}_1 \\
\vec{a}_2 \\
\vdots \\
\vec{a}_n
\end{pmatrix}
\begin{pmatrix}
\vec{b}_1 \\
\vec{b}_2 \\
\vdots \\
\vec{b}_n
\end{pmatrix}\right) \cdot
\bec{c}
$$


$i$番目の要素は
$$
\begin{pmatrix}
\vdots \\
\vec{a}_i \star \begin{pmatrix}
\vec{b}_1 \\
\vec{b}_2 \\
\vdots \\
\vec{b}_n
\end{pmatrix}  \\
\vdots
\end{pmatrix} \cdot \bec{c} =
\left(\vec{a}_i \star \begin{pmatrix}
\vec{b}_1 \\
\vec{b}_2 \\
\vdots \\
\vec{b}_n
\end{pmatrix}\right) \ast \bec{c}
$$


* $\tilde{A}$は $A$ の要素をduplicateしてtupleにするやつ 演算はcomponentwise
* $\tilde{A} \tilde{B} = \widetilde{A B}$
* $A (B w)$はヘテロ演算なしの結果 $\tilde{A} (\tilde{B} w)$ と同じで、これは結合則から $(\tilde{A} \tilde{B}) w$
* $\widetilde{A B} w$はヘテロ演算ありの$(A B) s$と等しい



こっちの計算だと、かりに復号することになってもブロック単位で要素ならべて行列演算すれば良いだけなので楽

実装方針1だとほどいてから並べないといけないので

---

$$
A \ast \begin{pmatrix}
a_1 \\
a_2 \\
\vdots \\
a_{12}
\end{pmatrix} =
A \begin{pmatrix}
a_1 & a_4 & a_7 & a_{10}\\
a_2 & a_5 & a_8 & a_{11} \\
a_3 & a_6 & a_9 & a_{12} \\
\end{pmatrix} =
\begin{pmatrix}
A a_{1,2,3} & A a_{4,5,6} & A a_{7,8,9} & A a_{10, 11, 12}
\end{pmatrix}
$$

* こっちが実装パターン1かなあ
* 復号処理を考えると

$$
O^{-1} (B^{-1}
\begin{pmatrix}
B a_{1, 2, 3} & B a_{4, 5, 6} & B_{7, 8, 9} & B_{10, 11, 12}
\end{pmatrix})
= O^{-1} \begin{pmatrix}
a_{1, 2, 3} & a_{4, 5, 6} & a_{7, 8, 9} & a_{10, 11, 12}
\end{pmatrix}
= \begin{pmatrix}
a_1 \\
a_2 \\
\vdots \\
a_{12}
\end{pmatrix}
$$


* データ $\bec{r}$ を行列化 $\zeta \bec{r}$
* $A (\zeta \bec{r})$ が符号化
    * 出来上がった行列の行 $i$ がノード $i$ に送るデータ
* $D (A (\zeta \bec{r}))$ が 正方行列になるような行ベクトルの drop
    * これは復元に必要なデータをかき集めることに対応している
* $(D A)$ が逆ベクトル持つのはVandermonde行列から作ったから
    * $D V$ は逆行列を持つのは $V$ の性質から
    * $D V'$ が逆行列持つのはなぜ？
    * $V' = V (D' V)^{-1}$ というsystematic MDS化

    $$
      (D V') ((D' V) (D V)^{-1}) = D V (D' V)^{-1} ((D' V) (D V)^{-1}) = 1
    $$

* $(D A)^{-1} (D (A (\zeta \bec{r})))$ が実際の計算だが、これは
$\zeta \bec{r}$に一致する。
* 最後に$\zeta^{-1} (\zeta \bec{r}) = \bec{r}$ でデータベクトルが戻る

列ベクトル $\bec{r}$ を行列化 $\zeta\bec{r}$ するときの方法が

$$
\eta\begin{pmatrix}
a_1 \\
a_2 \\
\vdots \\
a_{12}
\end{pmatrix} =
\begin{pmatrix}
a_1 & a_4 & a_7 & a_{10} \\
a_2 & a_5 & a_8 & a_{11} \\
a_3 & a_6 & a_9 & a_{12}
\end{pmatrix}
$$

とすると$\eta$は全単射

$$
\kappa\begin{pmatrix}
a_1 \\
a_2 \\
\vdots \\
a_{12}
\end{pmatrix} =
\begin{pmatrix}
a_1 & a_2 & a_3 & a_4 \\
a_5 & a_6 & a_7 & a_8 \\
a_9 & a_{10} & a_{11} & a_{12}
\end{pmatrix}
$$

とすると$\kappa$は全単射で、$\kappa$については

+ systematic MDSを $\kappa \bec{r}$ に掛ける時には

  $$
    \begin{pmatrix}
     I_3 \\
     M
    \end{pmatrix} (\kappa \bec{r}) =
    \begin{pmatrix}
    I_3 (\kappa \bec{r}) \\
    M (\kappa \bec{r})
    \end{pmatrix}
  $$

  であるから ノード1 にはデータの先頭から4つ、2にはその次から4つ、3にはその次から4つをそのまま送れば良いことになる。
+ 復号のときにもデータノードたちが残っていれば、バイト列を適当に並び替えてメモリに配置すればそれが元データになっている
+ パリティを使わなければならない場合

  $$
    (D A)^{-1} \begin{pmatrix}
    \text{ノード $N_1$ のデータ列} \\
    \text{ノード $N_2$ のデータ列} \\
    \text{ノード $N_3$ のデータ列}
    \end{pmatrix} = \begin{pmatrix}
    a_1 & a_2 & a_3 & a_4 \\
    a_5 & a_6 & a_7 & a_8 \\
    a_9 & a_{10} & a_{11} & a_{12}
    \end{pmatrix}
  $$

  の計算についてはノードをまたいで計算しないとダメかあ
---




$$
A \ast \begin{pmatrix}
a_1 \\
a_2 \\
\vdots \\
a_{12}
\end{pmatrix} =_?
A \begin{pmatrix}
a_1 & a_2 & a_3 & a_4 \\
a_5 & a_6 & a_7 & a_8 \\
a_9 & a_{10} & a_{11} & a_{12}
\end{pmatrix}
$$


* 列ベクトルの位置のノードにデータを送る; 列を次々に送っていく
  * 行ベクトルがある位置に送られるデータ全体
* 列ベクトル $x$ を行列にする操作 $Ox$ はありそう $O^{-1}$ もありそう

$$
A \ast v = {O'}^{-1} A (O v)
$$





# コーシー行列

# 論文メモ

+ https://ieeexplore.ieee.org/document/6292924
+ https://oatao.univ-toulouse.fr/2176/1/Lacan_2176.pdf
+ https://www.usenix.org/system/files/fast19-zhou.pdf
+ https://library.eecs.utk.edu/storage/171phpm11QF4ut-cs-05-569.pdf
