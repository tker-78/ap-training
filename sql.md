<h1>1. 基本の操作</h1>

<h2>テーブルの作成</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">CREATE</span> <span class="syntax-all syntax-keyword">DATABASE</span> <span class="syntax-all syntax-entity">newdatabase</span>;</code></pre>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">CREATE</span> <span class="syntax-all syntax-keyword">TABLE</span> <span class="syntax-all syntax-entity">Expense</span>
(expense_id <span class="syntax-all syntax-keyword">CHAR</span>(<span class="syntax-all syntax-constant">4</span>) <span class="syntax-all syntax-keyword">NOT NULL</span>,
 expense_name <span class="syntax-all syntax-keyword">VARCHAR</span>(<span class="syntax-all syntax-constant">100</span>) <span class="syntax-all syntax-keyword">NOT NULL</span>,
 expense_category <span class="syntax-all syntax-keyword">VARCHAR</span>(<span class="syntax-all syntax-constant">100</span>) <span class="syntax-all syntax-keyword">NOT NULL</span>,
 value <span class="syntax-all syntax-keyword">INTEGER</span>,
 data_of_register <span class="syntax-all syntax-keyword">DATE</span>,
 <span class="syntax-all syntax-keyword">PRIMARY KEY</span> expense_id));</code></pre>

<h2>命名ルール</h2>

<ul>
	<li>テーブルと列名には半角文字のアルファベット、数字、アンダーバーのみが使える. <code>-</code>, <code>$</code>, <code>#</code>, <code>?</code>などの記号は使えない.</li>
	<li>名前の最初は必ず半角のアルファベット</li>
</ul>

<h2>データ型</h2>

<p><code>INTEGER</code>: 整数の型</p>

<p><code>CHAR</code>: 固定長文字列. CHAR(最大長)で指定する.</p>

<p><code>VARCHAR</code>: 可変長文字列. VARCHAR(最大長)で指定する.</p>

<p><code>DATE</code>: 日付型.</p>

<h2>制約</h2>

<p><code>NOT NULL</code>: 空白を禁止する.</p>

<p><code>PRIMAY KEY</code>: 主キー制約.</p>

<h2>テーブルの削除</h2>

<pre><code class="code-highlighted code-sql">DROP TEBLE Expense;</code></pre>

<p>削除したテーブルとそのデータは復活できない.実行時には注意すること.</p>

<h2>テーブル定義の変更</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">ALTER</span> <span class="syntax-all syntax-keyword">TABLE</span> Expense ADD COLUMN expense_method <span class="syntax-all syntax-keyword">VARCHAR</span>(<span class="syntax-all syntax-constant">100</span>);</code></pre>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">ALTER</span> <span class="syntax-all syntax-keyword">TABLE</span> Expense DROP COLUMN expense_category;
<span class="syntax-all syntax-comment"># カラムを削除
</span></code></pre>

<h2>テーブルへのデータ登録</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">BEGIN</span> TRANSACTION;

<span class="syntax-all syntax-keyword">INSERT INTO</span> Expense <span class="syntax-all syntax-keyword">VALUES</span> (<span class="syntax-all syntax-string">&#39;0001&#39;</span>, <span class="syntax-all syntax-string">&#39;T-shirt&#39;</span>, <span class="syntax-all syntax-string">&#39;cloth&#39;</span>, <span class="syntax-all syntax-constant">1000</span>, <span class="syntax-all syntax-constant">500</span>, <span class="syntax-all syntax-string">&#39;2022-05-29&#39;</span>);
<span class="syntax-all syntax-keyword">INSERT INTO</span> Expense <span class="syntax-all syntax-keyword">VALUES</span> (<span class="syntax-all syntax-string">&#39;0002&#39;</span>, <span class="syntax-all syntax-string">&#39;Hat&#39;</span>, <span class="syntax-all syntax-constant">2000</span>, <span class="syntax-all syntax-constant">400</span>, <span class="syntax-all syntax-string">&#39;2022-05-14&#39;</span>);
...

<span class="syntax-all syntax-keyword">COMMIT</span>;</code></pre>

<h2>データのアップデート</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">UPDATE</span> Expense <span class="syntax-all syntax-keyword">SET</span> value <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-constant">2000</span>
<span class="syntax-all syntax-keyword">WHERE</span> id <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-string">&#39;007&#39;</span>;</code></pre>

<h1>2. 検索</h1>

<h2>SELECT文</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-keyword">*</span> <span class="syntax-all syntax-keyword">FROM</span> Expense</code></pre>

<h2>別名</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">SELECT</span> expense_id <span class="syntax-all syntax-keyword">AS</span> ID
<span class="syntax-all syntax-keyword">FROM</span> Expense</code></pre>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">SELECT</span> id, name <span class="syntax-all syntax-keyword">AS</span> <span class="syntax-all syntax-string">&quot;名前&quot;</span>, category <span class="syntax-all syntax-keyword">AS</span> <span class="syntax-all syntax-string">&quot;分類&quot;</span>
<span class="syntax-all syntax-keyword">FROM</span> Expense</code></pre>

<figure><img src="DraggedImage.png"/></figure>

<h2>定数の出力</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">SELECT</span> name, <span class="syntax-all syntax-constant">38</span> <span class="syntax-all syntax-keyword">AS</span> VALUE, <span class="syntax-all syntax-string">&#39;2020-01-01&#39;</span> <span class="syntax-all syntax-keyword">AS</span> <span class="syntax-all syntax-keyword">DATE</span>
<span class="syntax-all syntax-keyword">From</span> Expense;</code></pre>

<figure><img src="DraggedImage-1.png"/></figure>

<h2>結果から重複行を省く</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">SELECT DISTINCT</span> category
  <span class="syntax-all syntax-keyword">FROM</span> Expense;</code></pre>

<figure><img src="DraggedImage-2.png"/></figure>

<figure><img src="DraggedImage-3.png"/></figure>

<p><code>NUll</code>は1種類のデータとして扱われる.</p>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">SELECT DISTINCT</span> name, category
  <span class="syntax-all syntax-keyword">FROM</span> Expense;</code></pre>

<p>複数のカラムを指定した場合、全てのカラムの値が一致するものは重複として削除される.</p>

<figure><img src="DraggedImage-4.png"/></figure>

<h2>WHERE句</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">SELECT</span> category
  <span class="syntax-all syntax-keyword">FROM</span> Expense
  <span class="syntax-all syntax-keyword">WHERE</span> name <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-string">&#39;iPad&#39;</span>;</code></pre>

<figure><img src="DraggedImage-5.png"/></figure>

<h2>コメントの書き方</h2>

<p><code>--</code>を先頭につける</p>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- SELECT name, date
</span><span class="syntax-all syntax-comment">--   FROM Expense
</span><span class="syntax-all syntax-comment">--   WHERE name = &#39;iPad&#39;;
</span></code></pre>

<p>または、<code>/*</code> <code>*/</code>で囲む.</p>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">/*
</span><span class="syntax-all syntax-comment">SELECT name, date
</span><span class="syntax-all syntax-comment">  FROM Expense
</span><span class="syntax-all syntax-comment">  WHERE name = &#39;iPad&#39;;
</span><span class="syntax-all syntax-comment">*/</span></code></pre>

<h2>算術演算子と比較演算子</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-constant">1</span> <span class="syntax-all syntax-keyword">*</span> <span class="syntax-all syntax-constant">10</span>;</code></pre>

<figure><img src="DraggedImage-6.png"/></figure>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-constant">2</span> <span class="syntax-all syntax-keyword">*</span> <span class="syntax-all syntax-constant">10</span> <span class="syntax-all syntax-keyword">AS</span> VALUE;</code></pre>

<figure><img src="DraggedImage-7.png"/></figure>

<p><code>NULL</code>を含む計算結果は全て<code>NULL</code>になる</p>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-keyword">NULL</span> <span class="syntax-all syntax-keyword">*</span> <span class="syntax-all syntax-constant">10</span> <span class="syntax-all syntax-keyword">AS</span> VALUE;</code></pre>

<figure><img src="DraggedImage-8.png"/></figure>

<h3>比較演算子</h3>

<p><code>=</code>: equal</p>

<p><code>&lt;&gt;</code>: not equal</p>

<p><code>&gt;=</code>: 以上</p>

<p><code>&gt;</code>: より大きい</p>

<p><code>&lt;=</code>: 以下</p>

<p><code>&lt;</code>: より小さい</p>

<p><code>IS NULL</code>: NULLかどうか判断する</p>

<p><code>IS NOT NULL</code>: NOT NULLかどうか判断する</p>

<p><code>&lt;&gt;</code>では<code>NULL</code>を検索できない.</p>

<h3>論理演算子</h3>

<p><code>NOT</code>:</p>

<p><code>AND</code>:</p>

<p><code>OR</code>:</p>

<p><code>AND</code>は<code>OR</code>よりも優先度が高い.</p>

<p><code>OR</code>を優先する場合は、<code>()</code>で囲むこと.</p>

<p><code>TRUE</code>:</p>

<p><code>FALSE</code>:</p>

<p><code>UNKNOWN</code>: 真でも偽でもない場合の値.</p>

<h1>3. 集約と並び替え</h1>

<h2>COUNT</h2>

<pre><code>SELECT COUNT(*) AS &quot;個数&quot;
FROM Expense;</code></pre>

<figure><img src="DraggedImage-9.png"/></figure>

<p>特定のカラムを指定すると、<code>NULL</code>の行はカウントされない.</p>

<p><code>COUNT(*)</code>での指定では、<code>NULL</code>を含む行もカウントされる.</p>

<h2>SUM</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-constant">SUM</span>(value)
<span class="syntax-all syntax-keyword">FROM</span> Expense;</code></pre>

<h2>AVG</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-constant">AVG</span>(value)
<span class="syntax-all syntax-keyword">FROM</span> Expense;</code></pre>

<h2>MAX, MIN</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-constant">MAX</span>(value), <span class="syntax-all syntax-constant">MIN</span>(value)
<span class="syntax-all syntax-keyword">FROM</span> Expense;</code></pre>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-constant">MAX</span>(<span class="syntax-all syntax-keyword">date</span>), <span class="syntax-all syntax-constant">MIN</span>(<span class="syntax-all syntax-keyword">date</span>)
<span class="syntax-all syntax-keyword">FROM</span> Expense;</code></pre>

<figure><img src="DraggedImage-10.png"/></figure>

<h2>DISTINCT + 集約関数</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-constant">COUNT</span>((DISTINCT category)
<span class="syntax-all syntax-keyword">FROM</span> Expense;</code></pre>

<figure><img src="DraggedImage-11.png"/></figure>

<h2>グループに切り分ける</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- categoryごとの行数を数える
</span><span class="syntax-all syntax-keyword">SELECT</span> category, <span class="syntax-all syntax-constant">COUNT</span>(<span class="syntax-all syntax-keyword">*</span>)
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">GROUP BY</span> category;</code></pre>

<figure><img src="DraggedImage-12.png"/></figure>

<p><em><code>GROUP BY</code>句は<code>FROM</code>の後ろに書くこと.</em></p>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- WHERE句で絞り込む
</span><span class="syntax-all syntax-keyword">SELECT</span> category, <span class="syntax-all syntax-constant">COUNT</span>(<span class="syntax-all syntax-keyword">*</span>)
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">WHERE</span> value IS <span class="syntax-all syntax-keyword">NULL</span>
<span class="syntax-all syntax-keyword">GROUP BY</span> category;</code></pre>

<figure><img src="DraggedImage-13.png"/></figure>

<h3>注意点</h3>

<ul>
	<li>SELECT文には定数、集約関数、GROUP BY句で指定した列名しか書けない</li>
	<li>GROUP BY句には列の別名は使えない</li>
	<li>GROUP BY句での出力順序はランダム</li>
	<li>WHERE句には集約関数は書かないこと.</li>
</ul>

<h2>集約結果への条件指定</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- 集約結果から指定の条件に合致するデータを抽出する
</span><span class="syntax-all syntax-keyword">SELECT</span> category, <span class="syntax-all syntax-constant">COUNT</span>(<span class="syntax-all syntax-keyword">*</span>)
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">WHERE</span> value IS <span class="syntax-all syntax-keyword">NULL</span>
<span class="syntax-all syntax-keyword">GROUP BY</span> category
<span class="syntax-all syntax-keyword">HAVING</span> <span class="syntax-all syntax-constant">COUNT</span>(<span class="syntax-all syntax-keyword">*</span>) <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-constant">1</span>;</code></pre>

<figure><img src="DraggedImage-14.png"/></figure>

<p><em>集約キーに対する条件指定は、WHEREでもHAVINGのどちらでもできるが、処理速度を考慮すると、WHEREで指定した方がいい</em></p>

<h2>検索結果の並び替え</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">SELECT</span> id, name, <span class="syntax-all syntax-keyword">date</span>
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">ORDER BY</span> <span class="syntax-all syntax-keyword">date</span> <span class="syntax-all syntax-keyword">DESC</span>;</code></pre>

<figure><img src="DraggedImage-15.png"/></figure>

<p><code>ORDER BY</code>句はSELECT文の最後に書くこと.</p>

<p>複数のソートキーの指定もできる.</p>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- SELECT に含まれていない列でもソートキーに指定できる
</span><span class="syntax-all syntax-keyword">SELECT</span> id, name, <span class="syntax-all syntax-keyword">date</span>
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">ORDER BY</span> category <span class="syntax-all syntax-keyword">ASC</span>;</code></pre>

<figure><img src="DraggedImage-16.png"/></figure>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- 集約関数もソートキーに指定できる
</span><span class="syntax-all syntax-keyword">SELECT</span> category, <span class="syntax-all syntax-constant">COUNT</span>(<span class="syntax-all syntax-keyword">*</span>)
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">GROUP BY</span> category
<span class="syntax-all syntax-keyword">ORDER BY</span> <span class="syntax-all syntax-constant">COUNT</span>(<span class="syntax-all syntax-keyword">*</span>);</code></pre>

<figure><img src="DraggedImage-17.png"/></figure>

<p>売値の合計が買値の合計の2/3以上の金額のcategoryを抜き出す.</p>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">SELECT</span> category, <span class="syntax-all syntax-constant">SUM</span>(value), <span class="syntax-all syntax-constant">SUM</span>(sell)
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">GROUP BY</span> category
<span class="syntax-all syntax-keyword">HAVING</span> <span class="syntax-all syntax-constant">SUM</span>(sell) <span class="syntax-all syntax-keyword">&gt;</span> <span class="syntax-all syntax-constant">SUM</span>(value)<span class="syntax-all syntax-keyword">/</span><span class="syntax-all syntax-constant">1</span>.<span class="syntax-all syntax-constant">5</span>;</code></pre>

<figure><img src="DraggedImage-18.png"/><img src="DraggedImage-19.png"/></figure>

<h1>4. データの更新</h1>

<h2>INSERT</h2>

<h3>DEFAULT値の指定</h3>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">CREATE</span> <span class="syntax-all syntax-keyword">TABLE</span> <span class="syntax-all syntax-entity">Sample</span>
(id <span class="syntax-all syntax-keyword">CHAR</span>(<span class="syntax-all syntax-constant">4</span>) <span class="syntax-all syntax-keyword">NOT NULL</span>,
 value <span class="syntax-all syntax-keyword">INTEGER</span> DEFAULT <span class="syntax-all syntax-constant">0</span>,
 ...
);

<span class="syntax-all syntax-keyword">INSERT INTO</span> Sample <span class="syntax-all syntax-keyword">VALUES</span> (<span class="syntax-all syntax-string">&#39;0001&#39;</span>, DEFAULT); <span class="syntax-all syntax-comment">-- valueには0が挿入される
</span></code></pre>

<p><mark>DEFAULT値のINSERTがうまくいかなかった</mark></p>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">INSERT INTO</span> ExpenseIns (id, category, name) <span class="syntax-all syntax-keyword">VALUES</span> (<span class="syntax-all syntax-string">&#39;0002&#39;</span>, <span class="syntax-all syntax-string">&#39;gadget&#39;</span>, <span class="syntax-all syntax-string">&#39;iPad&#39;</span>)
<span class="syntax-all syntax-comment">-- INSERTの指定から除外したカラムは、デフォルト値が挿入される
</span></code></pre>

<figure><img src="DraggedImage-20.png"/></figure>

<h3>別テーブルからのインサート</h3>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">INSERT INTO</span> ExpenseInsCopy
<span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-keyword">*</span>
<span class="syntax-all syntax-keyword">FROM</span> ExpenseIns
<span class="syntax-all syntax-keyword">WHERE</span> id <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-string">&#39;0001&#39;</span>;</code></pre>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- GROUP BYを使う
</span><span class="syntax-all syntax-keyword">INSERT INTO</span> ExpneseInsCopy
<span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-keyword">*</span>
<span class="syntax-all syntax-keyword">FROM</span> ExpenseIns
<span class="syntax-all syntax-keyword">GROUP BY</span> category
<span class="syntax-all syntax-keyword">HAVING</span> category <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-string">&#39;book&#39;</span>;</code></pre>

<h2>DELETE</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">--テーブルは残したまま、データを削除する
</span><span class="syntax-all syntax-keyword">DELETE</span> <span class="syntax-all syntax-keyword">FROM</span> Expense;</code></pre>

<p>DELETE文で使える制御構文はWHERE句のみ.</p>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- テーブルそのものを削除する
</span><span class="syntax-all syntax-keyword">DROP</span> <span class="syntax-all syntax-keyword">TABLE</span> Expense;</code></pre>

<h2>UPDATE</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- データを更新する
</span><span class="syntax-all syntax-keyword">UPDATE</span> Expense <span class="syntax-all syntax-keyword">SET</span> value <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-constant">2000</span>
<span class="syntax-all syntax-keyword">WHERE</span> category <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-string">&#39;book&#39;</span>;</code></pre>

<p>データを指定しない場合、全てのデータが更新される.</p>

<h2>トランザクション</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">BEGIN</span> TRANSACTION;

<span class="syntax-all syntax-keyword">CREATE</span> <span class="syntax-all syntax-keyword">TABLE</span> <span class="syntax-all syntax-entity">Sample</span>
(id <span class="syntax-all syntax-keyword">INTEGER</span> <span class="syntax-all syntax-keyword">NOT NULL</span>,
 name <span class="syntax-all syntax-keyword">VARCHAR</span>(<span class="syntax-all syntax-constant">100</span>)
 );

<span class="syntax-all syntax-keyword">INSERT INTO</span> Sample <span class="syntax-all syntax-keyword">VALUES</span> (<span class="syntax-all syntax-constant">1</span>, <span class="syntax-all syntax-string">&#39;sample name&#39;</span>);
<span class="syntax-all syntax-keyword">INSERT INTO</span> Sample <span class="syntax-all syntax-keyword">VALUES</span> (<span class="syntax-all syntax-constant">2</span>, <span class="syntax-all syntax-string">&#39;next sample&#39;</span>);

<span class="syntax-all syntax-keyword">COMMIT</span>;</code></pre>

<figure><img src="DraggedImage-21.png"/></figure>

<h3>Rollback</h3>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">BEGIN</span> TRANSACTION;

<span class="syntax-all syntax-keyword">CREATE</span> <span class="syntax-all syntax-keyword">TABLE</span> <span class="syntax-all syntax-entity">Sample2</span>
(id <span class="syntax-all syntax-keyword">INTEGER</span> <span class="syntax-all syntax-keyword">NOT NULL</span>,
 name <span class="syntax-all syntax-keyword">VARCHAR</span>(<span class="syntax-all syntax-constant">100</span>)
 );

<span class="syntax-all syntax-keyword">INSERT INTO</span> sample2 <span class="syntax-all syntax-keyword">VALUES</span> (<span class="syntax-all syntax-constant">1</span>, <span class="syntax-all syntax-string">&#39;sample name&#39;</span>);
<span class="syntax-all syntax-keyword">INSERT INTO</span> sample2 <span class="syntax-all syntax-keyword">VALUES</span> (<span class="syntax-all syntax-constant">2</span>, <span class="syntax-all syntax-string">&#39;next sample&#39;</span>);

<span class="syntax-all syntax-keyword">ROLLBACK</span>;</code></pre>

<p><code>ROLLBACK</code>で全てのクエリが取り消される.</p>

<h3>ACID特性</h3>

<p><mark>割愛</mark></p>

<h1>5. 複雑な問合せ</h1>

<h2>ビューとテーブル</h2>

<p>ビューは、SELECT文を保存するだけで、データを保存はしない.</p>

<p>ビューを使うことで、容量の節約を図れる.</p>

<h3>ビューを作成する</h3>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">CREATE</span> <span class="syntax-all syntax-keyword">VIEW</span> <span class="syntax-all syntax-entity">SampleView</span> (category, cat_sum)
<span class="syntax-all syntax-keyword">AS</span>
<span class="syntax-all syntax-keyword">SELECT</span> category, <span class="syntax-all syntax-constant">SUM</span>(value)
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">GROUP BY</span> category;</code></pre>

<figure><img src="DraggedImage-22.png"/></figure>

<h3>ビューを使う</h3>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">SELECT</span> category, cat_sum
<span class="syntax-all syntax-keyword">FROM</span> SampleView;</code></pre>

<figure><img src="DraggedImage-23.png"/></figure>

<p>一度ビューを作っておけば、あとは簡単なSELECT文によって、いつでも集計結果を得られるようになる.</p>

<p>多段ビューの作成も可能だが、パフォーマンスの低下を招くため、極力行わないようにする.</p>

<h3>ビューの注意事項</h3>

<ul>
	<li>ORDER BY句だけは使えない</li>
	<li>集約したビューに対しては、テーブルの更新はできない.</li>
</ul>

<h3>ビューの削除</h3>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">DROP</span> <span class="syntax-all syntax-keyword">VIEW</span> SampleView;</code></pre>

<h2>サブクエリ</h2>

<p>使い捨てのビューのこと.</p>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- FROM句に直接ビュー定義のSELECT文を書く
</span><span class="syntax-all syntax-keyword">SELECT</span> category, cat_sum
<span class="syntax-all syntax-keyword">FROM</span> (
<span class="syntax-all syntax-keyword">SELECT</span> category, <span class="syntax-all syntax-constant">SUM</span>(value) <span class="syntax-all syntax-keyword">AS</span> cat_sum
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">GROUP BY</span> category
) <span class="syntax-all syntax-keyword">AS</span> SampleView;</code></pre>

<figure><img src="DraggedImage-24.png"/></figure>

<p>サブクエリの場合、ビュー<code>SampleView</code>は保存されない.</p>

<h2>スカラ・サブクエリ</h2>

<p>スカラとは、「単一の」という意味.</p>

<p>スカラサブクエリは、必ず1行1列のだけの戻り値を返す.</p>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">--平均よりもvalueが大きなデータを返す
</span><span class="syntax-all syntax-keyword">SELECT</span> id, name, category, value
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">WHERE</span> value <span class="syntax-all syntax-keyword">&gt;</span> (<span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-constant">AVG</span>(value) <span class="syntax-all syntax-keyword">FROM</span> Expense);</code></pre>

<figure><img src="DraggedImage-25.png"/></figure>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- 全データの平均値をカラムに追加したビューを作成する
</span><span class="syntax-all syntax-keyword">SELECT</span> id, name, category, value, 
(<span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-constant">AVG</span>(value) <span class="syntax-all syntax-keyword">FROM</span> Expense <span class="syntax-all syntax-keyword">AS</span> avg_value) <span class="syntax-all syntax-keyword">AS</span> AVG
<span class="syntax-all syntax-keyword">FROM</span> Expense <span class="syntax-all syntax-keyword">AS</span> SampleView;</code></pre>

<figure><img src="DraggedImage-26.png"/></figure>

<p>スカラ値がかける場所にはどこにでもスカラサブクエリを書くことができる.</p>

<h3>スカラサブクエリの注意点</h3>

<ul>
	<li>絶対にサブクエリが複数行を返さないようにすること.</li>
</ul>

<h2>相関サブクエリ</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- categoryごとの平均金額を上回るレコードを抽出する
</span><span class="syntax-all syntax-keyword">SELECT</span> category, name, value, 
<span class="syntax-all syntax-keyword">FROM</span> Expense <span class="syntax-all syntax-keyword">AS</span> E1
<span class="syntax-all syntax-keyword">WHERE</span> value <span class="syntax-all syntax-keyword">&gt;</span> (
<span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-constant">AVG</span>(value)
<span class="syntax-all syntax-keyword">FROM</span> Expense <span class="syntax-all syntax-keyword">AS</span> E2
<span class="syntax-all syntax-keyword">WHERE</span> <span class="syntax-all syntax-constant">E1</span>.<span class="syntax-all syntax-constant">category</span> <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-constant">E2</span>.<span class="syntax-all syntax-constant">category</span>
<span class="syntax-all syntax-keyword">GROUP BY</span> category
);</code></pre>

<figure><img src="DraggedImage-27.png"/></figure>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- categoryごとの平均valueをカラムに追加したビューを作成する
</span><span class="syntax-all syntax-keyword">SELECT</span> id, name, category, value, (<span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-constant">AVG</span>(value) <span class="syntax-all syntax-keyword">FROM</span> Expense <span class="syntax-all syntax-keyword">AS</span> E2 <span class="syntax-all syntax-keyword">WHERE</span> <span class="syntax-all syntax-constant">E1</span>.<span class="syntax-all syntax-constant">category</span> <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-constant">E2</span>.<span class="syntax-all syntax-constant">category</span> <span class="syntax-all syntax-keyword">GROUP BY</span> category) <span class="syntax-all syntax-keyword">AS</span> cat_avg
<span class="syntax-all syntax-keyword">FROM</span> Expense <span class="syntax-all syntax-keyword">AS</span> E1;</code></pre>

<figure><img src="DraggedImage-28.png"/></figure>

<h1>6. 関数、述語、CASE文</h1>

<h2>関数</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- 絶対値
</span><span class="syntax-all syntax-keyword">SELECT</span> name, ABS(value) <span class="syntax-all syntax-keyword">AS</span> abs_value
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">WHERE</span> category <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-string">&#39;book&#39;</span>;</code></pre>

<figure><img src="DraggedImage-29.png"/></figure>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- 剰余
</span><span class="syntax-all syntax-keyword">SELECT</span> name, MOD(value, <span class="syntax-all syntax-constant">3</span>) <span class="syntax-all syntax-keyword">AS</span> mod
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">WHERE</span> category <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-string">&#39;book&#39;</span>;</code></pre>

<figure><img src="DraggedImage-30.png"/></figure>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- 四捨五入
</span><span class="syntax-all syntax-keyword">SELECT</span> name, ROUND(value) <span class="syntax-all syntax-keyword">AS</span> round
<span class="syntax-all syntax-keyword">FROM</span> Expense;</code></pre>

<h2>文字列関数</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- 連結
</span><span class="syntax-all syntax-keyword">SELECT</span> name <span class="syntax-all syntax-keyword">||</span> <span class="syntax-all syntax-string">&quot; | &quot;</span> <span class="syntax-all syntax-keyword">||</span> category <span class="syntax-all syntax-keyword">AS</span> concat
<span class="syntax-all syntax-keyword">FROM</span> Expense;</code></pre>

<figure><img src="DraggedImage-31.png"/></figure>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- 文字列の長さ
</span><span class="syntax-all syntax-keyword">SELECT</span> name, LENGTH(name) <span class="syntax-all syntax-keyword">AS</span> len
<span class="syntax-all syntax-keyword">FROM</span> Expense;</code></pre>

<figure><img src="DraggedImage-32.png"/></figure>

<p>スペースも1文字にカウントされる.</p>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- 小文字化(LOWER), 大文字化(UPPER)
</span><span class="syntax-all syntax-keyword">SELECT</span> name, <span class="syntax-all syntax-constant">UPPER</span>(name) <span class="syntax-all syntax-keyword">AS</span> <span class="syntax-all syntax-constant">upper</span>, <span class="syntax-all syntax-constant">LOWER</span>(name) <span class="syntax-all syntax-keyword">AS</span> <span class="syntax-all syntax-constant">LOWER</span>
<span class="syntax-all syntax-keyword">FROM</span> Expense;</code></pre>

<figure><img src="DraggedImage-33.png"/></figure>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- 文字の置換
</span><span class="syntax-all syntax-keyword">SELECT</span> name, category, REPLACE(category, <span class="syntax-all syntax-string">&quot;book&quot;</span>, <span class="syntax-all syntax-string">&quot;document&quot;</span>) <span class="syntax-all syntax-keyword">AS</span> rep
<span class="syntax-all syntax-keyword">FROM</span> Expense;</code></pre>

<p><code>REPLACE(対象文字列, 置換前の文字列, 置換後の文字列)</code></p>

<figure><img src="DraggedImage-34.png"/></figure>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- 文字列の切り出し
</span><span class="syntax-all syntax-keyword">SELECT</span> name, <span class="syntax-all syntax-constant">SUBSTRING</span>(
name <span class="syntax-all syntax-keyword">FROM</span> <span class="syntax-all syntax-constant">0</span> FOR <span class="syntax-all syntax-constant">3</span>
)
<span class="syntax-all syntax-keyword">FROM</span> Expense;</code></pre>

<p><code>SUBSTRING(対象文字列 FROM 切り出し開始位置 FOR 切り出す文字数)</code></p>

<p><mark>sqliteでは使えない</mark></p>

<h2>日付関数</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- 現在の日付
</span><span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-constant">CURRENT_DATE</span> <span class="syntax-all syntax-keyword">AS</span> today;</code></pre>

<figure><img src="DraggedImage-35.png"/></figure>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- 現在の時間
</span><span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-constant">CURRENT_TIME</span> <span class="syntax-all syntax-keyword">AS</span> now;</code></pre>

<figure><img src="DraggedImage-36.png"/></figure>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- 現在の日時
</span><span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-constant">CURRENT_TIMESTAMP</span> <span class="syntax-all syntax-keyword">AS</span> now;</code></pre>

<figure><img src="DraggedImage-37.png"/></figure>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- 日付要素の切り出し
</span><span class="syntax-all syntax-keyword">SELECT</span> EXTRACT(YEAR <span class="syntax-all syntax-keyword">FROM</span> <span class="syntax-all syntax-constant">CURRENT_TIMESTAMP</span>) <span class="syntax-all syntax-keyword">AS</span> year;</code></pre>

<p><mark>sqliteでは使えない</mark></p>

<h2>変換関数</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- 型変換
</span><span class="syntax-all syntax-keyword">SELECT</span> CAST(value <span class="syntax-all syntax-keyword">AS</span> <span class="syntax-all syntax-keyword">VARCHAR</span>(<span class="syntax-all syntax-constant">100</span>)) <span class="syntax-all syntax-keyword">AS</span> var_value
<span class="syntax-all syntax-keyword">FROM</span> Expense;</code></pre>

<figure><img src="DraggedImage-38.png"/></figure>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- NULLを値に変換
</span><span class="syntax-all syntax-comment">-- 最初のNULLではない引数を返す
</span><span class="syntax-all syntax-keyword">SELECT</span> COALESCE(<span class="syntax-all syntax-keyword">NULL</span>, <span class="syntax-all syntax-constant">1</span>) <span class="syntax-all syntax-keyword">AS</span> col_1,
COALESCE(<span class="syntax-all syntax-keyword">NULL</span>, <span class="syntax-all syntax-string">&#39;test&#39;</span>, <span class="syntax-all syntax-keyword">NULL</span>) <span class="syntax-all syntax-keyword">AS</span> col_2,
COALESCE(<span class="syntax-all syntax-keyword">NULL</span>, <span class="syntax-all syntax-keyword">NULL</span>, <span class="syntax-all syntax-string">&#39;2020-01-04&#39;</span>) <span class="syntax-all syntax-keyword">AS</span> col_3;</code></pre>

<figure><img src="DraggedImage-39.png"/></figure>

<p><code>NULL</code>を他の値に変換するために使われることが多い.</p>

<h2>述語</h2>

<ul>
	<li>述語とは、戻り値が真理値になる関数のこと</li>
</ul>

<h3>LIKE</h3>

<h4>前方一致</h4>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- 前方一致
</span><span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-keyword">*</span>
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">WHERE</span> name <span class="syntax-all syntax-keyword">LIKE</span> <span class="syntax-all syntax-string">&#39;harry%&#39;</span>;
<span class="syntax-all syntax-comment">-- nameの先頭に harryを含むレコード
</span></code></pre>

<figure><img src="DraggedImage-40.png"/></figure>

<p><code>%</code>: 0文字以上の任意の文字列</p>

<p><code>_</code>: 任意の1文字</p>

<h4>中間一致</h4>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- 中間一致
</span><span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-keyword">*</span>
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">WHERE</span> name <span class="syntax-all syntax-keyword">LIKE</span> <span class="syntax-all syntax-string">&#39;%pot%&#39;</span>;</code></pre>

<figure><img src="DraggedImage-41.png"/></figure>

<h4>後方一致</h4>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- 後方一致
</span><span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-keyword">*</span>
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">WHERE</span> name <span class="syntax-all syntax-keyword">LIKE</span> <span class="syntax-all syntax-string">&#39;%harry&#39;</span>;</code></pre>

<h3>BETWEEN</h3>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">SELECT</span> name, value
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">WHERE</span> value BETWEEN <span class="syntax-all syntax-constant">2000</span> <span class="syntax-all syntax-keyword">AND</span> <span class="syntax-all syntax-constant">3000</span>;
<span class="syntax-all syntax-comment">-- 2000, 3000も含む
</span></code></pre>

<figure><img src="DraggedImage-42.png"/></figure>

<h3>IS NULL, IS NOT NULL</h3>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- IS NULL
</span><span class="syntax-all syntax-keyword">SELECT</span> name, category
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">WHERE</span> category IS <span class="syntax-all syntax-keyword">NULL</span>;</code></pre>

<figure><img src="DraggedImage-43.png"/></figure>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- IS NOT NULL
</span><span class="syntax-all syntax-keyword">SELECT</span> name, category
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">WHERE</span> category <span class="syntax-all syntax-keyword">IS NOT NULL</span>;</code></pre>

<figure><img src="DraggedImage-44.png"/></figure>

<h3>IN</h3>

<p>ORの省略形として使う</p>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- OR
</span><span class="syntax-all syntax-keyword">SELECT</span> name, category, value
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">WHERE</span> value <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-constant">2000</span> <span class="syntax-all syntax-keyword">OR</span> value <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-constant">3000</span>;</code></pre>

<figure><img src="DraggedImage-45.png"/></figure>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- IN
</span><span class="syntax-all syntax-keyword">SELECT</span> name, category, value
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">WHERE</span> value <span class="syntax-all syntax-keyword">IN</span> (<span class="syntax-all syntax-constant">2000</span>, <span class="syntax-all syntax-constant">3000</span>);</code></pre>

<figure><img src="DraggedImage-46.png"/></figure>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- NOT IN
</span><span class="syntax-all syntax-keyword">SELECT</span> name, category, value
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">WHERE</span> value NOT <span class="syntax-all syntax-keyword">IN</span> (<span class="syntax-all syntax-constant">2000</span>, <span class="syntax-all syntax-constant">3000</span>);</code></pre>

<figure><img src="DraggedImage-47.png"/></figure>

<h4>INとサブクエリ</h4>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- ExpenseInsのカテゴリに存在するカテゴリのみを抜き出す
</span><span class="syntax-all syntax-keyword">SELECT</span> name, category, value
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">WHERE</span> category <span class="syntax-all syntax-keyword">IN</span> (<span class="syntax-all syntax-keyword">SELECT</span> category <span class="syntax-all syntax-keyword">FROM</span> ExpenseINS);</code></pre>

<figure><img src="DraggedImage-48.png"/></figure>

<figure><img src="DraggedImage-49.png"/></figure>

<p>bookとgadgetだけ抜きだせた.</p>

<h3>EXISTS</h3>

<p><code>EXISTS</code>を使わなくても<code>IN</code>, <code>NOT IN</code>でほぼ代用できる</p>

<p><code>EXIST</code>の引数は常に相関サブクエリを指定すること.</p>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- ExpenseInsと同じ名前のレコードのvalueの合計値を表示する
</span><span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-constant">SUM</span>(value)
<span class="syntax-all syntax-keyword">FROM</span> Expense <span class="syntax-all syntax-keyword">AS</span> E1
<span class="syntax-all syntax-keyword">WHERE</span> EXISTS (
  <span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-keyword">*</span>
  <span class="syntax-all syntax-keyword">FROM</span> ExpenseIns <span class="syntax-all syntax-keyword">AS</span> E2
  <span class="syntax-all syntax-keyword">WHERE</span> <span class="syntax-all syntax-constant">E1</span>.<span class="syntax-all syntax-constant">name</span> <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-constant">E2</span>.<span class="syntax-all syntax-constant">name</span>
);</code></pre>

<figure><img src="DraggedImage-50.png"/></figure>

<h2>CASE式</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- CASE
</span><span class="syntax-all syntax-keyword">SELECT</span> name,
	CASE WHEN category <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-string">&quot;book&quot;</span>
				THEN <span class="syntax-all syntax-string">&#39;A:&#39;</span> <span class="syntax-all syntax-keyword">||</span> category
			WHEN category <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-string">&quot;gadget&quot;</span>
				THEN <span class="syntax-all syntax-string">&#39;B:&#39;</span> <span class="syntax-all syntax-keyword">||</span> category
			ELSE <span class="syntax-all syntax-keyword">NULL</span>
  END <span class="syntax-all syntax-keyword">AS</span> category_index
<span class="syntax-all syntax-keyword">FROM</span> Expense;</code></pre>

<figure><img src="DraggedImage-51.png"/></figure>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- categoryごとに合計したvalueを列で表示する
</span><span class="syntax-all syntax-keyword">SELECT</span> 
<span class="syntax-all syntax-constant">SUM</span>(CASE WHEN category <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-string">&#39;book&#39;</span>
	THEN value
	ELSE <span class="syntax-all syntax-constant">0</span>
  END
) <span class="syntax-all syntax-keyword">AS</span> book_sum,
<span class="syntax-all syntax-constant">SUM</span>(CASE WHEN category <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-string">&#39;gadget&#39;</span>
	THEN value
	ELSE <span class="syntax-all syntax-constant">0</span>
  END
) <span class="syntax-all syntax-keyword">AS</span> gadget_sum
<span class="syntax-all syntax-keyword">FROM</span> Expense;</code></pre>

<figure><img src="DraggedImage-52.png"/></figure>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- Expenseテーブルから、valueのレンジによって分類してその個数を返す
</span><span class="syntax-all syntax-keyword">SELECT</span> 
<span class="syntax-all syntax-constant">COUNT</span>(
  CASE WHEN value <span class="syntax-all syntax-keyword">&lt;</span> <span class="syntax-all syntax-constant">2000</span> 
		THEN value
		END
) <span class="syntax-all syntax-keyword">AS</span> low,
<span class="syntax-all syntax-constant">COUNT</span>(
  CASE WHEN (value <span class="syntax-all syntax-keyword">&gt;=</span> <span class="syntax-all syntax-constant">2000</span>) <span class="syntax-all syntax-keyword">AND</span> (value <span class="syntax-all syntax-keyword">&lt;</span> <span class="syntax-all syntax-constant">3000</span>)
	THEN value
	END
) <span class="syntax-all syntax-keyword">AS</span> mid,
<span class="syntax-all syntax-constant">COUNT</span>(
  CASE WHEN value <span class="syntax-all syntax-keyword">&gt;=</span> <span class="syntax-all syntax-constant">3000</span>
	THEN value
	END
) <span class="syntax-all syntax-keyword">AS</span> high
<span class="syntax-all syntax-keyword">FROM</span> Expense;</code></pre>

<figure><img src="DraggedImage-53.png"/></figure>

<h1>7. 集合演算</h1>

<h2>UNION(和)</h2>

<ul>
	<li>Expense</li>
</ul>

<figure><img src="DraggedImage-54.png"/></figure>

<ul>
	<li>ExpenseCp</li>
</ul>

<figure><img src="DraggedImage-55.png"/></figure>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- テーブルの足し算
</span><span class="syntax-all syntax-keyword">SELECT</span> id, name, value
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">UNION</span>
<span class="syntax-all syntax-keyword">SELECT</span> id, name, value
<span class="syntax-all syntax-keyword">FROM</span> ExpenseCp;</code></pre>

<figure><img src="DraggedImage-56.png"/></figure>

<h3>注意点</h3>

<ul>
	<li>演算対象のテーブルの列数は同じであること</li>
	<li>演算対象のレコードの列のデータ型が一致していること</li>
	<li>ORDER BY句は最後に一つだけ.</li>
</ul>

<h2>ALL</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- 重複行を排除しない場合
</span><span class="syntax-all syntax-keyword">SELECT</span> id, name, value
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">UNION ALL</span>
<span class="syntax-all syntax-keyword">SELECT</span> id, name, value
<span class="syntax-all syntax-keyword">FROM</span> ExpenseCp;</code></pre>

<h2>INTERSECT</h2>

<p>2つのレコードの共通部分を選択する.</p>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">SELECT</span> name, id, value
<span class="syntax-all syntax-keyword">FROM</span> Expense
INTERSECT
<span class="syntax-all syntax-keyword">SELECT</span> name, id, value
<span class="syntax-all syntax-keyword">FROM</span> ExpenseCp;</code></pre>

<p>何も表示されない.</p>

<p>共通のレコードを挿入してみる.</p>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">INSERT INTO</span> Expense <span class="syntax-all syntax-keyword">VALUES</span>(<span class="syntax-all syntax-string">&#39;009&#39;</span>, <span class="syntax-all syntax-string">&#39;MAC&#39;</span>, <span class="syntax-all syntax-string">&#39;gadget&#39;</span>, <span class="syntax-all syntax-string">&#39;2022-06-01&#39;</span>, <span class="syntax-all syntax-constant">1500</span>, <span class="syntax-all syntax-constant">800</span>);
<span class="syntax-all syntax-keyword">INSERT INTO</span> ExpenseCp <span class="syntax-all syntax-keyword">VALUES</span>(<span class="syntax-all syntax-string">&#39;009&#39;</span>, <span class="syntax-all syntax-string">&#39;MAC&#39;</span>, <span class="syntax-all syntax-string">&#39;gadget&#39;</span>, <span class="syntax-all syntax-string">&#39;2022-06-01&#39;</span>, <span class="syntax-all syntax-constant">1500</span>, <span class="syntax-all syntax-constant">800</span>);</code></pre>

<figure><img src="DraggedImage-57.png"/></figure>

<h2>EXCEPT</h2>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">SELECT</span> name, id, value
<span class="syntax-all syntax-keyword">FROM</span> Expense
EXCEPT
<span class="syntax-all syntax-keyword">SELECT</span> name, id, value
<span class="syntax-all syntax-keyword">FROM</span> ExpenseCp;</code></pre>

<figure><img src="DraggedImage-58.png"/></figure>

<h2>結合 JOIN</h2>

<p>別テーブルから列を持ってきて「列を増やす」操作.</p>

<h3>INNER JOIN</h3>

<ul>
	<li>SellList</li>
</ul>

<figure><img src="DraggedImage-59.png"/></figure>

<ul>
	<li>BookInfo</li>
</ul>

<figure><img src="DraggedImage-60.png"/></figure>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- テーブルの結合
</span><span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-constant">BI</span>.<span class="syntax-all syntax-constant">id</span>, <span class="syntax-all syntax-constant">BI</span>.<span class="syntax-all syntax-constant">title</span>, <span class="syntax-all syntax-constant">BI</span>.<span class="syntax-all syntax-constant">author</span>, <span class="syntax-all syntax-constant">S</span>.<span class="syntax-all syntax-constant">value</span>
<span class="syntax-all syntax-keyword">FROM</span> BookInfo <span class="syntax-all syntax-keyword">AS</span> BI <span class="syntax-all syntax-keyword">INNER JOIN</span> SellList <span class="syntax-all syntax-keyword">AS</span> SL
  <span class="syntax-all syntax-keyword">ON</span> <span class="syntax-all syntax-constant">BI</span>.<span class="syntax-all syntax-constant">id</span> <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-constant">SL</span>.<span class="syntax-all syntax-constant">id</span>;</code></pre>

<figure><img src="DraggedImage-61.png"/></figure>

<h3>OUTER JOIN</h3>

<p>どちらか一方のテーブルに存在するなら全て出力する.</p>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- テーブルの結合
</span><span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-constant">BI</span>.<span class="syntax-all syntax-constant">id</span>, <span class="syntax-all syntax-constant">BI</span>.<span class="syntax-all syntax-constant">title</span>, <span class="syntax-all syntax-constant">BI</span>.<span class="syntax-all syntax-constant">author</span>, <span class="syntax-all syntax-constant">SL</span>.<span class="syntax-all syntax-constant">value</span>
<span class="syntax-all syntax-keyword">FROM</span> BookInfo <span class="syntax-all syntax-keyword">AS</span> BI <span class="syntax-all syntax-keyword">LEFT OUTER JOIN</span> SellList <span class="syntax-all syntax-keyword">AS</span> SL
<span class="syntax-all syntax-keyword">ON</span> <span class="syntax-all syntax-constant">Bi</span>.<span class="syntax-all syntax-constant">id</span> <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-constant">SL</span>.<span class="syntax-all syntax-constant">id</span>;</code></pre>

<p><em><code>RIGHT OUTER JOIN</code>はサポートしていないらしい</em></p>

<p><code>LEFT OUTER JOIN</code> の場合、左側に指定したテーブル(この場合はBookInfo)をマスタとする.</p>

<p>マスタにしか存在しないレコードも出力する.</p>

<figure><img src="DraggedImage-62.png"/></figure>

<h3>3つのテーブルの結合</h3>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-constant">BI</span>.<span class="syntax-all syntax-constant">id</span>, <span class="syntax-all syntax-constant">BI</span>.<span class="syntax-all syntax-constant">title</span>, <span class="syntax-all syntax-constant">BI</span>.<span class="syntax-all syntax-constant">author</span>, <span class="syntax-all syntax-constant">SL1</span>.<span class="syntax-all syntax-constant">value</span> <span class="syntax-all syntax-keyword">AS</span> value1, <span class="syntax-all syntax-constant">SL2</span>.<span class="syntax-all syntax-constant">value</span> <span class="syntax-all syntax-keyword">AS</span> value2
<span class="syntax-all syntax-keyword">FROM</span> BookInfo <span class="syntax-all syntax-keyword">AS</span> BI <span class="syntax-all syntax-keyword">LEFT OUTER JOIN</span> SellList <span class="syntax-all syntax-keyword">AS</span> SL1
  <span class="syntax-all syntax-keyword">ON</span> <span class="syntax-all syntax-constant">BI</span>.<span class="syntax-all syntax-constant">id</span> <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-constant">SL1</span>.<span class="syntax-all syntax-constant">id</span>
	<span class="syntax-all syntax-keyword">INNER JOIN</span> SellList2 <span class="syntax-all syntax-keyword">AS</span> SL2
  <span class="syntax-all syntax-keyword">ON</span> <span class="syntax-all syntax-constant">BI</span>.<span class="syntax-all syntax-constant">id</span> <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-constant">SL2</span>.<span class="syntax-all syntax-constant">id</span>;</code></pre>

<figure><img src="DraggedImage-63.png"/></figure>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- NULLを不明に置き換え
</span><span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-constant">BI</span>.<span class="syntax-all syntax-constant">id</span>, <span class="syntax-all syntax-constant">BI</span>.<span class="syntax-all syntax-constant">title</span>, <span class="syntax-all syntax-constant">BI</span>.<span class="syntax-all syntax-constant">author</span>, COALESCE(<span class="syntax-all syntax-constant">SL1</span>.<span class="syntax-all syntax-constant">value</span>, <span class="syntax-all syntax-string">&quot;不明&quot;</span>) <span class="syntax-all syntax-keyword">AS</span> value1, <span class="syntax-all syntax-constant">SL2</span>.<span class="syntax-all syntax-constant">value</span> <span class="syntax-all syntax-keyword">AS</span> value2
<span class="syntax-all syntax-keyword">FROM</span> BookInfo <span class="syntax-all syntax-keyword">AS</span> BI <span class="syntax-all syntax-keyword">LEFT OUTER JOIN</span> SellList <span class="syntax-all syntax-keyword">AS</span> SL1
  <span class="syntax-all syntax-keyword">ON</span> <span class="syntax-all syntax-constant">BI</span>.<span class="syntax-all syntax-constant">id</span> <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-constant">SL1</span>.<span class="syntax-all syntax-constant">id</span>
	<span class="syntax-all syntax-keyword">INNER JOIN</span> SellList2 <span class="syntax-all syntax-keyword">AS</span> SL2
  <span class="syntax-all syntax-keyword">ON</span> <span class="syntax-all syntax-constant">BI</span>.<span class="syntax-all syntax-constant">id</span> <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-constant">SL2</span>.<span class="syntax-all syntax-constant">id</span>;</code></pre>

<figure><img src="DraggedImage-64.png"/></figure>

<h3>クロス結合 CROSS JOIN</h3>

<p><mark>基本的に実務では使わない</mark></p>

<h1>8. 高度な処理</h1>

<h2>ウィンドウ関数</h2>

<p>OLAP関数とも呼ばれる.</p>

<p>ウィンドウ関数はSELECT句の中でしか使えない.</p>

<h3>RANK関数</h3>

<p>ランキングの算出.</p>

<pre><code class="code-highlighted code-ruby"><span class="syntax-all syntax-keyword">--</span> category内でのランキングを安い順に表示
<span class="syntax-all syntax-constant">SELECT</span> name, category, value,
  <span class="syntax-all syntax-constant">RANK</span> () <span class="syntax-all syntax-constant">OVER</span> ( <span class="syntax-all syntax-constant">PARTITION</span> <span class="syntax-all syntax-constant">BY</span> category <span class="syntax-all syntax-constant">ORDER</span> <span class="syntax-all syntax-constant">BY</span> value) <span class="syntax-all syntax-constant">AS</span> ranking
<span class="syntax-all syntax-constant">FROM</span> <span class="syntax-all syntax-constant">Expense</span>;</code></pre>

<figure><img src="DraggedImage-65.png"/></figure>

<pre><code class="code-highlighted code-ruby"><span class="syntax-all syntax-keyword">--</span> <span class="syntax-all syntax-constant">PARTITION</span> <span class="syntax-all syntax-constant">BYの指定をしない</span>
<span class="syntax-all syntax-constant">SELECT</span> name, category,value, <span class="syntax-all syntax-constant">RANK</span> () ( <span class="syntax-all syntax-constant">ORDER</span> <span class="syntax-all syntax-constant">BY</span> value) <span class="syntax-all syntax-constant">AS</span> ranking
<span class="syntax-all syntax-constant">FROM</span> <span class="syntax-all syntax-constant">Expense</span>;</code></pre>

<figure><img src="DraggedImage-66.png"/></figure>

<p>テーブル全体での順位に変わった.</p>

<ul>
	<li>DENSE_RANK関数</li>
</ul>

<p>同順位のレコードが存在しても、後続の順位が飛ばない.</p>

<ul>
	<li>ROW_RANK関数</li>
</ul>

<p>一意の連番を付与する.</p>

<h2>SUMをウィンドウ関数で使用する</h2>

<pre><code class="code-highlighted code-ruby"><span class="syntax-all syntax-constant">SELECT</span> id, name, value, <span class="syntax-all syntax-constant">SUM</span> (value) <span class="syntax-all syntax-constant">OVER</span> ( <span class="syntax-all syntax-constant">ORDER</span> <span class="syntax-all syntax-constant">BY</span> id) <span class="syntax-all syntax-constant">AS</span> current_sum
<span class="syntax-all syntax-constant">FROM</span> <span class="syntax-all syntax-constant">Expense</span>;</code></pre>

<figure><img src="DraggedImage-67.png"/></figure>

<p>累積のvalueの合計値が出力される.</p>

<h3>移動平均を算出する</h3>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- 直近の3レコードの平均を表示する
</span><span class="syntax-all syntax-keyword">SELECT</span> id, name, value, <span class="syntax-all syntax-constant">AVG</span> (value) OVER ( <span class="syntax-all syntax-keyword">ORDER BY</span> id, ROWS <span class="syntax-all syntax-constant">2</span> PRECEDING) <span class="syntax-all syntax-keyword">AS</span> moving_avg
<span class="syntax-all syntax-keyword">FROM</span> Expense;</code></pre>

<figure><img src="DraggedImage-68.png"/></figure>

<p><code>PRECEDING</code>: 直前のレコード</p>

<p><code>FOLLOWING</code>: 直後のレコード</p>

<h2>GROUPING演算子</h2>

<p>合計行の算出に使う.</p>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- GROUP BYでは算出できない.
</span><span class="syntax-all syntax-keyword">SELECT</span> category, <span class="syntax-all syntax-constant">SUM</span>(value)
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">GROUP BY</span> category;</code></pre>

<figure><img src="DraggedImage-69.png"/></figure>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- UNION ALLを使う
</span><span class="syntax-all syntax-keyword">SELECT</span> <span class="syntax-all syntax-string">&#39;合計&#39;</span> <span class="syntax-all syntax-keyword">AS</span> category, <span class="syntax-all syntax-constant">SUM</span>(value)
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">UNION ALL</span>
<span class="syntax-all syntax-keyword">SELECT</span> category, <span class="syntax-all syntax-constant">SUM</span>(value)
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">GROUP BY</span> category;</code></pre>

<figure><img src="DraggedImage-70.png"/></figure>

<h3>ROLLUP</h3>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- ROLLUPを使う
</span><span class="syntax-all syntax-keyword">SELECT</span> category, <span class="syntax-all syntax-constant">SUM</span>(value) <span class="syntax-all syntax-keyword">AS</span> sum_value
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">GROUP BY</span> ROLLUP(category);</code></pre>

<p><mark>ROLLUPはsqlite3では実装されていない</mark></p>

<h3>CUBE</h3>

<pre><code class="code-highlighted code-sql"><span class="syntax-all syntax-comment">-- CUBEを使う
</span><span class="syntax-all syntax-keyword">SELECT</span> CASE WHEN GROUPING(category) <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-constant">1</span>
  THEN <span class="syntax-all syntax-string">&quot;商品分類 合計&quot;</span>
  ELSE category END <span class="syntax-all syntax-keyword">AS</span> category,
  CASE WHEN GROUPING(<span class="syntax-all syntax-keyword">date</span>) <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-constant">1</span>
  THEN <span class="syntax-all syntax-string">&quot;登録日合計&quot;</span>
  ELSE CAST(<span class="syntax-all syntax-keyword">date</span> <span class="syntax-all syntax-keyword">AS</span> <span class="syntax-all syntax-keyword">VARCHAR</span>(<span class="syntax-all syntax-constant">20</span>)) END <span class="syntax-all syntax-keyword">AS</span> <span class="syntax-all syntax-keyword">date</span>,
  <span class="syntax-all syntax-constant">SUM</span>(value) <span class="syntax-all syntax-keyword">AS</span> value
<span class="syntax-all syntax-keyword">FROM</span> Expense
<span class="syntax-all syntax-keyword">GROUP BY</span> CUBE(category, <span class="syntax-all syntax-keyword">date</span>) </code></pre>

<p><mark>CUBEはsqlite3では実装されていない</mark></p>

<h3>GROUPING SETS</h3>

<p><mark>sqlite3では実装されていない</mark></p>

<h1>9. データベースへの接続</h1>

<p>Rubyからsqliteに接続して、</p>

<p>Expenseテーブルの作成を行ってみる.</p>

<p>ActiveRecordは使う.</p>

<p>下記の手順でデータベースとの接続は成功.</p>

<pre><code class="code-highlighted code-ruby"><span class="syntax-all syntax-keyword">&gt;</span> <span class="syntax-all syntax-keyword">require</span> <span class="syntax-all syntax-string">&#39;active_record&#39;</span>
<span class="syntax-all syntax-keyword">&gt;</span> database_path <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-string">&quot;./sample.sqlite&quot;</span>
<span class="syntax-all syntax-keyword">&gt;</span> spec <span class="syntax-all syntax-keyword">=</span> { <span class="syntax-all syntax-constant">adapter:</span> <span class="syntax-all syntax-string">&quot;sqlite3&quot;</span>, <span class="syntax-all syntax-constant">database:</span> database_path }
<span class="syntax-all syntax-keyword">&gt;</span> <span class="syntax-all syntax-constant">ActiveRecord</span>::<span class="syntax-all syntax-constant">Base</span>.establish_connection spec
<span class="syntax-all syntax-keyword">&gt;</span> connection <span class="syntax-all syntax-keyword">=</span> <span class="syntax-all syntax-constant">ActiveRecord</span>::<span class="syntax-all syntax-constant">Base</span>.connection
<span class="syntax-all syntax-keyword">&gt;</span> connection.create_table <span class="syntax-all syntax-constant">:tasks</span> <span class="syntax-all syntax-keyword">do</span> |<span class="syntax-all syntax-parameter">t</span>|
	t.column <span class="syntax-all syntax-constant">:name</span>, <span class="syntax-all syntax-constant">:string</span>, <span class="syntax-all syntax-constant">null:</span> <span class="syntax-all syntax-constant">false</span>
	t.column <span class="syntax-all syntax-constant">:content</span>, <span class="syntax-all syntax-constant">:string</span>, <span class="syntax-all syntax-constant">null:</span> <span class="syntax-all syntax-constant">false</span>
	t.timestamps
  <span class="syntax-all syntax-keyword">end</span></code></pre>

<pre><code class="code-highlighted code-ruby">$ sqlite3
<span class="syntax-all syntax-keyword">&gt;</span> .table
tasks
<span class="syntax-all syntax-keyword">&gt;</span> <span class="syntax-all syntax-constant">INSERT</span> <span class="syntax-all syntax-constant">INTO</span> <span class="syntax-all syntax-constant">TASKS</span> <span class="syntax-all syntax-constant">VALUES</span> (<span class="syntax-all syntax-constant">1</span>, <span class="syntax-all syntax-string">&quot;name&quot;</span>, <span class="syntax-all syntax-string">&quot;content&quot;</span>, <span class="syntax-all syntax-string">&quot;2022-01-01&quot;</span>, <span class="syntax-all syntax-string">&quot;2022-02-02&quot;</span>)</code></pre>

<figure><img src="DraggedImage-71.png"/></figure>

<p>せっかくなので、<code>ActiveRecord</code>で生のSQLでクエリを発行してみる.</p>

<pre><code class="code-highlighted code-ruby"><span class="syntax-all syntax-keyword">&gt;</span> <span class="syntax-all syntax-constant">ActiveRecord</span>::<span class="syntax-all syntax-constant">Base</span>.connection.execute <span class="syntax-all syntax-string">&quot;INSERT INTO tasks VALUES(1, &#39;name&#39;, &#39;content&#39;, &#39;2022-01-01&#39;, &#39;2020-03-03&#39;);&quot;</span></code></pre>

<figure><img src="DraggedImage-72.png"/></figure>

<pre><code class="code-highlighted code-ruby"><span class="syntax-all syntax-keyword">&gt;</span> <span class="syntax-all syntax-constant">ActiveRecord</span>::<span class="syntax-all syntax-constant">Base</span>.connection.execute(<span class="syntax-all syntax-string">&quot;SELECT * FROM tasks;&quot;</span>)
=&gt; [{<span class="syntax-all syntax-string">&quot;id&quot;</span>=&gt;<span class="syntax-all syntax-constant">1</span>, <span class="syntax-all syntax-string">&quot;name&quot;</span>=&gt;<span class="syntax-all syntax-string">&quot;name&quot;</span>, <span class="syntax-all syntax-string">&quot;content&quot;</span>=&gt;<span class="syntax-all syntax-string">&quot;content&quot;</span>, <span class="syntax-all syntax-string">&quot;created_at&quot;</span>=&gt;<span class="syntax-all syntax-string">&quot;2022-01-01&quot;</span>, <span class="syntax-all syntax-string">&quot;updated_at&quot;</span>=&gt;<span class="syntax-all syntax-string">&quot;2020-03-03&quot;</span>}]</code></pre>


