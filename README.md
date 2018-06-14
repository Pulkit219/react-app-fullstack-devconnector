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



<li>
HOW TO CREATE A TOKEN WITH JWT

```bcrypt.compare(password, user.password).then(isMatch => {
        if (isMatch) {
          // res.json({msg:'successs'});
         
          // User Matched
          const payload = { id: user.id, name: user.name, avatar: user.avatar }; // Create JWT Payload
  
          // Sign Token
          jwt.sign(
            payload,
            keys.secretOrKey,
            { expiresIn: 3600 },
            (err, token) => {
              res.json({
                success: true,
                token: 'Bearer ' + token
              });
            }
          );
        } else {
          // errors.password = 'Password incorrect';
          // return res.status(400).json(errors);
         
            res.status(400).json({password:"Password incorrect"});
          
        }
      });
```
  
</li>



<li>
HOW TO USE PASSPORT WITH JWT STRATEGY

```//Passport middleware
app.use(passport.initialize());
//Passport Config
require('./config/passport')(passport);



EXTRACTING JWT TOKEN INFO
const JwtStrategy = require('passport-jwt').Strategy;
const ExtractJwt = require('passport-jwt').ExtractJwt;
const mongoose = require('mongoose');
const User = mongoose.model('users');
const keys = require('../config/keys');

const opts = {};
opts.jwtFromRequest = ExtractJwt.fromAuthHeaderAsBearerToken();
opts.secretOrKey = keys.secretOrKey;

module.exports = passport => {
  passport.use(
    new JwtStrategy(opts, (jwt_payload, done) => {
      User.findById(jwt_payload.id)
        .then(user => {
          if (user) {
            return done(null, user);
          }
          return done(null, false);
        })
        .catch(err => console.log(err));
    })
  );
};


ADDING A MIDDLEWARE AND MAKING ROUTE PROTECTED
router.get('/current',passport.authenticate('jwt',{session:false}), (req,res)=>{
  res.json({
    id:req.user.id,
    name:req.user.name,
    email:req.user.email
  });
})

```
  
</li>

