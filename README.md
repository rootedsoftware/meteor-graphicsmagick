I am using this dockerfile for Meteor + Graphicsmagick and using MUP to deploy it. 

Make this change to your mup.js file


    docker: {
      image: "joshjoe/meteor-graphicsmagick",
    },
    
Then make sure you are also making a volume available to docker if you want to map something to a permenant location so your files arenn't deleted when you do new mup deploys. 


    volumes: {
      "/opt/uploads": "/uploads"
    },
    
Here is my whole mup.js file for reference. 

```
module.exports = {
  servers: {
    one: {
      host: '1.2.3.4',
      username: 'myusername',
      pem:'/Users/mylocalusername/.ssh/do',
      opts: {
        port: 1235
      }
    }
  },
  meteor: {
    name: 'meteorapp',
    path: '/Users/mylocalusername/meteor/meteorapp',
    volumes: {
      "/opt/uploaddirectory": "/uploaddirectory"
    },
    docker: {
      image: "joshjoe/meteor-graphicsmagick",
    },
    servers: {
      one: {}
    },
    buildOptions: {
      debug: true,
      serverOnly: true,
    },
    env: {
      PORT: "80",
      ROOT_URL: 'http://subdomain.domain.com',
      MONGO_URL: 'mongodb://localhost/meteor'
    },
    deployCheckWaitTime: 120
  },
  mongo: {
    oplog: true,
    port: 27017,
    servers: {
      one: {},
    },
  },
};
```
