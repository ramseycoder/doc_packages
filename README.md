# doc_packages
bref documentation des packages que j'ai eu a recherché.

## express

  ce module permet de mettre en place un serveur web
  
  ` npm instal express`
  
 ```bash 
    const express = require('express');
    const app = express(); 
    app.get('/',(req,res)=>{  
     res.send('hello world')  
    })  
    app.listen(300);`
  ```
 
## socket.io

  ce module permet de réaliser une communication en temps réel entre le client et le serveur  
  
  ` npm install socket.io`
  
initalisation coté serveur
  
  ```bash
  const app = require('express')();
  const http = require('http').createServer(app);
  
  const io = require('io')(http);
  
  io.on('connection',(socket) =>{
    console.log("user connected");
    socket.on('message',()=>{
         socket.emit('message','hello world');
     });
   });`
   
  ```

  intialisation coté front

```bash
<html>
     <head>
        <meta charset = "utf-8">
     </head>
     <body>
        <script src="/socket.io/socket.io.js/"><script>
        <script>
            const socket = io();
            socket.emit('messsage');
            socket.on('message',(data)=>{
                console.log(data);
            }
        </script>
     </body>
  </html>
  
 ```

## express-socket.io-session

  ce module permet de partager une session de expresss avec socket.io
  
  `npm install express-socket.io-session`
  
  ```bash
    const app = require('express')();
    const http = require('http').createServer(app);
    const session = require('express-session')({
        secret: "ce que je suis",
        resave: true,
        saveUninitialized: true
      })
    const io = require('socket.io')(http);
    const sharedSession = require('express-socket.io-session');
    
    app.use(session)
    
    io.use(sharedSession(session))
    io.on('connection',(socket)=>{
        socket.on('lOGIN',(data)=>{
            session.handshake.session.userdata = data;
            session.handshake.session.save();
        });
        socket.on('LOGOUT',()=>{
          if(session.handshake.session.userdata){
            delete session.handshake.session.userdata;
            session.handshake.session.save();
          }
        }
    });
 ```
 
 ## mongoose
 
  mongoose est un module qui permet de communiquer plus simplement avec mongodb  a travers des schémas et des models
  
  `npm install mongoose`
  
  création de modèle avec mongoose
  
  ```bash 
    const mongoose = require('mongoose');
    const UserSchema = mongoose.Schema({
        name:{type:String},
        email:{type:String},
        password: {type: String},
    });
    const User = mongoose.model('user',UserSchema);
 ```
 
 // creation d'un modéle
 
 ```bash
    const User = require('./models/user.model') // on exporte notre modèle User qui se trouve dans le dossier models du                                                         répertoire courant
    
    const user = new User({
      name: "koffi",
      email: "rameaux.koffi@uvci.edu.ci",
      password: "nevergiveup,borntowin"
    });
    
    user.save().then(user=>{
       return user // retour  le user qui vient d'être insérer
    }).catch(er=>{
      return e  // retourne l'erreur qui a été recupérer.
    })
  ```
  
  // update d'un modèle
  
  ```bash
    User.find({email:"jean@gmail.com"}).then(user=>{
       return user // retour  le user qui vient d'être rechercher
    }).catch(er=>{
      return e  // retourne l'erreur qui a été recupérer.
    })
    
  ```
  
##  morgan

  morgan est ce package qui effectue les débogage sur les différents liens de vos pages, il vous donnes des infos tel que le status de la requête, le type de la requête , le nombre de secondes de l'éxécution.
  
  `npm install morgan `
  
  ```bash
    const app = require('express')();
    const morgan = require('morgan');
    app.use(morgan('dev'));
  ```
  
  
  
  


