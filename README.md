# react-app-fullstack-devconnector
A full stack react app using Mongo Express with JWT authentication


<li>
HOW TO SET UP BACKEND SERVER WITH NODEJS AND MONGODB

```const express = require('express');
const mongoose= require('mongoose');
const app =express();


//DB config
const db =require('./config/keys').mongoURI;

//COnnect to MongoDB
mongoose.connect(db)
.then(()=>console.log("MOngoDB connected"))
.catch((err)=>console.log(err))

app.get('/', (req,res)=>res.send('Hello ddddddd'));

const port =process.env.PORT || 5000;


app.listen(port,()=>console.log(`server running on port${port}`));
```
  
</li>