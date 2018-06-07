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



<li>
HOW TO CREATE A MODEL AND EXPORT IT

```const moongoose=require('moongose');
const Schema =mongoose.Schema;

//Create Schema
const UserSchema =new Schema({
    name:{
        type:String,
        required:true
    },
    email:{
        type:String,
        required:true
    },
    avatar:{
        type:String,
        required:true
    },
    data:{
        type:Date,
        default:Date.now
    }
});

module.exports=User=mongoose.model('users',UserSchema);
```
  
</li>