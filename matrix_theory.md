行列の話を色々書きます

# 記法

$(h, w)$-行列というのは次のような高さが$h$で幅が$w$の行列です

$$
\begin{pmatrix}
x_{11} & x_{12} & \ldots & x_{1w} \\
x_{21} & x_{22} & \ldots & x_{2w} \\
& & \vdots \\
x_{h1} & x_{h2} & \ldots & x_{hw}
\end{pmatrix}
$$

# ヴァンデルモンド行列

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

# ヴァンデルモンド行列はMDS生成行列とは
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

# 実装方針
$GF(2^{32})$の有限体実装があるとする（1 objectが4バイトになるので実際にありがち）。
このときに、$320_{\text{Byte}}$のファイルを情報ブロック10のparity4で符号化・復号化するにはどうしたら良いか？

$(10, 14)$のヴァンデルモンド行列を使いたいので、
32バイト相当の$GF(2^{256})$上の行列演算があれば自然だが、$GF(2^{32})$しかない。

そこで $32_{\text{Byte}}/4_{\text{Byte}} = 8$ 分割した上で、
そのそれぞれで符号化と復号化を行うことにする。

1. 320バイトのデータ$D$を先頭から40バイトずつ8個に分割$d_1, d_2, \ldots, d_8$する。
2. $d_i$は40バイトなので$GF(2^{32})$上の$10$-要素ベクトルとして見られる。
3. $d_i V_{10, 14}$で得られる56バイトの$14$-要素ベクトルを集めた
$(d_1 V_{10, 14}, d_2 V_{10, 14}, \ldots, d_8 V_{10, 14})$が符号化済みのデータに相当する。
4. 復号する時には要素ごとに行えば良い。

# コーシー行列

# 論文メモ
+ https://ieeexplore.ieee.org/document/6292924
+ https://oatao.univ-toulouse.fr/2176/1/Lacan_2176.pdf
+ https://www.usenix.org/system/files/fast19-zhou.pdf
+ https://library.eecs.utk.edu/storage/171phpm11QF4ut-cs-05-569.pdf
