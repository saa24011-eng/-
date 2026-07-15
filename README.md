# <!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>直売所</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f9f9f9;
            color: #333;
            margin: 0;
            padding: 20px;
        }
        header {
            background-color: #4CAF50;
            color: white;
            padding: 10px 0;
            text-align: center;
        }
        .product {
            border: 2px solid #4CAF50;
            border-radius: 5px;
            margin: 10px 0;
            padding: 15px;
            background-color: #ffffff;
        }
        .comments {
            margin-top: 20px;
        }
        .comment {
            border-bottom: 1px solid #ddd;
            padding: 10px 0;
        }
        input[type="text"], input[type="submit"] {
            padding: 10px;
            margin: 5px 0;
            width: 100%;
        }
        button {
            background-color: #4CAF50;
            color: white;
            border: none;
            padding: 10px;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
    </style>
    <script type="module">
        // Firebase SDKの読み込み
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10/firebase-app.js";
        import { getFirestore, collection, addDoc, getDocs, orderBy, query } from "https://www.gstatic.com/firebasejs/10/firebase-firestore.js";

        // Firebase設定
        const firebaseConfig = {
            // ここに自分のconfigを貼る
        };

        // Firebase初期化
        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);

        document.addEventListener("DOMContentLoaded", async () => {
            const commentForm = document.getElementById("commentForm");
            const commentsList = document.getElementById("commentsList");

            commentForm.addEventListener("submit", async (e) => {
                e.preventDefault();
                const commentInput = document.getElementById("commentInput");
                const commentText = commentInput.value;

                if (commentText) {
                    await addDoc(collection(db, "comments"), {
                        text: commentText,
                        createdAt: new Date()
                    });
                    commentInput.value = '';
                    loadComments();
                }
            });

            const loadComments = async () => {
                commentsList.innerHTML = '';
                const commentsQuery = query(collection(db, "comments"), orderBy("createdAt", "desc"));
                const querySnapshot = await getDocs(commentsQuery);
                querySnapshot.forEach((doc) => {
                    const comment = document.createElement("div");
                    comment.className = "comment";
                    comment.textContent = doc.data().text;
                    commentsList.appendChild(comment);
                });
            };

            loadComments();
        });
    </script>
</head>
<body>
    <header>
        <h1>直売所</h1>
    </header>
    <!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>西条農業高校 野菜直売サイト</title>

<style>
body{
    font-family: sans-serif;
    background:#f4fff4;
    text-align:center;
    margin:0;
}

header{
    background:#2e8b57;
    color:white;
    padding:25px;
}

.container{
    display:flex;
    flex-wrap:wrap;
    justify-content:center;
    gap:20px;
    margin:30px;
}

.card{
    width:250px;
    background:white;
    border-radius:15px;
    box-shadow:0 0 10px rgba(0,0,0,0.2);
    overflow:hidden;
}

.card img{
    width:100%;
    height:180px;
    object-fit:cover;
}

.card h2{
    color:#2e8b57;
}

.card p{
    padding:10px;
}
</style>

</head>
<body>

<header>
<h1>🍅 西条農業高校 野菜直売サイト 🫑</h1>
<p>新鮮な野菜を販売しています！</p>
</header>

<div class="container">

<div class="card">
<img src="tomato.jpg" alt="ミニトマト">
<h2>ミニトマト</h2>
<p>甘くてジューシー！サラダにぴったり。</p>
</div>

<div class="card">
<img src="pepper.jpg" alt="ピーマン">
<h2>ピーマン</h2>
<p>肉厚で苦みが少なく食べやすい！</p>
</div>

<div class="card">
<img src="eggplant.jpg" alt="ナス">
<h2>ナス</h2>
<p>焼きナスや麻婆ナスにおすすめ！</p>
</div>

<div class="card">
<img src="shiso.jpg" alt="シソ">
<h2>シソ</h2>
<p>香り豊かで料理のアクセントに。</p>
</div>

<div class="card">
<img src="goya.jpg" alt="ゴーヤ">
<h2>ゴーヤ</h2>
<p>夏バテ予防にぴったりの野菜！</p>
</div>

</div>

</body>
</html>
    <section class="product">
        <h2>取り扱い商品</h2>
        <p>ミニトマトやナス、ピーマンは夏野菜でとてもみずみずしくおいしい。</p>
        <p>どの商品も１００グラム８０えん！</p>
    </section>

    <section class="comments">
        <h2>コメントを書いてね！</h2>
        <form id="commentForm">
            <input type="text" id="commentInput" placeholder="コメントを入力" required>
            <input type="submit" value="送信">
        </form>
        <h3>コメント一覧</h3>
        <div id="commentsList"></div>
    </section>

    <footer>
        <button>いいね</button>
    </footer>
</body>
</html>
-
