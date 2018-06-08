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



<li>
HOW TO CREATE A NEW USER , SAVE IT TO MONGODB AND HASH THE PASSWORD USING BCRYPT

```const gravatar =require('gravatar');
const bcrypt=require('bcryptjs');

// @route   GET api/users/test
// @desc    Tests users route
// @access  Public
router.get('/test', (req,res)=>res.json({msg:"user works"}));


// @route   GET api/users/test
// @desc    Tests users route
// @access  Public
router.post('/register', (req, res) => {
    
    User.findOne({ email: req.body.email }).then(user => {
      if (user) {
        errors.email = 'Email already exists';
        return res.status(400).json(errors);
      } else {
        const avatar = gravatar.url(req.body.email, {
          s: '200', // Size
          r: 'pg', // Rating
          d: 'mm' // Default
        });
  
        const newUser = new User({
          name: req.body.name,
          email: req.body.email,
          avatar,
          password: req.body.password
        });
  
        bcrypt.genSalt(10, (err, salt) => {
          bcrypt.hash(newUser.password, salt, (err, hash) => {
            if (err) throw err;
            newUser.password = hash;
            newUser
              .save()
              .then(user => res.json(user))
              .catch(err => console.log(err));
          });
        });
      }
    });
  });
```
  
</li>