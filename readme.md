# QUICK START
npm i && node index.js

# PROCESS
大概流程

<pre>
var sess = req.session;
var loginUser = sess.loginUser;
var isLogined = !!loginUser;

/login
if(user)
    req.session.regenerate(function(err){   //建立session
        req.session.loginUser = user.name;
    }
else
    err

/logout
    req.session.destroy(function(err) {     //拿掉session
        res.redirect('./');
    }

LoginPage
<% if(isLogined){ %>
    已登入
<% }else{ %>
    <form method="POST" action="/login">
    請登入
</pre>
# Node_Modules
## EJS

根目錄的網頁用views/index.ejs渲染  
<pre>
index.js
app.set('views', 'views/');
app.set('view engine', 'ejs');
app.get('/', function(req, res, next) {
    res.render('index', {
        title : 'ejs'
    });
});
</pre>
index.ejs 所有<%= title %>都會變成ejs  

## body-parser
所有app.get的網站  
request進來的data 都轉成json  
<pre>
app.use(bodyParser.json());  
app.get('/', function(req, res,){});  
</pre>
## express-session
session 有幾個參數  
<pre>
app.use(session({
    name: identityKey,
    secret: 'your secret',         // 不知道能幹嘛Q 但一定要提供任意secrt才能運作
    store: new FileStore(),        // 本地端存放session
    //mongodb 存放session
    store: new MongoStore({ url: "mongodb://localhost:27017/mymondb" }),  
    saveUninitialized: false,      // 是否自动保存未初始化的会话，建议false
    resave: false,                 // 是否每次都重新保存会话，建议false
    cookie: {
        maxAge: 1000 * 1000        // 有效期，单位是毫秒
    }
})
</pre>
## session-file-store
同上面參數  
store: new FileStore(),  
只要取得session 就會把該session存放在session資料夾裡  

## connect-mongo
連接mongodb  

## cookie-parser
新版的 express-session 似乎不需要再裝這個套件  
